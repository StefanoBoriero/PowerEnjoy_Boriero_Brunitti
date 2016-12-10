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
![ComponentInterfaces](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/ComponentsInterfaces.md "ComponentsInt")  
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

####2.4.2 State Diagrams
![UserStatus]
(https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/StateDiagrams/UserStateDiagram.jpg
"UserStatus")

###2.5 Component interfaces 
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
