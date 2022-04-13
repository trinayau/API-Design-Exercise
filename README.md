# FindYourNeighbour: An API Design Exercise

We are building a neighbourhood collaboration site and we want to make a system to keep track of people, houses, and addresses of those houses.

* Each person has a name, age and number of people in their household
* Each house has an address and an owner
* Each address has a postcode and street address

## The REST API will need to enable users to:
* Store people, houses and addresses
* Look up a house, its address and owner
* Look up people in our neighbourhood within certain age brackets and with specific household sizes

## Database 
### Consider the type of data we will be storing and type of database we should implement (SQL vs NoSQL)
SQL, as we have strict requirements for data and there should be no null values/empty fields. 
### Create a schema for this database
![Database Schema](Blank%20diagram.png)

### Consider the requests our API should be capable of handling
API should handle:
- Creating a new person, house and address record in database
- Changing your own records - person, house and address in database
- Deleting your own records - person, house and address in database
- Querying the database for house, its address and owner
- Querying the people table in the database for age brackets and household sizes

### List the routes you will need with their HTTP verb and path
Querying the database for house, its address and owner. 
* `GET /House`
* `GET /Address`
* `GET /Person`  

Querying the people table in the database for age brackets and household sizes. 
* `GET /Person/age?between=20+25&household=5`- Find person whose age is in the 20-25 bracket and belongs to a household of 5 people 

Creating a new person, house and address record in database. 
* 'GET /person/new` to receive form to fill out new person
* `POST /person` to add new person to person table in database
Changing your own records - person, house and address in database. 
* `GET /address/:id/edit` - Show user how to edit address
* `POST /address/:id` - Edit the address   

Deleting your own record. 
* `DELETE person/:id` - Deletes record of person with that id
* `DELETE house/:id` - Deletes record of house with that id
* `DELETE address/:id` - Deletes record of address with that id
### Determine the responses that should be returned and the content types of these requests and responses  
| Route                    | Response | Content Type                  |
|--------------------------|----------|-------------------------------|
| GET /house/new           |    200   |        HTML Doc - Form        |
| POST /house              |    201   |             JSON              |
| GET /house               |    200   |              JSON             |
| GET /house/:unhappyroute |    404   |             Error             |
| DELETE /house/:id        |    200   | HTML - Message to say deleted |
| GET /address/:id/edit    |    200   |        HTML Doc - Form        |
| POST /address/:id        |    201   |    JSON - Show new address    |
| DELETE /house/:idNotYourHouse |    403   |             Error        |


# Create documentation for your API on a tool of your choice
Using GitHub README:
This API uses GET/POST requests to communicate and HTTP response codes to indenticate status and errors. All responses come in standard JSON. All requests must include a content-type of application/json and the body must be valid JSON.

## URL
/house/:id
/person/:id
/address/:id

## Method
`GET` | `POST` | `DELETE`

## URL Parameters
Required:
`id=[integer]`  

Optional:
`/person/age?between=[integer]+[integer]`  - Find person of age between two integers
`/person/household=[integer]` - Find person with a household size of integer

## Data Parameters
If you make a post request, the body payload should look like this:
```
 {person name: STRING
  person age: INT
  household size: INT
  
  }
```

## Response Codes 
### Response Codes
```
200: Success
400: Bad request
401: Unauthorized
404: Cannot be found
405: Method not allowed
422: Unprocessable Entity 
50X: Server Error
```
