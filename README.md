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

- /05/08/16 - Project creation, built dependencies and scaffolding, installed Node.js and npm.
- /05/08/15 - Set up basic project structure and configurations, connection to PostgresSQL db.
- /06/08/15 - Added polymer library component support
- /06/08/15 - Start developing UI prototypes 

## License

Copyright (c) 2016

Licensed under the [MIT license](LICENSE).
