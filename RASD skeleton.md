![PolimiLogo](https://upload.wikimedia.org/wikipedia/it/b/be/Logo_Politecnico_Milano.png "Polimi")  

#PowerEnJoy project   
---
RASD v1
---
Boriero Stefano  
Brunitti Simone  
********
<p style="page-break-before:always;"></p>

### Table of contents  ###
1. **Introduction**  
  1.1 Purpose  
	1.2 Scope  
	1.3 Glossary  
	1.4 Reference documents  
	1.5 Overview  
2. **Overall description**  
	2.1 Product perspective  
	2.2 Goals  
	2.3 User characteristics  
	2.4 Scenarios  
	2.5 Constraints  
	2.6 Assumptions and dependecies  
3. **Specific Requirements**  
  3.1 External Interface Requirements  
  3.2 Functional Requirements  
  3.3 Performance Requirements  
  3.4 Design Constraints  
  3.5 Software System Attributes  
  3.6 Other Requirements  

<p style="page-break-before:always;"></p>

#1 Introduction   
###1.1 Purpose  
The purpose of Power Enjoy is to provide a green car sharing service, which allows users to rent electric supplied cars by means of both browser and mobile application.
The app requires the user to be registered to the system, by providing their credentials (including driving license) and payment information. Once registered, they can find the locations of the nearest available cars, from either their current position or a specified one, and reserve them. After the reservation, the car will be available for up to one hour. If the car is not picked up in the given time, a fee will be charged, and the car becomes available again. When the user reaches the reserved car, he can unlock it, using the app. During the ride, the user is charged a given amount of money per minute: the total fee is shown on a screen in the car. Once the car is parked in a safe area and the user exits the car, the system locks the car automatically and stops charging the user. The system incentivizes virtuous behaviours of the users by applying discounts.


###1.2 Scope  
The main focus of this RASD is to describe the PowerEnJoy App and the underlying system that will suppport it.  Since PowerEnJoy is a newborn startup, the system must necessarily be designed from scratch. This system will be interfaced with the PowerEnJoy App, which is a web Application and as such can be accessed either by means of a mobile device or a pc.  The system receives data from an android device installed on each car interfacing with various sensors  (additional details on sensors can be found in paragraph 2.6). Finally, the system will implement different functionalities that will be used by employees in order to manage and keep track of cars that need assistance.

###1.3 Glossary  
| Term       | Meaning           |
| ------------- |-------------|
| Debtor User    |A user with a negative balance |
| Signalled User   |A user with at least one rule infraction      |
| Banned User |A user with repeated infractions      |
| Regular user    |A user that is neither Debtor nor Banned |
| Active User |A user with one Active Reservation|
| Active Reservation    |A reservation which has not ended yet  |
| Safe Area   |A parking area defined by the company      |
| Charging Area |A special Safe Area with electric plugs used to charge the cars     |
| Personal Information    |Username and password, payment information, driving license |
| Balance   |Amount of money that user has deposited on his account and can still use to pay      |
| Passenger |Person in a car that is not driving    |
| Abandoned Car   |A car that has been parked outside a Safe Area for more than 5 straight hours      |
| Reserved Car |A car with an Active Reservation     |





###1.4 Reference Documents  
Car electronic equipment: [Electronic Control Unit - Wikipedia](https://en.wikipedia.org/wiki/Electronic_control_unit)


###1.5 Overview  

<p style="page-break-before:always;"></p>  

#2 Overall Description  
###2.1 Product Perspective   


###2.2 Goals  
The main goals this system is meant to offer the fulfillment of these goals:
- G1 Enable Regular users to reserve a car  
- G2 Unlock a reserved car  
- G3 Deposit money  
- G4 Enable employee to easily detect cars that need assistance  
- G5 Define the set of safe areas  
- G6 Discourage a bad usage of the services  



###2.3 User Characteristics  
There are two categories of users that will interact with the system: customers and employees.  
A customer can be any person who is older than 18 years old and owns a driving license. In order to access the app, the customer will first need to register supplying some personal details.  
An employee is a person who works for PowerEnJoy, thus managing and taking care of cars that need assistance. Their credentials to access the system will be given to them once they are hired.


###2.4 Scenarios  
**SCENARIO 1**  
Jenkins is a university student who just moved in town to attend lectures. He's concerned with pollution issues, so he often travels with public transport in the city, although he doesn't like it at all. A student that lives in town suggests him to try the PowerEnJoy service as he's really satisfied with it. Jenkins thinks that this service is what really suits its needs, as it offers an environment friendly way to move around the city, so decides to register to the system. He surfs to the web application through a web browser, and starts the registration process: he enters all the information and waits for the password to be delivered. As soon as he has received it, he logs in.

**SCENARIO 2**  
William's car has suffered an accident last week, so he has been using PowerEnJoy to move around during these days. While preparing to go to work, he wants to check if there's any available car to reserve in order to get to work: to do so, he logs into the system and navigates to the "Reserve a car" functionality. Using its position, he reserves a car in a safe area near its home and walks to it. Once reached, he notices that one of the headlight is broken, so decides to report this damage to the system: he accesses the application and navigates to the "Report Damage" function, and fills a form to describe the kind of damage the car has. Since he cannot use this car, he has to look for another one: luckily there is another available car in the same safe area, so he reserves it and goes to work.

**SCENARIO 3**  
Poseidon works for PowerEnJoy to provide assistance to vehicles. His working day has just started, so he logs into the system to organize his schedule. He consults the assistance list to choose the nearest car to reserve, and finds that a car parked in a charging area near its position has a low level of battery and is not plugged: this looks like an easy task to him, so he takes in charge the vehicle and heads to the charging area. Once solved the issue, he accesses the application through the smartphone provided by the company to tag the issue as solved, then consults the assistance list to select his next task.

**SCENARIO 4**  
Andrew and his friends want to go to the cinema, but none of them have their car available at the moment. Andrew, however, is already registered to PowerEnJoy and decides to reserve a car for the evening. He opens the app, logs in and selects "reserve a car". Since he is on the train at the moment, he chooses to enter his home address as search area. He selects 500 m as search distance. He selects the nearest car. Once reached, Andrew uses the app to open the car. He then proceeds to pick up his two friends and then he drives to the cinema. After the movie, Andrew brings the two friends home and then parks the car in a safe area. Since he had at least two passengers, he gets a 20% discount on the total fee.

**SCENARIO 5**  
Richard needs to go the airport, but there is nobody who is willing to bring him there. Since he doesn't want to pay a lot of money for parking in the airport parking, he decides to rent a car from PowerEnJoy. He reserves a car by means of the app and drives to the airport, leaving the car in the proximity of the airport. Since Richard didn't park in a safe area, the system keeps charging him for a given amount of time. After this amount of time, the car is locked and tagged as abandoned, and Richard isn't charged anymore. Subsequently, an employee sees that the car is abandoned. The employee takes in charge the case and goes where the car has been parked. Once there, he uses his copy of the key to enter the car and drives the car to the nearest charging area. Finally, he plugs the car to the electrical grid and uses his phone to tag the case as solved. In this way, the system will automatically tag the car as available again.


###2.5 Constraints  
####2.5.1 Regulations  
The user must give permission to the system to have access to his current position. Moreover, since the system has access to sensible information, including payment deatails, it needs to meet high security requirements.  

####2.5.2 Hardware Limitations  
-	Mobile: smartphone with 3G connection and access to a web browser
-	PC: access to an internet connection and a web browser

#####2.5.3 Parallelism  
The system supports parallelism, in order to be accessed by multiple customer and employees at any given time. To make this possible, the system will have to deal with critical situations, such as avoiding multiple reservations on the same car from different customers (the system will disable the selection of an available car from the map as soon as someone tries to reserve it, locking it for a given amount of time).

###2.6 Assumptions and Dependencies  

####2.6.1 Domain Assumptions  
* Every car is equipped with an Electronic Control Unit, consisting of the following components:  
	- Door Control Unit (DCU): actuators for opening and closing doors by remote control, sensors to capture actual state of doors  
	- Engine Control Unit (ECU): sensors to collect data and actuators to ensure optimal performances  
	- Seat Control Unit: sensors to detect the presence of passengers on the vehicle  
	- Telematic Control Unit (TCU): sensor to ensure vehicle tracking (GPS)  
	- Battery Managment System (BMS): sensors monitoring battery state  
* Every car is equipped with an on-board android device with GSM, GPRS, LTE and Wi-Ficommunication modules.  
* Cars can be opened with physical keys by company employees  
* The company provides employees with a smartphone during working hours to access the system while outside PowerEnJoy headquarter  
* Discounts are non-cumulative: in case of multiple applicable discounts, only the highest will be applied  
* A person doesn't have two driving licenses for the same category of vehicles  
* The number of passangers is non negative  
* Usernames are unique  
* Vehicles always unlock within one minute from the moment the user presses the unlock button
* When new vehicles are acquired by the company, its information is registered in the system by an employee
* When a vehicle is dismissed by the company, its information is cancelled from the system by an employee



<p style="page-break-before:always;"></p>  

#3 Specific Requirements  
###3.1 External Interface Requirements   
The system has to interface with external payment providers: in particular it must be able to request a payment and to retrieve the outcome of the payment. It also has to interface with Google Maps, as it will rely on it to show current position of vehicles.  
The on-board android device has to interface with the Electric Control Unit in order to access its sensors and actuators.

###3.2 Functional Requirements  

####3.2.1 Requirements  
In order to fulfill the above specified goals, the system has to provide these functionalities:  
- G1 Enable Regular users to reserve a car  
	- System is able to distinguish between Regular and non-Regular users  
	- System allows user to define search area (specific address or current position)  
	- System is able to retrieve user current position  
	- System is able to detect available cars within a specified area  
	- System is able to tag a car as reserved  
- G2 Unlock a reserved car  
	- System is able to retrieve user current position  
	- System is able to check if user is near the current reserved car  
	- System is able to unlock a car remotely  
- G3 Deposit money
	- System is able to interface with an external payment provider  
- G4 Enable employee to easily detect cars that need assistance  
	- System is able to detect if a car is in outside a safe area  
	- System is able to detect if a car has low battery   
	- System allows employee to access an assistance list containing all cars that need assistance  
	- System is able to notify the employee if a new car is added to the assistance list  
	- System allows employee to take charge of a car in assistance list  
	- System is able to tag car as TookInCharge  
	- System allows employees to register a new car in the fleet  
	- System allows employees to remove a car from the fleet  
- G5 Define the set of safe areas  
	- System allows employees to define a safe area on a map corresponding to a real world safe area  
- G6 Discourage bad usage of the services
	- System is able to tag user as a debtor if his balance is negative  
	- System is able to disable reservation functions for debtors  
	- Notify the user if he has been tagged as debtor  
	- System Is able to charge 30% more on the ride if the car is left more than 3 km from the nearest power station or left with less than 20% battery  
	- System is able to charge 1 EUR to a user who doesn't pick up the car before the given timer expires  
	- System is able to tag a user who infringed the rules as Signalled user  
	- System is able to ban a fraudulent user preventing him to access the services  



####3.2.2 Use Cases  
![Use Case](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/UseCases/UseCase.jpg "System UseCase")

#### Event Flows  

**NAME** : Registration  
**ACTORS** : Unregistered user  
**PRECONDITION** : None    
**EVENT FLOW** :  
  -	An Unregistered user opens the application: he's prompted to the login page
  -	Clicks on the "Register" button
  -	He is asked personal information, including payment information
  -	If the registration is successful, he receives back the password to log into the system
  
**POSTCONDITION** : The Unregistered user becomes Registered user and can log into the system  
**EXCEPTION** :  
  -	The registration fails because the Unregistered user didn’t fill in all necessary information
  -	The registration fails because some information is in conflict with another user
  -	The registration fails because payment information is incorrect
  
____ 
  
**NAME**: Reserve a car  
**ACTORS**: Active User  
**PRECONDITION**: The user must be logged in the app and must be on the homepage. The user must not be tagged as debtor.  
**EVENT FLOW**:    
- The user selects "Reserve a car" functionality from the menu: he's prompted to the "reserve a car" page
- The user selects the desired search area (either entering  a specific address or selecting to use the current position).
- The user inserts the desired search distance and presses the "search" button. The user is prompted to the "select a car" page.
- The user selects one of the available cars from the map.

**POSTCONDITION**: The reservation is forwarded to the system. The system tags the selected car as reserved and initialiazes a 1h timeout for that specific car. The user is tagged as active.  
**EXCEPTION**:  
- The user enters an invalid distance ( for axample a negative number) or an invalid search address. The reservation is not forwarded and the system asks to enter a valid value.  

____  
**NAME** : 
  Unlock Reserved car  
**ACTORS** : 
  Active User  
**PRECONDITION** : 
  The Registered user has reserved a car, has logged in and is on the home page  
**EVENT FLOW** :
  -	The user selects "Unlock car" functionality from the menu: he's prompted to the Unlock Reserved Car page
  -	He clicks the "Unlock" button and the car opens
  
**POSTCONDITION** : The car is open and the user can access it  
**EXCEPTION** :
  -	The user has GPS sensor switched off: the system will ask him to switch it on before prompting him to the Unlock Reserved Car page
  -	The user is too far from the car: the button won't be clickable

____ 
  
**NAME** : 
  Damage Report  
**ACTORS** :
  Active user  
**PRECONDITION**: 
  The user has reserved a car that has some damages, has logged in and is on the home page  
**EVENT FLOW**:
  -	The user selects "Report Damage" functionality from the menu: he's prompted to the Report Damage page
  -	He fills in a form describing the kind of damage the car has
  -	He clicks the "Submit" button to send the report
  
**POSTCONDITION** : 
  The company receives the report and becomes aware of the damage  
**EXCEPTION** : 
  none

____  

  
**NAME**: Deposit money to personal balance  
**ACTORS**: Active User  
**PRECONDITION**: The user must be logged in the app and must be on the homepage  
**EVENT FLOW**:  
- The user selects "Access personal area" functionality from the menu: he's prompted to the "Personal Area"page.
- He selects "Deposit money" functionality on the "Personal Area" page: he's prompted to the "Deposit Money" page.
- The user selects the amount of money he wants to deposit from a list of predefined amounts and clicks the "Deposit" button.

**POSTCONDITION**: The system updates the user account balance.  
**EXCEPTION**:
- The user tries to deposit more money than he has on his credit card. The system shows the user an error message and the balance is not updated.

____ 

 
**NAME** : Edit personal information  
**ACTORS**: Active User  
**PRECONDITION**: The user must be logged in the app and must be on the homepage.  
**EVENT FLOW**:  
 - The user selects "Access personal area" functionality from the menu: he's prompted to the personal area page.
 - He selects "Edit personal information" functionality on the "personal area " page: he's prompted to the Edit personal information page.
 - The user edits his personal information (such as payment details, email etc.) using a form.
 - The user presses the "save" button.
 
**POSTCONDITION**: The new personal information is saved in the system.  
**EXCEPTION**:
- The user enters invalid payment information or invalid values. The system reverts the changes and asks the user to enter valid infomation.

____


**NAME**: Take in charge a vehicle  
**ACTORS**: Employee  
**PRECONDITIONS** :  
An employee wants to check if there's any vehicle that needs assistance and take care of it  
**EVENT FLOW** :  
-	The employee selects the "Take in Charge" function from the home menu
-	The system shows the vehicles that need assistance, with information concerning the issue
-	The employee selects one of them
-	The employee clicks on the "Take in Charge" button

**POSTCONDITIONS** : 
	The vehicle is tagged as Took in Charge, and is no longer listed among those that need assistance  
**EXCEPTIONS** :
-	The vehicle has just been taken in charge by another employee: the system will show an error message

____ 

**NAME** : Tag as solved  
**ACTORS** : Employee  
**PRECONDITION** : An undesired event occurred to one of the car. A manual setting of its state is needed. The employee has logged in with his credential and is on the home page  
**EVENT FLOW** :
-	The employee selects the "Tag as solved" function
-	The system shows him the list of the vehicle he's currently taking care of
-	He selects the vehicle he has assisted
-	He clicks on "Tag as Solved" button

**POSTCONDITIONS** :
-	The car is tagged as Available and is no longer in the employee's list of currently taken in charge vehicles

**EXCEPTIONS**:  the issue was not solved and the car needs assistance again  

____  
 
**NAME**: Add safe parking area  
**ACTORS**: Employee  
**PRECONDITION**: The employee must be logged in the system and be on the employee homepage.  
**EVENT FLOW**:  
- The employee selects "Add a safe parking area" functionality from the menu: he's prompted to the "Add a safe parking area"page.
- The "Add a safe parking area" page contains a map where the employee can draw polygons that define safe parking areas. The employee draws a safe area and saves.
 
**POSTCONDITION**: The new safe areas are saved in the system and are sent to all cars GPS system.  
**EXCEPTION**: None

____  
 
**NAME**: Add a car to the fleet  
**ACTORS**: Employee  
**PRECONDITION**: The employee must be logged in the system and be on the employee homepage.  
**EVENT FLOW**:    
- The employee selects "Add a car" functionality from the menu: he's prompted to the "Add a car"page
- The "Add a car" page contains a form asking the plate of the car and the mac address of the android device installed on it. The employee fills the form
- The employee clicks the add button

**POSTCONDITION**: The new car is added to the fleet of PowerEnJoy cars.  
**EXCEPTION**:  
- The employee enters an invalid mac address or plate number. The system asks to fill the form again.

____  

####3.2.3 Sequence Diagrams  
![Reservation Sequence Diagram](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/SequenceDiagram/Reservation Sequence diagram.jpg
"Reservation Sequence Diagram")

____  

![Report A Damage SequenceDiagram](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/SequenceDiagram/Damage Report Sequence Diagram.jpg
"Report a damage Sequence Diagram")

____  

![Unlocking Car SequenceDiagram](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/SequenceDiagram/Unlocking%20Car%20Sequence%20Diagram.jpg
"Unlock Car Sequence Diagram")

____  

####3.2.4 Activity Diagrams  
![Payment ActivityDiagram](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/Payment_ActitvityDiagram.jpg "Payment Activity Diagram")

____  


####3.2.5 State Chart Diagrams  
![Vehicle_StateChart](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/StateCharts/StateChart_Vehicle.jpg "Vehicle State Chart")

____  

####3.2.6 Class Diagram
![ClassDiagram](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/Class%20Diagram.jpg
"ClassDiagram")

____  

###3.3 Performance Requirements  


###3.4 Design Constraints  


###3.5 Software System Attributes  


###3.6 Other Requirements  



