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



###1.2 Scope  


###1.3 Glossary  


###1.4 Reference Documents  



###1.5 Overview  

<p style="page-break-before:always;"></p>  

#2 Overall Description  
###2.1 Product Perspective   


###2.2 Product Functions  


###2.3 User Characteristics  


###2.4 Scenarios  
**SCENARIO 1**  
Jenkins is a university student who just moved in town to attend lectures. He's concerned with pollution issues, so he often travels with public transport in the city, although he doesn't like it at all. A student that lives in town suggests him to try the PowerEnJoy service as he's really satisfied with it. Jenkins thinks that this service is what really suits its needs, as it offers an environment friendly way to travel in the city, so decides to register to the system. He surfs to the web application through a web browser, and starts the registration process: he enters all the information and waits for the password to be delivered. As soon as he has received it, he logs in.

**SCENARIO 2**  
William's car has suffered an accident last week, so he has been using PowerEnJoy to move around during these days. While preparing to go to work, he wants to check if there's any available car to reserve in order to get to work: to do so, he logs into the system and navigates to the "Reserve a car" functionality. Using its position, he reserves a car in a safe area near its home and walks to it. Once reached, he notices that one of the headlight is broken, so decides to report this damage to the system: he accesses the application and navigates to the "Report Damage" function, and fills a form to describe the kind of damage the car has. Since he cannot use this car, he has to look for another one: luckily there is another available car in the same safe area, so he reserves it and goes to work.

**SCENARIO 3**  
Poseidon works for PowerEnJoy to provide assistance to vehicles. His working day has just started, so he logs into the system to organize his schedule. He consults the assistance list to choose the nearest car to reserve, and finds that a car parked in a charging area near its position has a low level of battery and is not plugged: this looks like an easy task to him, so he takes in charge the vehicle and heads to the charging area. Once solved the issue, he accesses the application through the smartphone provided by the company to tag the issue as solved, then consults the assistance list to select his next task.


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
![Reservation Sequence Diagram](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti//blob/master/SequenceDiagram/Reservation Sequence diagram.jpg
"Reservation Sequence Diagram")
####3.2.4 Activity Diagrams  
![Payment ActivityDiagram](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/Payment_ActitvityDiagram.jpg "Payment Activity Diagram")
####3.2.5 State Chart Diagrams  
![Vehicle_StateChart](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/StateCharts/StateChart_Vehicle.jpg "Vehicle State Chart")

###3.3 Performance Requirements  


###3.4 Design Constraints  


###3.5 Software System Attributes  


###3.6 Other Requirements  



