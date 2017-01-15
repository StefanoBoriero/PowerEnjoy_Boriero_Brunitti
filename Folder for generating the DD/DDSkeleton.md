![PolimiLogo](https://upload.wikimedia.org/wikipedia/it/b/be/Logo_Politecnico_Milano.png "Polimi")  

#PowerEnJoy project   
---
Design Document
---

###Boriero Stefano  876106  
###Brunitti Simone   875039  
version: 1.0  
release date: December 11th, 2016
********
<p style="page-break-before:always;"></p>

### Table of contents  ###
1. **Introduction**  
  	* 1.1 Purpose  
	* 1.2 Scope  
	* 1.3 Glossary  
	* 1.4 Reference documents  
2. **Architectural design**  
	* 2.1 Overview 
	* 2.2 Component view  
	* 2.3 Deployment view  
	* 2.4 Runtime view
		* 2.4.1 Sequence Diagrams 
		* 2.4.2 State Diagrams    
	* 2.5 Component interfaces    
	* 2.6 Selected architectural styles and	patterns  
		* 2.6.1 General architecture 
		* 2.6.2 Design decisions
		* 2.6.3 Design patterns
  * 2.7 Other design decisions
3. **Algorithm design**  
4. **User interface design**
	* 4.1 UX Diagrams
	* 4.2 Mock-Ups
5. **Requirements traceability**
6. **Effort spent**

<p style="page-break-before:always;"></p>

#1 Introduction   
###1.1 Purpose 
###1.2 Scope 
###1.3 Glossary 
###1.4 Reference Documents 
#2 Architectural design 
###2.1 Overview  
###2.2 Component view  
![ComponentInterfaces](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/ComponentView.jpg "Component view")  
###2.3 Deployment view 
###2.4 Runtime view 
####2.4.1 Sequence Diagrams
#### Customer Login
![UnlockCar]
(https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/SequenceDiagrams/login%20sequence%20diagram%20alternative%20version.jpg
"CustomerLogin")
#####Description
When the user inputs his login credentials in the application, the application must compare this information with the one contained in the database. To do so, the application sends a request to the Client Dispatcher, which transfers the request to the Account Controller. The Account Controller queries the database to retrieve the password corresponding to the input username and subsequently compares the two passwords. If the comparison is positive, the account controller retrieves the user status and sends it to the application. Finallly, the application shows the client a different screen depending on the user status (if the client is a debtor he can't reserve, so that button will be disabled). 

____
#### Reserve a car
![ReserveCar]
(https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/SequenceDiagrams/Client_reservation_sequence.jpg
"ReserveCar")
####Description 
When the client selects to navigate to the reservation page from the menu, the app will ask the client to select a search position and a search radius. When the client picks a position, the app will contact the Reservation Controller running on the server by means of the Client Dispatcher. The reservation Controller will then query the DB in order to obtain all the positions of the vehicles which are in the selcted search area. This information is passed to the client app, which uses it to create a map using Google Maps API. Finally, when the user selects a vehicle, a reservation request is sent to the Reservation Controller that will create a new reservation and will change the vehicle status to reserved (starting a 1 hour timer if the reservartion is successfull). Finallly, the client app will show a message indicating the outcome of the operation.
____ 
#### Unlock Reserved car
![UnlockCar]
(https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/SequenceDiagrams/Unlock_car_sequence_diagram.jpg
"UnlockCar")
####Description
When the client selects to navigate to the unlock car page, the Client Application will display a page containing an «unlock car» button. If the user presses this button, the client will get the current device position and send a request to unlock the reserved car  to the Car Controller using the Client Dispatcher. When the Car Controller receives this request, it will query the DB to ask for the car that has been reserved by that particular user (if a reservation exists). If a reservation has been made, the Car Controller will compare the two sets of  coordinates and check if the car can be unlocked. If this is the case, the Car Controller will update the status off the car in the DB and wiil finally unlock the car, sending a message to the Car Application. Finally, the Client Application will display a message outlining the outcome of the operation.  
____  
#### End Ride  
![EndRide]
(https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/SequenceDiagrams/endRideSequence.jpg
"End of Ride")  
####Description  
When engine stops, the on-board car application sends a notification to the server throught the CarAppDispatcher. The RideController will collect all the information regarding the ride using the CarController. If the ride has actually ended (i.e. the car has been parked in a safe area or has been abandoned) the RideController will delegate the calculation of the bill to BillController. When the BillController receives the request, it will calculate the import of the bill according ti company policy, check if any discount is applicable than delegate the payment to BalanceController. This component will query the database to get user's current balance and update it. If after the update the balance is negative, user's status is updated to debtor and a notification is sent to her.


####2.4.2 State Diagrams
![UserStatus]
(https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/StateDiagrams/UserStateDiagram.jpg
"UserStatus")

###2.5 Component interfaces  
#### Registration Controller
![RegistrationController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/RegistrationController.jpg "RegistrationController")  
* INTERFACE:  
 * __register(personal_info)__ checks if the informations are valid, then the user is added to the database  
   * __InvalidInformationException__ this exception is raised if the information are incorrect  
* USES:  
 * __databaseController__

#### Account Controller
![AccountController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/AccountController.jpg "AccountController")
* INTERFACE:
 * __login():__ enables users to log in  
 * __get_personal_info():__ gets user's personal information from the database  
 * __edit_personal_info():__ updates user's personal information in the database  
* USES:
 * __databaseController__  
 
#### Reservation Controller
![ReservationController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/ReservationController.jpg "ReservationController")  
* INTERFACE:
 * __get_near_vehicles(position_information):__ gets from the database the cars available near the selected position  
 * __create_reservation(vehicle_id):__ creates a new reservation in the database; the selected car won't be available anymore
   * __UnavailableCarException:__ this exception is raised if the selected car is no longer available (another user has reserved it while he was looking at the map)  
 * __delete_reservation(reservation_id):__ ends the reservation if either the user hasn't unlocked the car or the time hasn't expired; the reserved car will be available  
* USES:
 * __databaseController__  

#### Balance Controller  
![BalanceController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/BalanceController.jpg "BalanceController")  
* INTERFACE:
 * __deposit(payment_provider, amount, user):__ adds to user's balance the indicated amount of money  
   * __TransactionException:__ this exception is raised if the transaction fails  
 * __pay(amount, user):__ subtracts the amount of a bill: if the balance becomes negative, a notification is sent to the user
* USES: 
 * __databaseController__  
 * __paymentGateway__  
 * __notificationGateway__
 
#### Report Controller  
![ReportController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/ReportController.jpg "ReportController")  
* INTERFACE:
  * __report_damage(report_form):__ adds the car which the report is about in the assistance list  
* USES:
  * __assistanceController__

#### Safe Area Controller  
![SafeAreaController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/SafeAreaController.jpg "SafeAreaController")  
* INTERFACE: 
 * __get_safe_areas():__ queries the database to get the set of safe areas already defined  
 * __create_safe_area(boundaries):__ updates the database by adding a new safe area  
   * __OverlapException:__ this exception is raised if a newly defined safe area overlaps an already defined one  
* USES:
 * __databaseController__  
 
#### Assistance Controller  
![AssistanceController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/AssistanceController.jpg "AssistanceController")  
* INTERFACE:  
 * __add(vehicle_id):__ adds the vehicle to the assistance list; it will no longer be available to reservation  
 * __take_in_charge(vehicle_id, employee_id):__ removes the vehicle from the assitance list as an employee will take care of the car  
   * __NotNeedyVehicleException:__ this exception is raised if the vehicle specified is not in the list (i.e. some other employee has taken it in charge while he was choosing what to do)  
 * __solved(vehicle_id):__ updates the database to set the vehicle as available as the issue was solved  
* USES:  
 * __databaseController__  
 
 #### Car Controller  
![CarController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/CarController.jpg "CarController")  
* INTERFACE:  
  * __unlock_car(user_information):__ checks if the user is near the reserved car, than forwards the unlock command to the car application  
    * __TooFarException:__ this exception is raised if the user is not close to the car  
    * __CannotUnlockException:__ this exception is raised if the opening fails  
  * __get_car_data(data_type):__ dialogs with on-board car application to get the specified data, and updates the database   
* USES:  
  * __ECUDataCollector__  
  * __carActuator__  
  * __databaseController__  
  
#### Ride Controller  
![RideController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/RideController.jpg "RideController")  
* INTERFACE:  
  * __start_ride():__ starts the monitoring of car during the ride  
  * __end_ride(ride_info):__ ends the ride, collects all the data to calculate the bill and forwards them to the dedicated component  
* USES:  
  * __carController__    
  * __billController__  
  
#### Bill Controller  
![BillController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/BillController.jpg "BillController")  
* INTERFACE:  
  * __calculate_bill(ride_info):__ calculates the amount of the bill, than forwards it to the component dedicated to its application    
* USES:  
  * __balanceController__  
  
#### Fault Controller  
![FaultController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/FaultController.jpg "FaultController")  
* INTERFACE:  
  * __notify_fault(fault_info):__ receives the information regarding some issues detected by on-board application and adds the car to the assistance list  
* USES:  
 * __assistanceController__  
 
#### Fleet Controller 
![FleetController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/FleetController.jpg "FleetController")  
* INTERFACE:  
 * __register_car(car_info):__ adds a new car to the fleet  
  * __AlreadyRegisteredException:__ this exception is raised if the car is already registered in the fleet  
 * __dismiss_car(car_info):__ removes a car from the fleet  
* USES:  
 * __databaseController__  

#### Car Application
![CarAppController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/CarApplication.jpg "CarApplication")   
* INTERFACE:  
 * __get_data(data_type)__ gets the required data from the ECU  
 * __unlock()__ unlocks the car via its actuators  
* USES:  
 * __carAppDispatcher  
 
#### Payment Gateway  
![PaymentGateway](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/PaymentGateway.jpg "PaymentGateway")  
* INTERFACE:  
 * __forward_payment(payment_info)__ forwards the payment request to the selected payment provider after a deposit has been requested  
* USES:
 * __externalPaymentProvider__  
 
#### Notification Gateway  
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

#### Employee Dispatcher
![EmployeeDispatcher](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/EmployeeDispatcher.jpg "EmployeeDispatcher") 
* INTERFACE:  
  * __dispatch_request(request_info):__ forwards employee's request to the dedicated component  
* USES:  
  * __safeAreaController__  
  * __assistanceController__  

#### CarApp Dispatcher  
![CarAppDispatcher](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/CarAppDispatcher.jpg "CarAppDispatcher")  
* INTERFACE:  
  * __dispatch_request(request_info):__ forwards request of car application to the dedicated component  
* USES:  
  * __fleetController__  
  * __faultController__  
  * __rideController__  
  
###2.6 Selected architectural styles and patterns
####2.6.1 General architecture  
The overall architecture we will adopt to develop the PowerEnJoy platform will be a **three-tier** architecture with distributed logic. Using this architecture, we will be able to decouple the business logic layer from the presentation and the data layers.
Our central system (where we can find the data layer and most of the business logic) needs to communicate both with the user and the vehicles. To achieve this communication, we will use:  
-A **client-server** architectural style for the communication with the user. In this case, the client is the user device (pc or mobile device). The client side takes care of the presentation logic and will also contain some business logic (mainly the one used to communicate with the Google Maps service). We will however try to keep the client as thin as possible.  
-An **event based** paradigm for the communication between the central system and the vehicles. Since the vehicles will need to notify state changes, the central system will register itself as a listener to all the vehicles and will act accordingly to these state changes. Moreover, the car must expose some methods to the central system (such as the one to unlock the car).  

####2.6.2 Design Decisions: 
**Google Maps API**: the user device will interact directly with Google Maps services through Google Maps APIs. This will allow the device to display useful maps used by the user to access PowerEnjoy services.  
**Java Persistence API**: we will use JPA for accessing, persisting, and managing our database, since JPA is already implemented in JEE.  

####2.6.3 Design Patterns:
**Client-server**: as aforementioned in the introduction of this chapter, we will make large use of the Client-Server design pattern, using it in the communication between the user device and the central system. To achieve this, the server will expose some methods (using a REST architecture) that will be used by the client to access the PowerEnJoy platform services.  
**Component-Based**: the server side of the system is structured following a component-based style. This decision gives the opportunity to divide the business logic into different parts, enabling developers to focus their work on single components. The product will also be scalable, as adding new functionalities would result in developing new components, leaving the existing structure unaltered.  
**JEE**: we will develop the system using JEE to develop a reliable system in a faster time. Security requirements will be more easily fulfilled using consolidated practices, as well as performance ones. The component-based style will also be reflected in the JEE Bean structure.  
**Adapter**: we will be using many interfaces between the components of our central system. In order to implement these interfaces, we will need to adopt the adapter design pattern.  

###2.7 Other design decisions 
#3 Algorithm design 
![PricingAlgorithm]
(https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Algorithms/pricing%20algorithm.jpg
"PricingAlgorithm")
#4 User interface design 
###4.1 UX Diagrams
#### Client UX Diagram
![ClientUX]
(https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/UXDiagrams/UXClient.jpg
"ClientUX")
____ 
#### Employee UX Diagram
![EmployeeUX]
(https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/UXDiagrams/EmployeeUX.jpg
"EmployeeUX") 

###4.2 Mock-Ups

#5 Requirements traceability 
#6 Effort spent 
