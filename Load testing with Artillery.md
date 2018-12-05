# Load Testing on a Website

### Author: Neerali Chauhan, Shoaib Merchant

Load Testing is the process of subjecting a website or an application to high real-life load conditions. This testing helps to determine how the website will perform when multiple users access it simultaneously. We use [Artillery](https://artillery.io/) for load testing.

Artillery is a modern, powerful & easy-to-use load testing toolkit. It is used to check how much scalable and resilient the application is under high load.

  - Artillery requires [Node.js](https://nodejs.org/) v4+ to run.
 
# Install Artillery

Once Node.js is installed, install Artillery with:
```sh
$ npm install -g artillery
```
To check that the installation succeeded, run:
```sh
$ artillery -V
```
You can see the version of artillery installed on the system.
# Run test on Artillery
Artillery is able to simulate the realistic user behavior with scenarios.
- Create a `hello.yml` file and copy the following code in it.
```scala
config:
  target: 'https://www.abc.com'
  phases:
    - duration: 60
      arrivalRate: 4
  defaults:
    headers:
      x-my-service-auth: 'load-check'
scenarios:
  - flow:
    - get:
        url: "/docs"
    - get:
        url: "/introduction"
```
### Description
- **config** is the part where target is defined.
- **target** is the server which is under load testing.
- **duration** and **arrivalRate** in **phases** describes that the load phase will last for 60 seconds with 4 new virtual users (arriving every second on average). Multiple phases can be defined.
- **x-my-service-auth** describes the header to be sent with every http request.
- The **scenarios** section describes what the virtual users created by Artillery will be doing.
- **flow** is an array of operations that a virtual user performs, e.g. GET and POST requests for an HTTP-based application.
- Here the virtual users will visit the "docs" and then the "introduction" page of www.abc.com.

### Running the test

Run the test with:
```sh
$ artillery run hello.yml
```
As Artillery runs the test, the end report generated after test will look like this:
```scala
All virtual users finished
Summary report @ 08:58:25(+0000) 2018-07-09
  Scenarios launched:  240
  Scenarios completed: 240
  Requests completed:  480
  RPS sent: 4.16
  Request latency:
    min: 321.2
    max: 46175.7
    median: 23092.8
    p95: 38340
    p99: 45341.4
  Scenario counts:
    0: 240 (100%)
  Codes:
    200: 456
    500: 24
```
**Scenarios launched** are the number of virtual users created
**Scenarios completed** are the number of virtual users wo have completed their scenarios
**Requests completed** is the number of HTTP requests sent
**RPS sent** is the number of HTTP requests completed per second
**Request latency** and **Scenario duration** are in milliseconds, and p95 and p99 values are the 95th and 99th percentile values (for eg. if p99 is 500 then 99 out of 100 requests took 500ms or less to complete).
**Codes** is the count of HTTP response codes.
If you see **NaN ("not a number")** reported as a value, that means not enough responses have been received to calculate the percentile. 
If there are any errors (such as socket timeouts), those will be printed under **Errors** in the report as well.

That's All for Now.
Happy Load Testing!





