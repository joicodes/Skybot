# SkyBot

Contributors: @joicodes, @lesley2958, @MJDev, @KlarizsaPadilla

## About SkyBot

SkyBot is an SMS chat bot that allows traveling Columbia students to share rides to the airport, matching them with other students going to the same airport at the same time. Currently, Columbia students have a designated Facebook Group called Columbia / Barnard Airport Cab Sharing, where they post their travel itineraries in hopes of connecting  with someone who has a similar flight departure time, in an effort to split a cab fare to save money. In New York City, cab fare to airports can be as high as $100 depending on the number of riders, transportation peak hours, and weather inclemation. SkyBot is a cost effective solution that addresses these pain points.

Using our matching algorithm, SkyBot accurately matches students with the closest travel itineraries and shared preferences! With API integrations, including Twilio, SendGrid, and Lyft students can easily:

- Access their travel itineraries
- Estimate transportation cost
- Split transportation cost
- Connects matches via LionMail
- Share calendar invites and reminders

SkyBot aims to provide a simple user interface to connect people in order to make the process of getting to your desired destination less of a hassle.

## Structure

```bash
├── .gitignore                    # Ignore unneeded Python files
├── .pylintrc                     # Python lint configuration
├── .travis.yml                   # CI Configuration
├── .pre-commit-config.yaml       # Precommit File
├── .coveragerc                   # Coverage Information
├── CONTRIBUTING.md               # Guide to adding to SkyBot
├── Procfile                      # Used when deploying the bot to production
├── README.md                     # This file
├── app.py                        # The main bot code
├── config.py                     # Database Configurations
├── database.py                   # Contains database schemas
├── manage.py                     # Database Managemenet
├── match.py                      # Contains matching algorithm
├── requirements.txt              # Libraries used to build the bot
├── runtime.txt                   # Python configuration for Heroku
├── nose.cfg             		  # TO DO
├── test/                         # All supporting code used by app.py
    ├── test_app.py               # TO DO
    ├── test_databases.py         # TO DO
├── coverage_docs/				  # TO DO
├── migrations/		     		  # TO DO
├── submissions/				  # TO DO
```

## Technology Stack

- Development Framework: Python (Flask)
- Unit Testing Tool: PyUnit
- Static Analysis Tool: PyLint
- Build Tool: Travis CI
- Continuous Integration Tool: Travis CI
- Data Storage: PostgreSQL
- VersionControl: Github
- Cloud Platform: Heroku
- APIs: Twilio, SendGrid, Lyft Fare Estimator


## Connecting to Twilio

We used Twilio’s Programmable SMS to set this up as an SMS service. Specifically, we wrote a function that will communicate with the Twilio API to provide a response, `sms_reply()`. For this function we use the `route()` decorator to tell Flask which URL should trigger this function.

``` python
@app.route("/sms", methods=['GET', 'POST'])
def sms_reply():
```


This function is triggered whenever a message is sent to our Twilio number. With `requests.values.get`, we retrieve several attributes associated with the message received from a user, including their phone number. To indicate this, we made the first parameter `From`; this yields a result in the format “+1XXXXXXXXXX.”

``` python
@app.route("/sms", methods=['GET', 'POST'])
def sms_reply():
    body = request.values.get('From', None)
```
