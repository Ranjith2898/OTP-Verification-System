# Code : 

import smtplib
import random
import time
import re
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

# Function to generate a 6-digit OTP
def generate_otp():
  return str(random.randint(100000, 999999))



# Function to send the OTP to the user's email
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


# Run the OTP Verification Process
otp_verification()

# Output

Enter your email address: gunnalaranjithkumar31@gmail.com 
OTP sent successfully to email.
Enter the OTP sent to your email: 43549787
Error: Invalid OTP format. Please enter a 6-digit OTP.
Enter the OTP sent to your email: 874387
Error: Incorrect OTP. You have 2 retries left.
Enter the OTP sent to your email: 4767y87
Error: Invalid OTP format. Please enter a 6-digit OTP.
Enter the OTP sent to your email: 656464767
Error: Invalid OTP format. Please enter a 6-digit OTP.
Enter the OTP sent to your email: 667865
Error: Incorrect OTP. You have 1 retries left.
Enter the OTP sent to your email: 788667
Error: Verification failed. Access denied!

or 

Enter your email address: gunnalaranjithkumar31@gmail.com 
OTP sent successfully to email.
Enter the OTP sent to your email: 875763
Success: OTP verified successfully! Access granted.
