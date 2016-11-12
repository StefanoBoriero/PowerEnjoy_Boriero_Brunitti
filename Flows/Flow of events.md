Scenario
John wants to register to the system in order to benefit of the car sharing. He accesses the web application and selects to register.
Once he filled in a form with all the information needed, he submits it.
After checking all the information, the system sends him the password to log in.  
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


SCENARIO:
Jack is in front of the car he reserved. He wants to unlock it, so he opens the application and navigates to the "Unlock car" function.
As his GPS sensor is switched off, the system asks him to turn it on in order to check his position.
Once the system enables him, he clicks on the unlock button and the car opens.  
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



SCENARIO
Singleton has reserved a car, and now stands in front of it. He notices that the car is damaged, so decides to report it.
He opens the application and navigates to the "Report damage" function. He fills in a form describing the kind of damage the car has, 
then sends it by clicking the "Submit" button.  
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

**EXCEPTIONS**:  the issue was not solved

Stefano Boriero 05/11/2016 2:30h
