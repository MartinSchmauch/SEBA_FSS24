# TUMatch - a hyperlocal matching platform

Welcome to our webapplication that we created in the SEBA course at TUM.
The application provides a platform where student co-founder and other students can match up to form a startup.

The application is based on the MERN stack and uses bootstrap react components for styling.
For payment services we use Stripe as payment provider. For make the payment provider work in a local environment, you need to create a local strip webhook. More about that under "Stripe Setup".


## Running the application in Docker
If you want to test the payment functionality as well, conduct the stripe setup, before containerization of the project.
### 1. Containerize project
Navigate to root of repository and execute ```docker compose build```
### 2. Run containerized project
After successfull containerization, start the application using: ```docker compose up```
You can now locally access the frontend of the webapplication under: [http://localhost:3000](http://localhost:3000)
(Database access is already provided by the mongoDbUrl attribute in the [config.js](/backend/config.js) that contains login information)

## Running the application locally
### 1 Install packages
Run  ```npm install ``` in the frontend and the backend directory, as both of them represent standalone react projects.

### 2 Start application
Run ```npm start``` in the frontend and the backend directory to start the backend server and the frontend service.
You can now locally access the frontend of the webapplication under: [http://localhost:3000](http://localhost:3000)


## Stripe Setup
We implemented the stripe functionality with local stripe webhooks. For each local machine, that runs the application, you need an own local stripe webhook. Below there is the instruction on how to create such a webhook.

### 1. Install the Stripe CLI
```console
brew install stripe/stripe-cli/stripe
```

### 2. Log in to your Stripe account
```console
stripe login
```
After running stripe login, press enter for a authentification link to open in your browser that redirects you to a strip login.
Enter the stripe credentials and approve the login request after successfull login:
user: leonurny@outlook.de
password: secret!!

### 3. Set up webhook forwarding to your local server
Go back to your console and create the webhook using the following command:
```console
stripe listen --forward-to localhost:8080/payment/webhook
```
You will receive a stripe webhook secret in the console output. Use this secret in the next step.

### 4. Add Webhook Secret to config.js
Store the stripe webhook secret under the key: "stripe_endpoint_secret" in the [config.js](/backend/config.js) file


## Test user
If you quickly want to check some features, you can use our example student and example investor. The investor already has a valid subscription via stripe, so if you don´t want to set up stripe, just use the example investor user.

### 1. Example investor: 
email: thomas.lutz@picus.com
password: 123456789

### 2. Example student
email: finn.fischer@tum.de
password: 12345678
