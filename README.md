# OTP Verification System

## 📌 Project Overview

The OTP Verification System is a Python-based authentication mechanism that generates a 6-digit OTP (One-Time Password) and sends it to a user's email for verification. The user must enter the received OTP to gain access, ensuring a secure login process.

## 🔥 Problem Statement

The goal is to develop an OTP verification system in Python that:

* Generates a random 6-digit OTP.
* Sends the OTP to the user's email.
* Validates the user-entered OTP.
* Provides retries in case of incorrect input.

## 🚀 Features

✔ Random OTP Generation

✔ Email-based OTP Delivery

✔ OTP Validation & Retry Option

✔ 5-Minute OTP Expiry

✔ Secure Error Handling

✔ User-Friendly Interaction

## 🛠️ Project Breakdown

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

💻 Python Implementation

## 📌 Key Libraries Used:

import smtplib

import random

import time

import re

from email.mime.text import MIMEText

from email.mime.multipart import MIMEMultipart

✅ OTP Generation Function

def generate_otp():

    return str(random.randint(100000, 999999))

## 📧 Function to Send OTP via Email

def send_email(recipient_email, otp):

    try:
        # Email Configurations
        sender_email = "monakumari08@gmail.com"
        sender_password = "niueguwoshoruejc"  # It's recommended to use an app password or environment variables

        # Setting up the email message
        subject = "Your OTP Verification Code"
        body = f"Your One-Time-Password (OTP) is: {otp}\nThis OTP is valid for 5 minutes."
        message = MIMEMultipart()
        message['From'] = sender_email
        message['To'] = recipient_email
        message['Subject'] = subject
        message.attach(MIMEText(body, 'plain'))

        # Sending email using SMTP server
        with smtplib.SMTP('smtp.gmail.com', 587) as server:
            server.starttls()  # Enable encryption
            server.login(sender_email, sender_password)
            server.send_message(message)
        print("OTP sent successfully to email.")

    except smtplib.SMTPAuthenticationError:
        print("Error: Authentication failed. Check your email or app password.")
        exit(1)
    except Exception as e:
        print(f"Error: Failed to send email: {e}")
        exit(1)
    #Function to validation OTP input and enforce exactly 6 digits
    def validate_otp_input(new_value):

      # Allow only digits and restrict to a maximum of 6 characters
      return new_value.isdigit() and len(new_value) <=6

    # Function to validate Email
    def is_valid_email(email):

      email_regex = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
      return re.match(email_regex, email) is not None

## 🔄 OTP Validation and Verification


    # Function to Verify OTP with retries and timeout
def otp_verification():

    while True:
        # Request the user's email address
        recipient_email = input("Enter your email address: ").strip()

        # Validate if email is provided
        if not recipient_email:
            print("Error: Email address cannot be empty.")
            continue

        # Check if the email format is valid
        if not is_valid_email(recipient_email):
            print("Warning: Invalid email format. Please enter a valid email address.")
            continue

        # Once valid, break the loop and proceed
        break

    # Generate and send OTP
    otp = generate_otp()
    send_email(recipient_email, otp)

    # Record the time the OTP was generated
    otp_time = time.time()
    retries = 3  # Number of retries allowed

    # OTP verification loop
    while retries > 0:
        # Ask the user to enter the OTP
        entered_otp = input("Enter the OTP sent to your email: ").strip()

        # Validate OTP input (should be 6 digits)
        if not validate_otp_input(entered_otp):
            print("Error: Invalid OTP format. Please enter a 6-digit OTP.")
            continue

        # Check if OTP is expired (5 minutes timeout)
        if time.time() - otp_time > 300:  # 5 minutes timeout
            print("Error: OTP has expired. Please request a new OTP.")
            return

        # Verify OTP entered by the user
        if entered_otp == otp:
            print("Success: OTP verified successfully! Access granted.")
            return
        else:
            retries -= 1
            if retries > 0:
                print(f"Error: Incorrect OTP. You have {retries} retries left.")
            else:
                print("Error: Verification failed. Access denied!")
                return

## 🔄 Running the OTP Verification

     otp_verification()

## 🎯 Expected Outputs

✅ Correct OTP Entry

Enter your email address: gunnalaranjithkumar31@gmail.com

OTP sent successfully.

Enter the OTP sent to your email: 123456

Success! OTP verified.

❌ Incorrect OTP Entry

Enter your email address: gunnalaranjithkumar31@gmail.com

OTP sent successfully.

Enter the OTP sent to your email: 654321

Incorrect OTP. 2 retries left.

Enter the OTP sent to your email: 543210

Incorrect OTP. 1 retry left.

Enter the OTP sent to your email: 111111

Verification failed. Access denied!


## 🔐 Security Considerations

* Use App Passwords instead of storing raw email passwords.
* Ensure OTP expiry (5 minutes) to prevent replay attacks.
* Limit OTP retries to prevent brute force attempts.

## 📢 Summary

🔹 This project implements a secure OTP-based authentication system.

🔹 It covers OTP generation, email verification, input validation, and security handling.

🔹 This concept is widely used in banking, e-commerce, and login verification systems.




  
