### Reserve a car
![ReserveCar]
(https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/SequenceDiagrams/Client_reservation_sequence.jpg
"ReserveCar")
##Description 
When the client selects to navigate to the reservation page from the menu, the app will ask the client to select a search position and a search radius. When the client picks a position, the app will contact the Reservation Controller running on the server by means of the Client Dispatcher. The reservation Controller will then query the DB in order to obtain all the positions of the vehicles which are in the selcted search area. This information is passed to the client app, which uses it to create a map using Google Maps API. Finally, when the user selects a vehicle, a reservation request is sent to the Reservation Controller that will create a new reservation and will change the vehicle status to reserved (starting a 1 hour timer if the reservartion is successfull). Finallly, the client app will show a message indicating the outcome of the operation.
