# CapstoneProject

> SeatFilla website by Dale/Richard

## SeatFilla
SeatFilla Information here

##Technologies
This project uses [Feathers](http://feathersjs.com). An open source web framework for building modern real-time applications.
Feathers sits on top of some very powerful javascript frameworks such as Node.js, SocketIO and Express.js. 

## Getting Started

Getting up and running is as easy as 1, 2, 3.

1. Make sure you have [NodeJS](https://nodejs.org/) and [npm](https://www.npmjs.com/) installed.
2. Install your dependencies
    
    ```
    cd path/to/CapstoneProject; npm install
    ```

3. Start your app
    
    ```
    npm start
    ```

## Testing

Simply run `npm test` and all your tests in the `test/` directory will be run.

##Project structure

- config contains a default.json and production.json application configuration file for things like the database connection strings and other configuration options.
public is the publicly hosted folder with the homepage
- src contains all the application source files
- hooks will contain global hooks
- middleware contains Express middleware
- services has a folder for each service. A service has an index.js and a hooks folder for service specific hooks
- app.js is the main application file which can be imported to test services
- index.js imports app.js and starts the server on the ports set in the configuration file
- test contains test files for the app, services and hooks

## Scaffolding

Feathers has a powerful command line interface. Here are a few things it can do:

```
$ npm install -g feathers-cli             # Install Feathers CLI

$ feathers generate service               # Generate a new Service
$ feathers generate hook                  # Generate a new Hook
$ feathers generate model                 # Generate a new Model
$ feathers help                           # Show all commands
```

## Help

For more information on all the things you can do with Feathers visit [docs.feathersjs.com](http://docs.feathersjs.com).

## Changelog

__0.1.0__

- Project proposal handed in
- /05/08/16 - Project creation, built dependencies and scaffolding, installed Node.js and npm.
- /05/08/15 - Set up basic project structure and configurations, connection to PostgresSQL db.
- /06/08/15 - Added polymer library component support
- /06/08/15 - UI Prototypes added, assets obtained although still looking
- /07/08/15 - Research into feathers/node.js/socket IO/express js
- /08/08/15 - Research continued
- /09/08/15 - Research continued
- /09/08/15 - Added bootstrap support
- /10/08/15 - User interface design begins

__0.1.1__


- /07/08/15 - Created /Interest service
              

## Todo:

SeatFilla scope

1.	Component based website using polymer/bootstrap/CSS/html5

1.1 Website:

-	View 3rd party supplied flights in real time (as they are pushed)
-	Create flight requests
-	Ability for suppliers to auction the flight or offer a flight for a fixed price
-	Users can bid on auctioned flights in real time
-	Latest bids on flights
-	Latest bought flight routes
-	Flight tracking/delay (updates a user if there’s any flight delays on an accepted flight)
-	Template engine

1.2 Control panel for customers:

-	View active requests
-	Cancel active requests
-	View status of requests (whether they have been accepted)
-	Confirm offers (that have been accepted)

1.3 Suppliers interface (convenience, API can be used)

-	View requests in real time
-	Accept requests in real time
-	View API documentation
-	View charts based on API usage

2.	Backend server in node.js/express.js/socket IO 

3.	Local login system /Single sign on (Login via Facebook, Instagram, Twitter)

4.	Authentication using JWT (API authentication tokens and login tokens)

5.	Backend database (PostgreSQL or NoSQL tbc)

6.	Payment system (Charge/Credit customers/3rd party suppliers)

7.	Available on android/IOS through porting 

8.	RESTful API (Details supplied below)

Flight requests – Service no.1

The service is responsible for creating a flight request to fly between a specific departure and arrival airport, between the specified date ranges, within certain predicates set by the requester.
Registered users of SeatFilla will create these requests. 3rd party users of SeatFilla will be able to query created requests to find willing applicants for their flights. 

Airlines and third party suppliers will then be able to find users interested flying between these destinations 

Methods:

GET SeatFilla.com/api/FlightRequest – Gets a flight request matching the specified criteria (TBD)

An example request may look like:

 (Note these are subject to change and just ideas of what a request may look like)

‘Requests’: [
}
          ‘DepartureAirport’Code: ‘AKL’,
          ‘ArrivalAirportCode’ : ’LAX’,
          ‘RequestID’: ‘xxxx-xxxx-xxxx-xxxx’ (UUID)
          ‘Applicant’: {
		ApplicantID: ‘xxxx-xxxx-xxxx-xxxx’ (UUID)
	 },
	‘FromDate’:  ISO DATE,
           ‘FromDateTo’: ISO DATE,
	‘RequiresReturn’: True/False,
	‘ReturnDate’: ISO DATE,
	‘ReturnDateTo’: ISO DATE,
	‘NoTicketsRequired’: INTEGER,
	‘MaximumPayment’ :  INTEGER,
	‘RequestTime’ : ISO DATE,
	‘RequestDate’: ISO DATE
}
]

POST SeatFilla.com/api/FlightRequest -  Creates a flight request (requires API token for creation)

PUT SeatFilla.com/api/FlightRequest  - Update the specified request (with same API token that created the request)

DELETE SeatFilla.com/api/FlightRequest – Deletes the specified request (with matching auth token)


Extras:

-	Create a hook on this service, update supplier interface in real time, notify web hook listeners.
-	Allow registration of web hook on this service when a create or delete operation occurs.


Flight Accept - Service no.2

Methods:

POST SeatFilla.com/api/FlightAccept

3rd party suppliers making use of api/FlightRequest request will also be able to make use of api/FlightAccept in order to accept any user offers on flights.

	[Requires verified authentication token]
  	
	{
	     RequestID: (ID of the request being accepted)
	     AuthToken: xxxx-xxxx-xxxx-xxxx
      	     ExpirationDate: ISO DATE (expiration date of the offer)
	     ExpirationTime: ISO TIME (expiration time of the offer)
	     ‘ConfirmationURL’:
	}

(Here the flight requester has until expiration date and time to confirm payment for the flight, at which point his account will be charged and the 3rd party suppliers account credited)

Extras:

-	Web hook to notify 3rd party users of a confirmed/denied flight request
-	Create hook to send user a notification, if they are online.     
-	Create hook to email, txt and notify user of flight being accepted.
-	Charge user who created the request a small fee


Flight Offer (Auction/Fixed price) - Service no.3 

(This is new and was not included in our project scope)

The flight offer service will allow 3rd party suppliers to ‘offer’ flights to SeatFilla, and SeatFilla will display them in real time, seat filler will also use any requests it has received for flights as prime candidates for an offered flight and also display it via the website/app.

If the offered flight is a fixed price it will be displayed on the SeatFilla website and users of SeatFilla will be able to purchase it directly.

If the offered flight is auction, the 3rd party supplier provides a minimum selling point, it is listed on our site from that price and SeatFilla users can bid in real time on the the offered flight until the expiration date, at which point the user is charged.

Methods:

GET SeatFilla.com/api/FlightOffer – Retrieves all flight offers
Search flight offer (between departure/arrival airport through the API)

POST SeatFilla.com/api/FlightOffer - Create a flight offer (Auction/Fixed price) (Collect flight details, provider details) (Live update through web sockets)

PUT SeatFilla.com/api/FlightOffer  - Update a flight offer

DELETE SeatFilla.com/api/FlightOffer - Remove a flight offer (With API token that created the request)


 Note: Create hook for create/remove from user interface

Analytics - Service No.4

Methods:

GET Seatfilla.com/api/SeatFillaAnalytics 

Obtain data/historical data from SeatFilla about purchase habits and flight popularity between certain dates/times


Additional requests (Panel/Lecturers):

## License

Copyright (c) 2016

Licensed under the [MIT license](LICENSE).
