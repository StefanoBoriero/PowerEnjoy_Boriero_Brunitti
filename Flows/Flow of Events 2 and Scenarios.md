**User reserves a car**  
**NAME**: User reserves a car  
**ACTORS**: User  
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

**User edits personal information**  
**NAME** :  User edits personal information  
**ACTORS**: User  
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

**User deposits money to personal balance**  
**NAME**: User deposits money to personal balance  
**ACTORS**: User  
**PRECONDITION**: The user must be logged in the app and must be on the homepage  
**EVENT FLOW**:  
- The user selects "Access personal area" functionality from the menu: he's prompted to the "Personal Area"page.
- He selects "Deposit money" functionality on the "Personal Area" page: he's prompted to the "Deposit Money" page.
- The user selects the amount of money he wants to deposit from a list of predefined amounts and clicks the "Deposit" button.

**POSTCONDITION**: The system updates the user account balance.  
**EXCEPTION**:
- The user tries to deposit more money than he has on his credit card. The system shows the user an error message and the balance is not updated.

____  

**Employee adds a safe parking area**  
**NAME**: Employee adds safe parking area  
**ACTORS**: Employee  
**PRECONDITION**: The employee must be logged in the system and be on the employee homepage.  
**EVENT FLOW**:  
- The employee selects "Add a safe parking area" functionality from the menu: he's prompted to the "Add a safe parking area"page.
- The "Add a safe parking area" page contains a map where the employee can draw polygons that define safe parking areas. The employee draws a safe area and saves.
 
**POSTCONDITION**: The new safe areas are saved in the system and are sent to all cars GPS system.  
**EXCEPTION**: None

____  

**Employee adds a car to the fleet**  
**NAME**: Employee adds a car to the fleet  
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


Andrew and his friends want to go to the cinema, but none of them have their car available at the moment. Andrew, however, 
is already registered to PowerEnJoy and decides to reserve a car for the evening. He opens the app, logs in and selects 
"reserve a car". Since he is on the train at the moment, he chooses to enter his home address as search area. He selects 500
m as search distance. He selects the nearest car. Once reached, Andrew uses the app to open the car. He then proceeds to pick
up his two friends and then he drives to the cinema. After the movie, Andrew brings the two friends home and then parks the car in a safe area. Since he had at least two passengers, he gets a 20% discount on the total fee.


Richard needs to go the airport, but there is nobody who is willing to bring him there. Since he doesn't want to pay a lot of money
for parking in the airport parking, he decides to rent a car from PowerEnJoy. He reserves a car by means of the app and drives to the
airport, leaving the car in the proximity of the airport. Since Richard didn't park in a safe area, the system keeps charging him for
a given amount of time. After this amount of time, the car is locked and tagged as abandoned, and Richard isn't charged anymore.
Subsequently, an employee sees that the car is abandoned. The employee takes in charge the case and goes where the car has been parked. Once there, he uses his copy of the key to enter the car and drives the car to the nearest charging area. Finally, he plugs the car to the electrical grid and uses his phone to tag the case as solved. In this way, the system will automatically tag the car as available again.

Simone Brunitti 05/11/2016 2:30h
