![PolimiLogo]

\#PowerEnJoy project
--------------------

Design Document
---------------

### Boriero Stefano 876106

### Brunitti Simone 875039

version: 1.0\
release date: December 11th, 2016\
\*\*\*\*\*\*\*\*\
<p style="page-break-before:always;"></p>

### Table of contents

1.  **Introduction**
    -   1.1 Purpose\
    -   1.2 Scope\
    -   1.3 Glossary\
    -   1.4 Reference documents\
2.  **Architectural design**
    -   2.1 Overview
    -   2.2 Component view
    -   2.3 Deployment view\
    -   2.4 Runtime view
        -   2.4.1 Sequence Diagrams
        -   2.4.2 State Diagrams\
    -   2.5 Component interfaces\
    -   2.6 Selected architectural styles and patterns
        -   2.6.1 General architecture
        -   2.6.2 Design decisions
        -   2.6.3 Design patterns

-   2.7 Other design decisions

1.  **Algorithm design**\
2.  **User interface design**
    -   4.1 UX Diagrams
    -   4.2 Mock-Ups
3.  **Requirements traceability**
4.  **Effort spent**

<p style="page-break-before:always;"></p>
1 Introduction
==============

### 1.1 Purpose

### 1.2 Scope

### 1.3 Glossary

### 1.4 Reference Documents

2 Architectural design
======================

### 2.1 Overview

### 2.2 Component view

![ComponentInterfaces]

### 2.3 Deployment view

### 2.4 Runtime view

#### 2.4.1 Sequence Diagrams

#### Customer Login

\[UnlockCar\]\
(<https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/SequenceDiagrams/login%20sequence%20diagram%20alternative%20version.jpg>\
“CustomerLogin”)

##### Description

When the user inputs his login credentials in the application, the
application must compare this information with the one contained in the
database. To do so, the application sends a request to the Client
Dispatcher, which transfers the request to the Account Controller. The
Account Controller queries the database to retrieve the password
corresponding to the input username and subsequently compares the two
passwords. If the comparison is positive, the account controller
retrieves the user status and sends it to the application. Finallly, the
application shows the client a different screen depending on the user
status (if the client is a debtor he can’t reserve, so that button will
be disabled).

------------------------------------------------------------------------

#### Reserve a car

\[ReserveCar\]\
(<https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/SequenceDiagrams/Client_reservation_sequence.jpg>\
“ReserveCar”)

#### Description

When the client selects to navigate to the reservation page from the
menu, the app will ask the client to select a search position and a
search radius. When the client picks a position, the app will contact
the Reservation Controller running on the server by means of the Client
Dispatcher. The reservation Controller will then query the DB in order
to obtain all the positions of the vehic

  [PolimiLogo]: https://upload.wikimedia.org/wikipedia/it/b/be/Logo_Politecnico_Milano.png
    "Polimi"
  [ComponentInterfaces]: https://github.com/StefanoBoriero/PowerEnjoy_Boriero_Brunitti/blob/master/DesignDocument/Components/ComponentsInterfaces.md
    "ComponentsInt"