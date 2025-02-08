# OTP Verification System

📌 Project Overview

The OTP Verification System is a Python-based authentication mechanism that generates a 6-digit OTP (One-Time Password) and sends it to a user's email for verification. The user must enter the received OTP to gain access, ensuring a secure login process.

🔥 Problem Statement

The goal is to develop an OTP verification system in Python that:

* Generates a random 6-digit OTP.
* Sends the OTP to the user's email.
* Validates the user-entered OTP.
* Provides retries in case of incorrect input.

🚀 Features

✔ Random OTP Generation

✔ Email-based OTP Delivery

✔ OTP Validation & Retry Option

✔ 5-Minute OTP Expiry

✔ Secure Error Handling

✔ User-Friendly Interaction

🛠️ Project Breakdown

1️⃣ Generate OTP

* Uses Python's random.randint() function to create a 6-digit numeric OTP.

2️⃣ Send OTP to Email

* Uses SMTP (Simple Mail Transfer Protocol) to send an email with the OTP.

* Gmail SMTP Server (smtp.gmail.com) is used for secure email transmission.

3️⃣ User Input

* Prompts the user to enter their email.

* Validates the email format using Regular Expressions (Regex).

4️⃣ Verify OTP

* Compares the user-entered OTP with the generated OTP.

* Allows up to 3 retry attempts before denying access.

* Ensures OTP expires after 5 minutes.

5️⃣ Error Handling

* Checks for invalid email formats.

* Ensures OTP input is exactly 6 digits.

* Handles SMTP authentication errors securely.


  
