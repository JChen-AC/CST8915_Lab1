# CST8915 Lab 1: Algonquin Pet Store on Azure VM

**Student Name**: Joshua Chen
**Student ID**: 041280453
**Course**: CST8915 Full-stack Cloud-native Development
**Semester**: Winter 2026

---

## Demo Video

https://youtu.be/krtPtf2v81M

---

## Technical Explanations

### Order Service (Node.js)

The order service was created using Node.js and its purpose is to process and receive orders from the Store Front service and then send the information to a queue on RabbitMQ. Its role in the architecture is to decouple the logic regarding processing the request, allowing it to be more scalable and helps maintainable architecture. Additionally, it can be deployed independently from the other services, as can be seen through the test with Rest Client, which should show it works. It communicates with the Store Front service by using http request, where it would listen for a request on the route /order and the process the request. It processes the request by getting the information from the request and converting it into a json array before opening a connection with the Rabbit MQ service using AMPQ, and creates a channel and adding the json object to the queue.  

### Product Service (Rust)

The product service is responsible for providing the order options and the corresponding information when requested by the store front. It is written in Rust and uses the Warp Web Framework to help facilitate communications with the store front. It only interacts with the Store Front service and uses http request to communicate. It listens to the “/product” route and waits for an HTTP GET request to trigger and responds with the information is a json array. The role of the product service is to store the products offered by the store, decoupling the store front from more data. The reason that this fits into the microservice architecture is that its sole purpose is to store and return the orders. And it can be independently deployed, as can be seen with the test where using the Rest Client, which should show it working. 

### Store Front (Vue.js)

The Store Front is the front end of the service and is where the user can see what the store offers and how the users place orders. It is written in Vue js and node js, with it communicating with the other services through http request. It fits into the architecture role of being the front-end and user interaction. With the interaction displaying the information and getting the order form.  Additionally, it can be independently deployable, showing you the three animals, the background image, and the layout of the website. 

### Rabbit MQ (RabbitMQ)

The RabbitMQ service is responsible for receiving and holding orders from the order service. It uses the RabbitMQ Framework, which is a queuing service. Its purpose is to facilitate communication between the different services, where it would receive orders from the order service and hold the information until another service can pop the queue to process the order. Its architecture role is to allow communication between the order service and whatever back-end service would process the orders by receiving the orders and processing them. The inter-Service communication method is an AMQP connection, which it uses to connect to the RabbitMQ server and create a channel to it, and send information to the queue. The architecture role of it is the event bus, as it handles the communication between the different services (specifically the order service and whatever it should connect to). Additionally, RabbitMQ is solely responsible for the queue and can be deployed independently from the other services.

---