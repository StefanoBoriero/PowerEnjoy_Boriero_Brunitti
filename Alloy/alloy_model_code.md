```alloy
abstract sig Boolean{}
one sig True extends Boolean{}
one sig False extends Boolean{}

sig Credential{}
sig Plate{}

abstract sig BatteryLevel{}
one sig High extends BatteryLevel{}
one sig Medium extends BatteryLevel {}
one sig Low extends BatteryLevel{}

abstract sig Position{}
sig InSafeArea extends Position{}
sig NearSafeArea extends Position{}
sig FarFromSafeArea extends Position{}

abstract sig DistanceFromCurrentReservedCar{}
sig Far extends DistanceFromCurrentReservedCar{}
sig Near extends DistanceFromCurrentReservedCar{}

one sig Company{
	vehicles: set Vehicle,
	employees: set Employee,
	safeAreas: set SafeArea
}
{
	#vehicles > 0
	#employees >0
}

abstract sig User{
	credential: Credential
}

sig Customer extends User{
	distance: lone DistanceFromCurrentReservedCar,
	balance: Int,
	vehicleInUse: lone Vehicle,
	banned: one Boolean
}

sig Employee extends User{
	vehiclesInCharge: set Vehicle
}

sig Vehicle{
	battery: one BatteryLevel,
	position: one Position,
	opened: one Boolean,
	damaged: one Boolean,
	seats: one Int
}
{
	seats > 0
}

sig Ride{
	passengers: one Int,
	finalPosition: lone Position
}
{
	passengers >=0
}

sig Reservation{
	user: one Customer,
	vehicle: one Vehicle,
	timeExpired: Boolean,
	ride: lone Ride
}
{
	timeExpired = True implies ride = none
}

sig Plug{
	chargingVehicle: lone Vehicle
}

sig SafeArea{}
sig ChargingArea extends SafeArea{
	plugs: set Plug
}

/**
PREDICATES
**/
//Predicates over Customers
pred isDebtor[c: Customer]{
	c.balance < 0
}
pred isBanned[c: Customer]{
	c.banned = True
}
pred isRegular[c: Customer]{
	!isDebtor[c] and !isBanned[c]
 }
pred hasAnActiveReservationForVehicle[c: Customer, v:Vehicle]{
	one r: Reservation | r.user = c and r.vehicle = v and isActive[r]
}
pred hasAnActiveReservation[c:Customer]{
	one r: Reservation | r.user = c and isActive[r]
}

//Predicates over Vehicles
pred isAvailable[v: Vehicle]{not isReserved[v] and not needAssistance[v]}
pred isReserved[v: Vehicle]{one r: Reservation | r.vehicle = v and isActive[r]}
pred isAbandoned[v: Vehicle]{one r: Reservation | abandonedVehicle[r] and r.ride.finalPosition = v.position}
pred needAssistance[v: Vehicle]{ isAbandoned[v] or (v.battery = Low and (not isCharging[v])) or v.damaged = True }
pred inUse[v:Vehicle]{ one r: Reservation | r.vehicle = v and isActive[r]
}
pred isCharging[v: Vehicle]{
	one p: Plug | p.chargingVehicle = v
}
pred isTookInCharge[v: Vehicle]{
	one e:Employee | v in e.vehiclesInCharge
}

//Predicates over Rides
pred isEnded[ride: Ride]{
	ride.finalPosition != none
}

//Predicates over Reservations
pred missedPickUp[res: Reservation]{
	res.timeExpired = True and
	res.ride = none}
pred abandonedVehicle[res: Reservation]{
	not isActive[res] and
	not missedPickUp[res] and
	res.ride.finalPosition not in InSafeArea}
pred isActive[res: Reservation]{
	res.timeExpired = False and 
	( res.ride = none or not isEnded[res.ride] )
}

//Predicates over Plugs
pred isUsed[p: Plug]{
	p.chargingVehicle != none
}

/**
FACTS
**/
fact noRideWithoutReservation{
	all ri: Ride| one res: Reservation | ri in res.ride
}
fact reserveOnlyAvailableVehicles{all r: Reservation | isReserved[r.vehicle]}
fact noTwoUserWithSameCredential{no disjoint u1,u2: User | u1.credential = u2.credential}
fact passengersMustNotExceedSeats{all r: Reservation | r.ride != none implies r.ride.passengers < r.vehicle.seats}
fact noTwoActiveReservationFromSameUser{no disjoint r1,r2: Reservation | r1.user = r2.user and isActive[r1] and isActive[r2] }
fact noTwoActiveReservationForSameVehicle{no disjoint r1,r2: Reservation | r1.vehicle = r2.vehicle and isActive[r1] and isActive[r2]}

fact noVehiclePluggedMoreThanOnce{
	all p: Plug, v: Vehicle | v in p.chargingVehicle implies v not in (Plug - p).chargingVehicle
}
fact noPlugWithoutChargingArea{
	all p: Plug | one c: ChargingArea | p in c.plugs
}
fact noChargingVehicleIsUsed{
	no c: ChargingArea, c1: Customer | 
	c.plugs.chargingVehicle &
	c1.vehicleInUse != none
}
fact carOpenOnlyIfReserved{
	all v: Vehicle | v.opened = True implies isReserved[v]
}

fact noTwoUsersDrivingSameCar{
	no disjoint c1,c2: Customer | c1.vehicleInUse = c2.vehicleInUse
}
fact noTwoSameCredentials{
	no disjoint u1,u2: User | u1.credential = u2.credential
}
fact allVehiclesBelongsToCompany{
	all v:Vehicle | v in Company.vehicles
}
fact allEmployeesWorkForCompany{
	all e: Employee | e in Company.employees
}
fact noTwoEmployeeCareSameVehicle{
	all disjoint e1, e2: Employee | e1.vehiclesInCharge & e2.vehiclesInCharge = none
}
fact takeInChargeOnlyNeedyVehicles{
	all v: Vehicle | isTookInCharge[v] implies needAssistance[v]
}
fact distanceFromVehicle{
	all u: User| u.distance != none implies hasAnActiveReservation[u]
}
fact reservedVehiclesAreInUse{
	all c: Customer | all v: Vehicle | hasAnActiveReservationForVehicle[c,v] iff c.vehicleInUse = v
}
fact allSafeAreasBelongToCompany{
	no s: SafeArea | s not in Company.safeAreas
}

/**
ASSERTIONS
**/
assert noPlugInDifferentChargingArea{
	no p: Plug, disjoint c1, c2: ChargingArea | p in c1.plugs and p in c2.plugs
}

assert noSameRideForDifferentReservation{
	no ri:Ride, disjoint res1, res2: Reservation | ri in res1.ride and ri in res2.ride
}

assert noTwoPlugInSameVehicle{
	no disjoint p1, p2: Plug | p1.chargingVehicle != none and p2.chargingVehicle != none and p1.chargingVehicle = p2.chargingVehicle
}

assert noTwoEmployeesWorkOnSameVehicle{
	all v:Vehicle | no disjoint e1, e2: Employee | v in e1.vehiclesInCharge and v in e2.vehiclesInCharge
}

/**
PREDICATES TO RUN
**/
pred reserveVehicle[c: Customer, v: Vehicle, c': Customer, v': Vehicle]{
	//Preconditions
	isRegular[c] and
	not hasAnActiveReservation[c] and
	isAvailable[v] and

	//Postconditions
	isReserved[v'] and
	one r:Reservation | r.user = c' and r.vehicle = v' and isActive[r] and
	c'.vehicleInUse = v'
}

pred unlockVehicle[c, c': Customer, v,v':Vehicle]{
	//Preconditions
	hasAnActiveReservationForVehicle[c,v]
	c.distance = Near
	v.opened = False

	//Postconditions
	v'.opened = True
	v.position = v'.position
	v.battery = v'.battery
	v.seats = v'.seats
	c.distance = c'.distance
	c.balance = c'.balance
	hasAnActiveReservationForVehicle[c',v']
}

pred takeInCharge[e, e': Employee, v, v': Vehicle]{
	//Precondition
	needAssistance[v]
	not isTookInCharge[v]

	//Postconditions
	needAssistance[v']
	isTookInCharge[v']
	e'.vehiclesInCharge != e.vehiclesInCharge
	v' in e'.vehiclesInCharge
}
pred show{

}
run show for 3
check noPlugInDifferentChargingArea
check noSameRideForDifferentReservation
check noTwoPlugInSameVehicle
check noTwoEmployeesWorkOnSameVehicle
run reserveVehicle
run unlockVehicle
run takeInCharge
```
