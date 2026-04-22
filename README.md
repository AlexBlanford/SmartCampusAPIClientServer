# Build and Run

Open the terminal to the project foler and run:
mvn clean install
mvn exec:java


Base URL:

http://localhost:8080/api/v1




# Sample curl Commands

### 1. Discovery


curl http://localhost:8080/api/v1


### 2. Create Room


curl -X POST http://localhost:8080/api/v1/rooms \
-H "Content-Type: application/json" \
-d "{\"id\":\"LIB-301\",\"name\":\"Library\",\"capacity\":50}"


### 3. Get Rooms


curl http://localhost:8080/api/v1/rooms


### 4. Create Sensor


curl -X POST http://localhost:8080/api/v1/sensors \
-H "Content-Type: application/json" \
-d "{\"id\":\"TEMP-001\",\"type\":\"Temperature\",\"status\":\"ACTIVE\",\"currentValue\":22.5,\"roomId\":\"LIB-301\"}"


### 5. Filter Sensors


curl http://localhost:8080/api/v1/sensors?type=Temperature


### 6. Add Reading


curl -X POST http://localhost:8080/api/v1/sensors/TEMP-001/readings \
-H "Content-Type: application/json" \
-d "{\"id\":\"READ-001\",\"timestamp\":1710000000000,\"value\":24.8}"


### 7. Get Readings


curl http://localhost:8080/api/v1/sensors/TEMP-001/readings



# Report Answers

### Part 1.1

In JAX-RS, resource classes usually have a request scope, which means that a new instance is made for each request. Because of this, shared data shouldn't be kept in the resource itself. Instead, shared data is kept in static structures so that it can be accessed by more than one request.

### Part 1.2

Hypermedia (HATEOAS) lets clients find out what actions and resources are available in real time through API responses. This makes the API less dependent on outside documentation and makes it easier to change as it grows.

### Part 2.1

Sending back only IDs makes the payload smaller and speeds up performance, but it gives the client less information. Returning full objects gives more information, but it also makes the response bigger

### Part 2.2

DELETE is idempotent because calling it more than once gives the same final result. Once a room is deleted, more DELETE requests don't change the state of the system.

### Part 3.1

The server may reject a request from a client if it has an unsupported content type like 'text/plain' or 'application/xml' because the endpoint expects JSON. This usually gets a 415 Unsupported Media Type response

### Part 3.2

Using @QueryParam is better for filtering because it lets you filter in different ways while keeping the resource path the same. It can handle more requests than making separate endpoints for each filter

### Part 4.1

The Sub-Resource Locator pattern puts nested resources into their own classes. This makes the API easier to maintain and helps organize the code

### Part 4.2

The sensor's "currentValue" is updated right away when a new reading is added. This makes sure that the sensor always shows the most recent reading

### Part 5.2

HTTP 422 is better than 404 because the request is valid, but the data given is wrong (for example, it points to a room that doesn't exist).

### Part 5.4

Exposing stack traces can show private information about the program's structure, like file names and class names. Hackers can use this to learn about the system and take advantage of it

### Part 5.5

Using filters for logging is better because logging is something that affects many parts of the system. Instead of repeating code at every endpoint, filters let you handle logging in one place
