# Headlines
> A Simple REST API for matching headlines to employees

Headlines provides a RESTful API for matching headlines to employees of interest. Each headline has an associated  ```location_of_interest```. Headlines are matched to employees based on a match between the employee's ```location``` and the
headline's ```location_of_interest```. Passing a date to Headlines will:
1) Retrieve all headlines that were published on that date (```pubclication_date == date```).
2) Return:
    - The list of matching headlines
    - for each headline: A list of employees whose ```location``` matches the ```location_of_interest``` of the headline.
Data is currently mock data, generated with the help of some publicly-available data generators. See more info in the 
credits section

## Usage

- GET /headlines/<DATE_STRING> will return all headlines whose publication date matches <DATE_STRING> and employees who match on location of interest.

## Installation and Configuration
Set your environment variables as defined below. Create a ```.env``` file in the main Headlines directory. Add environment variables as described below.

From within the main Headlines directory simply run
```javascript
npm start
```
The ```package.json``` uses ```nodemon``` to restart the server in response to e.g. code changes

### MongoDB
This project was built using MongoDB community edition on MacOS as described [here](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/ "Official Mongo CE on OS/X tutorial"). YMMV but as long as you can establish connectivity through the connection string in the Environment Variables section below you should be fine.

### Environment Variables
As mentioned above Headlines uses a .env file in the project directory to store environment specific variables. Make sure to edit that file to include variables for your specific environment:
```
- PORT: The port on which the headlines server listens
- MONGO_CONNECTION: Connection string to the mongo instance
- EMPLOYEE_FILE: The data file containing the employee data
- HEADLINE_FILE: The data file containing the headline data
```
Note that data files are included in the project in the `data` subdirectory. The environment variables that reference them need to include the path relative to the main oproject directory (e.g. `data/headlines.json`)

## Testing
Test scripts are written in node.js and use the [Request](https://github.com/request/request "Request project page") and [Mocha](https://mochajs.org/ "Mocha project page") js libraries.

### Running tests
From within the project directory simply run 
```javascript
npm test
```
to run the built-in test suite. Tests run under mocha, which is referenced in the package.json file in the main directory.

For inspection and/or tinkering see the test/tests.js file


## Structure
Headlines accepts a date parameter and retrieves all headlines whose *publication_date* match the passed parameter. Headlines will then inspect the *location_of_interest* property and retrieves all employees with a matching *location*. Headlines then retrieves those employees. If successful the reponse is structured as follows:
```javascript
{
  headlines:
  [
   { 
		 author: ""
     abstract: ""
     ...
     employees: [
     {
      id: "",
      name: "",
      lcoation: ""
      ...
     },
     ...
	}
  ]
```

## Future Enhancements
- Enhance Security
  - Better Rest Authentication
  - Stricter authentication requirements between the API backend and Mongo
- Implement data streaming to handle larger data sets
- Enhance matching algorithm
  - Allow multiple locations of interest in the headline data
- Better handling of date filter parameter. The current implementation requires a specific date format and will not match any headlines for proper dates in different formats.
- Include secure REST calls for CRUD operations on Employee and Headline data
- Enhance filtering capabilities
  - Allow a range of dates
  - Allow other headline filters
  - Allow employee filters


# Credits
- Data Generated using:	 https://www.onlinedatagenerator.com/

