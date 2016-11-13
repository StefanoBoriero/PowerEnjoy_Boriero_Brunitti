![PolimiLogo](https://upload.wikimedia.org/wikipedia/it/b/be/Logo_Politecnico_Milano.png "Polimi")  

**PowerEnJoy project**  
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
	2.2 Product functions  
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


###1.4 Reference Documents  



###1.5 Overview  

<p style="page-break-before:always;"></p>  

#2 Overall Description  
###2.1 Product Perspective   


###2.2 Product Functions  


###2.3 User Characteristics  
There are two categories of users that will interact with the system: customers and employees.
A customer can be any person who is older than 18 years old and owns a driving license. In order to access the app, the customer will first need to register supllying some personal details.
An employee is a person who works for PowerEnJoy, thus managing and taking care of cars that need assistance. Their credentials to access the system will be given to them once they are hired.


###2.4 Scenarios  
**SCENARIO 1**  
Jenkins is a university student who just moved in town to attend lectures. He's concerned with pollution issues, so he often travels with public transport in the city, although he doesn't like it at all. A student that lives in town suggests him to try the PowerEnJoy service as he's really satisfied with it. Jenkins thinks that this service is what really suits its needs, as it offers an environment friendly way to travel in the city, so decides to register to the system. He surfs to the web application through a web browser, and starts the registration process: he enters all the information and waits for the password to be delivered. As soon as he has received it, he logs in.

**SCENARIO 2**  
William's car has suffered an accident last week, so he has been using PowerEnJoy to move around during these days. While preparing to go to work, he wants to check if there's any available car to reserve in order to get to work: to do so, he logs into the system and navigates to the "Reserve a car" functionality. Using its position, he reserves a car in a safe area near its home and walks to it. Once reached, he notices that one of the headlight is broken, so decides to report this damage to the system: he accesses the application and navigates to the "Report Damage" function, and fills a form to describe the kind of damage the car has. Since he cannot use this car, he has to look for another one: luckily there is another available car in the same safe area, so he reserves it and goes to work.

**SCENARIO 3**  
Poseidon works for PowerEnJoy to provide assistance to vehicles. His working day has just started, so he logs into the system to organize his schedule. He consults the assistance list to choose the nearest car to reserve, and finds that a car parked in a charging area near its position has a low level of battery and is not plugged: this looks like an easy task to him, so he takes in charge the vehicle and heads to the charging area. Once solved the issue, he accesses the application through the smartphone provided by the company to tag the issue as solved, then consults the assistance list to select his next task.

**SCENARIO 4**  
Andrew and his friends want to go to the cinema, but none of them have their car available at the moment. Andrew, however, is already registered to PowerEnJoy and decides to reserve a car for the evening. He opens the app, logs in and selects "reserve a car". Since he is on the train at the moment, he chooses to enter his home address as search area. He selects 500 m as search distance. He selects the nearest car. Once reached, Andrew uses the app to open the car. He then proceeds to pick up his two friends and then he drives to the cinema. After the movie, Andrew brings the two friends home and then parks the car in a safe area. Since he had at least two passengers, he gets a 20% discount on the total fee.

**SCENARIO 5**
Richard needs to go the airport, but there is nobody who is willing to bring him there. Since he doesn't want to pay a lot of money for parking in the airport parking, he decides to rent a car from PowerEnJoy. He reserves a car by means of the app and drives to the airport, leaving the car in the proximity of the airport. Since Richard didn't park in a safe area, the system keeps charging him for a given amount of time. After this amount of time, the car is locked and tagged as abandoned, and Richard isn't charged anymore. Subsequently, an employee sees that the car is abandoned. The employee takes in charge the case and goes where the car has been parked. Once there, he uses his copy of the key to enter the car and drives the car to the nearest charging area. Finally, he plugs the car to the electrical grid and uses his phone to tag the case as solved. In this way, the system will automatically tag the car as available again.


###2.5 Constraints  


###2.6 Assumptions and Dependencies  

<p style="page-break-before:always;"></p>  

#3 Specific Requirements  
###3.1 External Interface Requirements   
The system has to interface with external payment providers: in particular it must be able to request a payment and to retrieve the outcome of the payment. It also has to interface with Google Maps, as it will rely on it to show current position of vehicles.

###3.2 Functional Requirements  
####3.2.1 Requirements  
####3.2.2 Use Cases  
####3.2.3 Sequence Diagrams  
![Reservation Sequence Diagram](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/SequenceDiagram/Reservation Sequence diagram.jpg
"Reservation Sequence Diagram")  
![Report A Damage SequenceDiagram](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/SequenceDiagram/Damage Report Sequence Diagram.jpg
"Report a damage Sequence Diagram")
####3.2.4 Activity Diagrams  
![Payment ActivityDiagram](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/Payment_ActitvityDiagram.jpg "Payment Activity Diagram")
####3.2.5 State Chart Diagrams  
![Vehicle_StateChart](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/StateCharts/StateChart_Vehicle.jpg "Vehicle State Chart")

###3.3 Performance Requirements  


###3.4 Design Constraints  


###3.5 Software System Attributes  


###3.6 Other Requirements  



