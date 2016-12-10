### Registration Controller
![RegistrationController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/RegistrationController.jpg "RegistrationController")  
* INTERFACE:  
 * __register(personal_info)__ checks if the informations are valid, then the user is added to the database  
   * __InvalidInformationException__ this exception is raised if the information are incorrect  
* USES:  
 * __databaseController__


### Account Controller
![AccountController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/AccountController.jpg "AccountController")
* INTERFACE:
 * __login():__ enables users to log in  
 * __getPersonalInfo():__ gets user's personal information from the database  
 * __editPersonalInfo():__ updates user's personal information in the database  
* USES:
 * __databaseController__  
 
### Reservation Controller
![ReservationController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/ReservationController.jpg "ReservationController")  
* INTERFACE:
 * __getNearVehicles(position_information):__ gets from the database the cars available near the selected position  
 * __createReservation(vehicle_id):__ creates a new reservation in the database; the selected car won't be available anymore
   * __UnavailableCarException:__ this exception is raised if the selected car is not available (another user has reserved it while he was looking at the map)  
 * __deleteReservation(reservation_id):__ ends the reservation if either the user hasn't unlocked the car or the time hasn't expired; the reserved car will be available  
* USES:
 * __databaseController__  

### Balance Controller  
![BalanceController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/BalanceController.jpg "BalanceController")  
* INTERFACE:
 * __deposit(payment_provider, amount, user):__ adds to user's balance the indicated amount of money  
   * __TransactionException:__ this exception is raised if the transaction fails  
 * __pay(amount, user):__ subtracts the amount of a bill: if the balance becomes negative, a notification is sent to the user
* USES: 
 * __databaseController__  
 * __paymentGateway__  
 * __notificationGateway__
 
### Report Controller  
![ReportController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/ReportController.jpg "ReportController")  
* INTERFACE:
  * __reportDamage(report_form):__ adds the car which the report is about in the assistance list  
* USES:
  * __assistanceController__

### Safe Area Controller  
![SafeAreaController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/SafeAreaController.jpg "SafeAreaController")  
* INTERFACE: 
 * __getSafeAreas():__ queries the database to get the set of safe areas already defined  
 * __createSafeArea(boundaries):__ updates the database by adding a new safe area  
   * __OverlapException:__ this exception is raised if a newly defined safe area overlaps an already defined one  
* USES:
 * __databaseController__  
 
### Assistance Controller  
![AssistanceController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/AssistanceController.jpg "AssistanceController")  
* INTERFACE:  
 * __add(vehicle_id):__ adds the vehicle to the assistance list; it will no longer be available to reservation  
 * __takeInCharge(vehicle_id, employee_id):__ removes the vehicle from the assitance list as an employee will take care of the car  
   * __NotNeedyVehicleException:__ this exception is raised if the vehicle specified is not in the list (i.e. some other employee has taken it in charge while he was choosing what to do)  
 * __solved(vehicle_id):__ updates the database to set the vehicle as available as the issue was solved  
* USES:  
 * __databaseController__  
 
 ### Car Controller  
![CarController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/CarController.jpg "CarController")  
* INTERFACE:  
  * __unlockCar(user_information):__ checks if the user is near the reserved car, than forwards the unlock command to the car application  
    * __TooFarException:__ this exception is raised if the user is not close to the car  
    * __CannotUnlockException:__ this exception is raised if the opening fails  
  * __getCarData(data_type):__ dialogs with on-board car application to get the specified data, and updates the database   
* USES:  
  * __ECUDataCollector__  
  * __carActuator__  
  * __databaseController__  
  
### Ride Controller  
![RideController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/RideController.jpg "RideController")  
* INTERFACE:  
  * __startRide():__ starts the monitoring of car during the ride  
  * __endRide():__ ends the ride, collects all the data to calculate the bill and forwards them to the dedicated component  
* USES:  
  * __carController__    
  * __billController__  
  
### Bill Controller  
![BillController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/BillController.jpg "BillController")  
* INTERFACE:  
  * __calculateBill(ride_info):__ calculates the amount of the bill, than forwards it to the component dedicated to its application    
* USES:  
  * __balanceController__  
  
### Fault Controller  
![FaultController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/FaultController.jpg "FaultController")  
* INTERFACE:  
  * __notifyFault(fault_info):__ receives the information regarding some issues detected by on-board application and adds the car to the assistance list  
* USES:  
 * __assistanceController__  
 
### Fleet Controller 
![FleetController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/FleetController.jpg "FleetController")  
* INTERFACE:  
 * __registerCar(car_info):__ adds a new car to the fleet  
  * __AlreadyRegisteredException:__ this exception is raised if the car is already registered in the fleet  
 * __dismissCar(car_info):__ removes a car from the fleet  
* USES:  
 * __databaseController__  

### Car Application
![CarAppController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/CarApplication.jpg "CarApplication")   
* INTERFACE:  
 * __getData(data_type)__ gets the required data from the ECU  
 * __unlock()__ unlocks the car via its actuators  
* USES:  
 * __none__  
 
### Payment Gateway  
![PaymentGateway](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/PaymentGateway.jpg "PaymentGateway")  
* INTERFACE:  
 * __forward_payment(payment_info)__ forwards the payment request to the selected payment provider after a deposit has been requested  
* USES:
 * __externalPaymentProvider__  
 
### Notification Gateway  
![NotificationGateway](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/NotificationGateway.jpg "NotificationGateway")  
* INTERFACE:  
 * __notify(user, info):__ notifies the user after a relevant event has occurred  
* USES:
 * __none__

### Client Dispatcher  
![ClientDispatcher](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/ClientDispatcher.jpg "ClientDispatcher")  
* INTERFACE:  
  * __dispatch_request(request_info):__ forwards client's request to the dedicated component  
* USES:  
  * __registrationController__  
  * __accountController__  
  * __reservationController__  
  * __balanceController__  
  * __reportController__  

### Employee Dispatcher
![EmployeeDispatcher](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/EmployeeDispatcher.jpg "EmployeeDispatcher") 
* INTERFACE:  
  * __dispatchRequest(request_info):__ forwards employee's request to the dedicated component  
* USES:  
  * __safeAreaController__  
  * __assistanceController__  

### CarApp Dispatcher  
![CarAppDispatcher](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/CarAppDispatcher.jpg "CarAppDispatcher")  
* INTERFACE:  
  * __dispatchRequest(request_info):__ forwards request of car application to the dedicated component  
* USES:  
  * __fleetController__  
  * __faultController__  
  * __rideController__  
