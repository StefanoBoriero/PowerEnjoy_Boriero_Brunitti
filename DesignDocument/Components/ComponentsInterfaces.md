
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
 * __deposit(payment_provider, amount):__ adds to user's balance the indicated amount of money  
  * __TransactionException:__ this exception is raised if the transaction fails
* USES: 
 * __databaseController__  
 * __paymentGateway__  
 
### Report Controller  
![ReportController](https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/Images/ReportController.jpg "ReportController")  
* INTERFACE:
  * __reportDamage(report_form):__ adds the car which the report is about in the assistance list  
* USES:
  * __assistanceController__
