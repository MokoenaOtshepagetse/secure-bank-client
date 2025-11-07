# Secure Bank Web Application

## 1. Web Application Information

This project is a secure banking web application built with the MERN stack (MongoDB, Express.js, React, and Node.js). It demonstrates a variety of industry-standard security practices to protect user data and ensure secure transactions.

### Key Features:
*   **Secure User Login:** Authenticates users against a database of hashed and salted passwords.
*   **User Dashboard:** Displays transaction information for the logged-in user.
*   **Simulated International Payments:** Allows users to perform mock international payment transactions.

## 2. Security Features Implemented

The core of this project is its security. Here are the key protection techniques we've implemented in the backend:

*   **bcrypt Password Hashing and Salting:** We use the bcrypt library to securely hash and salt user passwords before storing them in our MongoDB database. This means that even if our database were compromised, the passwords would be computationally difficult to crack.
*   **Secure Login Validation:** The login route securely compares the user's provided password with the stored hash to authenticate them.
*   **RegEx Input Whitelisting:** We use regular expressions as middleware to ensure that user input matches expected formats and does not contain malicious characters.
*   **NoSQL Injection Prevention:** By using Mongoose, our application is inherently protected against many NoSQL injection attacks, ensuring user input is treated as data, not code.
*   **HTTPS for Encrypted Communication:** The backend is configured to run on HTTPS using a self-signed certificate. This encrypts all data in transit between the frontend and the backend, protecting it from eavesdropping.
*   **Rate Limiting:** To protect against brute-force login attacks, we have implemented rate-limiting middleware. This will temporarily block an IP address after too many failed login attempts.
*   **CSRF and XSS Protection:** We have added middleware (like Helmet.js) to help protect against common vulnerabilities like Cross-Site Request Forgery (CSRF) and Cross-Site Scripting (XSS).

## 3. How to Test the Web Application (Frontend)

To test this application, please follow the setup instructions below. No programming knowledge is required.

### Step 1: Install the Required Tools

Make sure your computer has the following installed:

1.  **Node.js & npm:**
    *   Go to [https://nodejs.org](https://nodejs.org)
    *   Download the **LTS (Long-Term Support)** version.
    *   Install it by accepting all default options.
2.  **Git:**
    *   Download and install from [https://git-scm.com/downloads](https://git-scm.com/downloads)

### Step 2: Clone the Repositories

1.  Open a terminal (Command Prompt on Windows, or Terminal on Mac).
2.  Clone the backend code by running:
    `git clone https://github.com/jmatt-iiemsa/secure-bank-api.git`
3.  Clone the frontend code by running:
    `git clone https://github.com/jmatt-iiemsa/secure-bank-client.git`

### Step 3: Setup the Backend

1.  In your terminal, navigate to the backend folder:
    `cd secure-bank-api`
2.  Install all required packages by running:
    `npm install`
3.  **Create the `.env` file** in this folder. This file contains the database connection string and other secrets. It must be configured correctly for the application to work.

4.  **Populate the Database with Sample Users**. Run the following commands one by one from the `secure-bank-api` folder. These scripts will create the initial user and admin accounts needed for testing.

    *   To create the employee/admin account, run:
        ```bash
        node --experimental-modules seed/createEmployee.js
        ```
        *(Note: If the above command doesn't work, you may be able to run it without the flag: `node seed/createEmployee.js`)*

    *   To create the customer/user account, run:
        ```bash
        node --experimental-modules seed/createCustomer.js
        ```
         *(Note: If the above command doesn't work, you may be able to run it without the flag: `node seed/createCustomer.js`)*

5.  **Run the backend server** with the command:
    `npm run dev`
    *   You should see a message like: `Secure HTTPS server running at https://localhost:5000`
    *   **Leave this terminal window running in the background.**

### Step 4: Setup the Frontend

1.  Open a **new, separate** terminal window.
2.  Navigate to the frontend folder:
    `cd secure-bank-client`
3.  Install all required packages by running:
    `npm install`
4.  Start the frontend application with:
    `npm start`
    *   This should automatically open the web application in your browser at `http://localhost:3000`.

### Step 5: Test the Application

The application is now running. You can test its features using the credentials created by the seed scripts.

**User Credentials to Use:**
*   **Email:** `user@example.com`
*   **Password:** `SecurePassword123`

**Admin Credentials to Use:**
*   **Email:** `admin@example.com`
*   **Password:** `SecureAdminPass123`

#### Testing Scenarios:
1.  **Successful Login:** Use the correct user credentials to log in. You should be taken to the user dashboard.
2.  **Failed Login:** Try to log in with an incorrect password. You should see an error message.
3.  **Make a Payment:** Once logged in, navigate to the payments page and simulate a transaction.
4.  **Input Validation:** Try entering invalid data (e.g., an email without an "@" symbol) to see the error messages.

## 4. DevOps and Code Quality

*   **CircleCI:** We have an automated build and test pipeline configured in CircleCI. This ensures that every new code change is automatically tested for errors.
*   **SonarQube:** We use SonarQube to perform static code analysis. This helps us identify and fix security vulnerabilities, code smells, and bugs early in the development process.
