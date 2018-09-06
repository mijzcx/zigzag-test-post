# ZigZag Test POS

Front end Developer

Introduction
The purpose of this test is for you to demonstrate your strengths.

Task

Develop a front end web application that mimics a Point of Sale. For example https://squareup.com/au/pos
The POS builds up an order basket (one coke and a burger for example) with a total amount and sends that amount to a dummy web service.
Use http://demos.kaazing.com/echo/ as a simple web socket echo server.
The request that is sent and echoed back to you is:

{ "event": "purchase", "amount": 2334 }

Where the amount is dynamically calculated in your POS.
When you receive an echo back, confirm to the user that the payment has been processed. Clear your basket and provide a virtual receipt.

Use any JS framework that you're comfortable with for this. Style the POS as you wish. Make sure it works using whatever means you feel
appropriate.

Expected Output

Working code provided on Github or similar.
Code hosted or instructions to build and run locally provided.

> Instructions to run
```
# make sure you have vue-cli globally installed
$ yarn global add vue-cli
# or:
$ npm install -g vue-cli

# Node.js >= 8.9.0 is required.
$ yarn global add quasar-cli
# or:
$ npm install -g quasar-cli
```

* go to its base folder then, type

```
$> npm install
$> quasar dev

see localhost:8080
```
