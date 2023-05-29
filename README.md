# PixelPulse - An email tracker

<a name="readme-top"></a>
# 📗 Table of Contents

- [📖 About the Project](#about-project)
- [👥 Authors](#authors)
- [⭐️ Show your support](#support)
- [⚙️ Setup and Usage](#setup--usage)
- [🌍 How to use Geo location API](#how-to-use-a-geo-location-api)
- [📝 License and copyrights](#license--copyrights)
- [⚠️ Disclaimer](#disclaimer)

## About the Project <a name="about-project"></a>
### 1. Abstract:
The goal of this project is to develop an email tracking and resend system that detects
whether the recipient has read a sent email and takes appropriate actions based on
their response. The system addresses the common issue of unanswered emails by
automatically resending the email if it remains unseen, or if a reply has not been
received within a week.
### 2. Problem Statement:
The current email communication process lacks a reliable mechanism to
determine whether recipients have read sent emails, leading to uncertainties and delays
in receiving responses. This poses a challenge for individuals and organizations who
depend on timely communication for efficient workflow and effective collaboration.
Furthermore, there is no automated system in place to resend emails that have not
been seen or to prompt responses in case of prolonged silence.
### 3. Proposed Solution:
This project is in line with the Rethink theme.

**Email Tracking**: The system will utilize tracking technologies to monitor whether
recipients have read sent emails. It will provide real-time notifications to senders,
indicating when an email has been opened and read.
Resend Automation: If an email remains unseen after a specified period or if a reply has
not been received within a week, the system will automatically initiate a resend action.
This proactive approach ensures that important emails are not missed or overlooked by
recipients.

**Clear Status Notifications**: The system will provide clear and informative status
notifications to senders, indicating the current read status and the actions taken for each
email. This transparency empowers users with a comprehensive overview of their email
communications.

## 👥 Authors <a name="authors"></a>

👤 **Indira Kumar A K**

- GitHub: [@Indira-kumar](https://github.com/Indira-kumar)
- Twitter: [@theluckiestman](https://twitter.com/theluckiestman)
- LinkedIn: [Indira Kumar A K](https://www.linkedin.com/in/indira-kumar-a-k-b612381bb/)

👤 **Gayathri Sthanusubramonian**

- GitHub: [@Gayathri2522](https://github.com/Gayathri2522)
- LinkedIn: [Gayathri Sthanusubramonian](https://www.linkedin.com/in/gayathri-sthanusubramonian-9aa882213/)
- Twitter: [@Gayathri2522](https://twitter.com/Gayathri2522)

👤 **Keshav Rathinavel**

- GitHub: [@keshavrathinavel](https://github.com/keshavrathinavel)
- Twitter: [@keshah08](https://twitter.com/keshaha08)
- LinkedIn: [Keshav Rathinavel](https://www.linkedin.com/in/keshavrathinavel/)

👤 **Anshuman Sahoo**

- GitHub: [@Cyberc0re-code](https://github.com/Cyberc0re-code)
- Twitter: [@Anshuman_2003](https://twitter.com/Anshuman_2003)
- LinkedIn: [Anshuman Sahoo](https://www.linkedin.com/in/anshuman-sahoo-832342206/)

## 🤝 Contributing <a name="contributing"></a>

Contributions, issues, and feature requests are welcome!
Feel free to check the [issues page]().

<!-- SUPPORT -->

## ⭐️ Show your support <a name="support"></a>

Give a ⭐️ if you like this project!


## Setup & Usage

### Basic Requirements

- Python3 and Pip
- Git

  - [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
  - [Setup Git](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)

- Heroku Account & Heroku CLI (or suitable platform)  
  If you're willing to use **Heroku**, [here](https://devcenter.heroku.com/articles/getting-started-with-python) they have explained all the steps for getting started with python apps.

- Code Editor (such as [VS Code](https://code.visualstudio.com/))

### Installation

1. First clone or download this repository as a Zip file to your local machine.

2. Navigate to the directory.

   ```bash
   cd pixelpulse
   ```

3. Create a virtual environment.

   ```python
   python3 -m venv venv
   ```

4. Activate virtual environment.

   _Linux:_

   ```bash
    source venv/bin/activate
   ```

   _Windows:_

   ```bash
   venv\Scripts\activate
   ```

5. Install dependencies.

   ```bash
   pip install -r requirements.txt
   ```

6. Change the time zone used in `routes.py`:
   (Default value is `Asia/Colombo`)

   ```python
   # Line 38
   TIMEZONE = "Your-Timezone"
   ```

   To choose the correct time zone, you can query all the supported time zones like this; open a separate python shell and run the following code.

   ```python
   import pytz
   pytz.all_timezones
   ```

7. As we use Firebase Realtime Database and Firebase Authentication, you have to create a Firebase project and obtain the credentials. Visit [Firebase Console](https://console.firebase.google.com/) and create a new project.  
   Then go to the project settings and click on the `Service Accounts` tab. Then click on the `Generate New Private Key` button. This will download a JSON file containing the credentials. Rename the file to `credentials.json` and place it in the root directory of the project.

8. Now you have to create a new Firebase Authentication user. To do that, you have to go to the `Authentication` tab in the Firebase Console. Then click on the `Set up sign-in method` button. Then click on the `Email/Password` tab and enable it. Then click on the `Users` tab and click on the `Add User` button. Enter the email and password of the user account you want to create. Then click on the `Add User` button.

9. Now you have to create a new Firebase Realtime Database. To do that, you have to go to the `Database` tab in the Firebase Console. Then click on the `Create Database` button. Then select the database location and click on the `Next` button. Then change the rules as follows and click on the `Enable` button:

   ```json
   {
     "rules": {
       "MailTrackData": {
         "Users": {
           "$uid": {
             ".read": "auth !== null && auth.uid === $uid",
             ".write": "auth !== null && auth.uid === $uid"
           }
         },

         "LinkHits": {
           ".read": false,
           ".write": true
         }
       }
     }
   }
   ```

10. Now go to project settings again and under the **General** tab you can find the `Web API Key`. And also,you are able to find the `Database URL` under the **SDK setup and configuration** tab there.  
    (Ex: `databaseURL: "https://your-app-default-rtdb.asia-southeast1.firebasedatabase.app"`)  
    Take a note of both of them since we will need them on the next step.

After that you can either test the application in your local machine or setup your selected platform, as you wish.

### Testing/Using on your Local Machine | Network

Before running the application, you have to set the following environment variables: (Just replace the values with your own and run the commands inside the activated virtual environment - No commas on Windows)

_Linux & macOS:_

```bash
 export FLASK_ENV="development"
 export FIREBASE_API_KEY="Your-Firebase-API-Key"
 export FIREBASE_DB_URL="Your-Firebase-Database-URL"
 export SECRET_KEY="replace-this-text-with-a-suitable-key"
```

_Windows:_

```bash
 set FLASK_ENV=development
 set FIREBASE_API_KEY=Your-Firebase-API-Key
 set FIREBASE_DB_URL=Your-Firebase-Database-URL
 set SECRET_KEY=replace-this-text-with-a-suitable-key
```

Then run the application using the following command:

```bash
flask run
```

Navigate to `localhost:5000` in your browser.  
If another program is already utilizing port 5000, `Address already in use` error will be displayed.
If that happens you can specify a different port like this:

```bash
flask run --port 5001
```

A login page will be displayed.  
Input your newly created account's email & password and that's it!


## Steps to create a tracking link for your email.

1. Visit the homepage of the app and sign into your account.

| Login Screen
| :-:

2. First add a suitable title for your message. You can add the subject of the specific email which will make it easier to identified at later times.

| Create Entry
| :-:

3. Then click '**Generate**'

4. Then, you can drag & drop the tracking image to the end of your message body. (**DO NOT copy & paste the image** since it will insert your image as a base64 image to the email body)
   Otherwise, you can manipulate the content of the email body using Developer Tools in browser.

5. Everything's done! Now send your email and wait for the results to appear. (you need to refresh your browser to load new entries)

## How to use a Geo Location API

Using a Geo Location API, you can collect additional information about the recipient such as;

- Approximate location
- Country
- ISP ( Internet Service Provider)
- VPN/Tor Usage ...

In `routes.py` line 70 to 75 contains a simple API usage that can be altered according to your opinions. Please note that **ipwhois** service has certain limitations (like amount of requests) which may eventually cause errors. So, you can choose a better API which fit into your needs.

### Special note about G-Mail

Since Google uses a special technique, "Image Proxies" to deliver images; this pixel based tracking method is not suitable to gather additional information about the recipients who use G-Mail. Instead of recipient's IP address and User-Agent, you will receive Google Image Proxy’s UA (User-Agent) and IP address which looks like this:

`Mozilla/5.0 (Windows NT 5.1; rv:11.0) Gecko Firefox/11.0 (via ggpht.com GoogleImageProxy)`

But, on the bright side, you can still get the resource accessed date and time!

### Why not using cookies for tracking?

Yes, you can set cookies for additional/accurate data collection. But they represent as third party cookies within devices. Most of the web browsers/platforms block such cookies by default. [maybe not Chrome yet 😉] So, it's the death of 3<sup>rd</sup> party cookies.  
**Update:** Since some browsers/platforms allow 3<sup>rd</sup> party cookies, we are going to implement a cookie based tracking method in the future.


## License & Copyrights

**The MIT License**

This program is free software: you can redistribute it and/or modify it under the terms of the **MIT License**

Refer to the [LICENSE](LICENSE) file for more details.

**Heroku, GMail, ipwhois, VS Code, Chrome** are copyrights and/or trademarks of their respective owners.

## Disclaimer

Tracking other users actions across any platform may considered as violation of their privacy. So, kindly use this in a responsible manner.
