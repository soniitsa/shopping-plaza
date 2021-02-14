User Experience (UX)

Project Goals
The goal of this project is to create an online bussiness store where people around the world can easily purchase clothing with ease.

User Stories
First Time Visitor Goals
1 As a first time visitor, I want to understand the main purpose of the site
2 As a first time visitor, I want to be able to easily navigate through the site
3 As a first time visitor, I want to be able to search for products specifically

Registered User Goals
1 As a registered user, I want to be able to easily login and logout of my account
2 As a registered user, I want to be able to see my order informations.

Site Owner Goals
As a site owner, I want to provide the user with information about the purpose of the site
As a site owner, I want to include a navigation bar to allow users to easily navigate to other pages on the site
As a site owner, I want all visitors and registered users to be able to easily contact me through email or social media platforms

Design
The overall design of this project is based on the boutique_ado site. 
The site features a simple and easy to follow layout with a navigation bar at the top,
the main content in the middle and a footer containing external links at the bottom.

Imagery

 These images are from various different fashion website sites. 
 fashionova.com

Technologies Used
Languages
HTML
CSS
JavaScript
Python
Django

Testing 
Contents
Code Validation
User Stories
Branches
Responsiveness
Performance
Manual Testing
Known Bugs

Heroku
This project is hosted on Heroku - A cloud platform service that enables developers to build, 
run and operate applications entirely in the cloud:

Before creating a Heroku app, open the repository,
in VS Code and create a requirements file that lists all the applications
and dependencies required to run the application: pip3 freeze --local > requirements.txt
Create a Heroku specific file called a Procfile - 
this is what Heroku looks for to know which file runs the app and how to run it: echo web: python run.py > Procfile
Open Heroku and login to your account or sign up for an account if you don't already have one
Open the dashboard and select "New" to create a new app
Name the app and set the region to Europe
Open the settings tab and open "Reveal Config Vars"
Add the environment variables from the env.py file:

To deploy the app from GitHub, open the deploy tab and change the deployment method to GitHub
Connect to your GitHub account and search for the name of the repository to connect to
Once connected, "Enable Automatic Deployments" and select the "Master" or "Main" branch to deploy
Click the "Deploy Branch" button to deploy the app to Heroku

Acknowledgements

A huge thank you to the Tutor Support for helping me spot an error in my code 
that wouldn't let me render the edit word functionality - 
It's always the silly things that catch me out!