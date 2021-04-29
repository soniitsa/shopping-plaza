# Project Goal
The goal of this project is to create an online bussiness store called Shopping Plaza, 
where people around the world can easily purchase clothing with ease. 

## User Stories
As A	I want to be able to...
Site User	Quickly and easily understand the purpose of the site
Site User	View a list of products & services available
Site User	View individual products & services
Site User	Sort for products & services that fit my requirements
Site User	Select products & services I want and add them to my basket
Site User	Easily view the total cost of my purchases at any time
Site User	Add additional information to inform designer on project requirements
Site User	Easily locate an inbuilt contact form to request quotes on unique projects
Site User	Pay for services via an inbuilt payment service
Site User	Sign in as a customer to view order history and upload commission images
Site Owner	Log in as a special user and view a list of all orders and uploaded images
Site Owner	Handle the customer request and upload of images all through the site
Site Owner	Showcase a portfolio of work which can be changed or removed through the site
Site Owner	Showcase testimonials from previous customers which can be added to or removed through the site
Site Owner	Display an about the designer section to humanise the work and encourage users to commit
Site Owner	Add, edit, view and delete items in the shop all through the site

### Registered User Goals
 As a registered user, I want to be able to easily login and logout of my account
 As a registered user, I want to be able to see my order informations.

#### Design
The overall design of this project is based on the boutique_ado site. 
The site features a simple and easy to follow layout with a navigation bar at the top,
the main content in the middle and a footer containing external links at the bottom.

###### Imagery

These images are from various different fashion website sites. 
fashionova.com

###### Technologies Used
Languages
HTML
CSS
JavaScript
Python
Django

# Code
codes where taken from the torturial video

# Testing 
Contents
Code Validation
User Stories
Branches
Responsiveness
Performance
Manual Testing
Known Bugs

### Testing
Bug Fixes
Adjust Quantity Buttons - During development of the bag app, 
an issue arose in which the plus and minus buttons to adjust quantity of an item in the bag didn't function properly.
The script was implemented on the product_detail page, wherein it worked perfectly fine, 
but the same could not be said for the bag page. As this was copied from the product_detail page, 
which in turn was near verbatim from the Boutique Ado walkthrough project, 
the code was studied and compared to that in the walkthrough.
The fix came when the copied code from the product_detail page was deleted entirely,
then rewritten manually from scratch. Though it was identical, to how it had been before, the code now worked.
 
Checkout Webhook - During the creation of webhooks to ensure the Stripe payments would work as intended, 
a 500 error was being raised when a payment was submitted. 
Both the payment_intent.created and charge.succeeded went go through as intended, 
but the payment_intent.succeeded did not without manually resubmitting it in the Stripe dashboard.
The terminal raised a ValueError saying the view checkout.webhooks.webhook didn’t return a HttpResponse object, 
and returned None instead. The issue came from the webhooks_handler.py file,
which was missing a return at the end of the handle_payment_intent_succeeded function's else statement. 
Once this was included, the error was resolved.

Duplicate Street_address1 - During tests of the payment system, an error appeared to show that 
the street_address2 input was being overridden by a second street_address1.
On closer inspection, this turned out to be a simple error on the checkout_success.html page wherein the 
street_address1 tag had been repeated and not changed to street_address2.

Unresponsible CSS/JS files - During production, an error arose in which any CSS or JS files outside 
the base files were not working as intended. Research underway to see if this was an issue with Bootstrap or Django, 
but in the end the answer was much simpler. In the base.html file, the extra_css and extra_js blocks had
been written as extracss and extrajs, meaning they weren't picking up new block files. 
This fix in turn solved all outstanding CSS and JS issues.

SECRET_KEY - Once the project had been deployed to Heroku and the Static and Media files were stored on AWS, 
two issues arose the next time the project was opened on Gitpod. 
The first was this warning: django.core.exceptions.ImproperlyConfigured: The SECRET_KEY setting must not be empty. 
This came as a surprise as there had been no issues with the SECRET_KEY thus far, 
and the deployed Heroku version worked fine. To fix this, a env.py file was created to store the SECRET_KEY, 
and - surprisingly - the following was added to the settings.py 
file: SECRET_KEY = os.environ.get('SECRET_KEY', 'some value if your key is not in the environment') 
The error no longer appeared, and since it appears to be a Gitpod-side problem, 
there should be no forseeable issues in the future of the project.
Media and Static Files Not Loading The second of the two post-deployment issues, 
when the Gitpod server was run all the media and static files no longer loaded after the Heroku deployment. 
At first, this was thought to be an issue with the DISABLE_COLLECTSTATIC, but this was not the case. 
Instead, it appeared to be a fault with the site attempting to load local files instead of the hosted AWS files. 
This was not the case on the Heroku site, so to fix the USE_AWS variable was added to the Gitpod environment. 
This solved the issue, however care was needed to ensure any changes made on local css files were pushed to AWS.

# Deployment to heroku
This project was deployed to Heroku via the following steps:

Use pip3 install to install gunicorn, psycopg2-binary and dj-database-url

Create a requirements.txt file with: pip3 freeze --local > requirements.txt

Create a Procfile and add web: gunicorn robertclarkdesign.wsgi:application then add, commit and push these changes.

Log into Heroku, click New and Create New App. Give the project a unique name, choose the region and click Create App.

Add Heroku Postgres in the Add-ons search bar, select Free account and Submit Order Form to add to the project.

From the Settings menu, click Reveal Config Vars. Set the variables for:

AWS_ACCESS_KEY_ID - Your AWS Access Key
AWS_SECRET_ACCESS_KEY - Your AWS Secret Access Key
DATABASE_URL - Your Postgres Database URL
SECRET_KEY - Your Secret Key
STRIPE_PUBLIC_KEY - Your Stripe Public Key
STRIPE_SECRET_KEY - Your Stripe Secret Key
STRIPE_WH_SECRET - Your Stripe WH Key
USE_AWS - True
Keys for Stripe and AWS can be found on their respective sites.

Select Github from the Deployment Method section, and select Automatic Deployment.

Select your Github user and enter the name of your repo, then select it from the search and click Connect.

Ensure your settings.py file is set to:

if 'DATABASE_URL' in os.environ:
   DATABASES = {
      'default': dj_database_url.parse(os.environ.get('DATABASE_URL'))
   }
else:
   DATABASES = {
      'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': BASE_DIR / 'db.sqlite3',
      }
   }
Use python3 manage.py makemigrations and python3 manage.py migrate to migrate database models to the Postgres database.

Load data fixtures using python3 manage.py loaddata <fixture> ensuring fixtures are loaded in the following order:

categories
Create a new superuser using python3 manage.py createsuperuser and entering a email, username and password.

Ensure settings.py has ALLOWED_HOSTS = ['robertclarkdesign.herokuapp.com', 'localhost']

In Stripe add the Heroku app checkout URL as the new webhook and update settings.py with new Stripe environment variables and email settings.

Add, commit and push all changed to Heroku.

If you are using AWS as this guide expects, please continue with the following

On Amazon Web Services (AWS), create an account, locate S3 and add a new bucket. For more information on this process, please visit AWS

Add the following CORS configuration:

[
{
      "AllowedHeaders": [
         "Authorization"
      ],
      "AllowedMethods": [
         "GET"
      ],
      "AllowedOrigins": [
         "*"
      ],
      "ExposeHeaders": []
}
]
With pip3 install install boto3 and django.storages and freeze with pip3 freeze --local > requirements.txt

Add storages to the list of INSTALLED_APPS in settings.py

Ensure the settings.py file has the following:

if 'USE_AWS' in os.environ:
   # Cache Control
   AWS_S3_OBJECT_PARAMETERS = {
      'Expires': 'Thu, 31 Dec 2099 20:00:00 GMT',
      'CacheControl': 'max-age=94608000',
   }

   # Bucket Config
   AWS_STORAGE_BUCKET_NAME = 'fashion.plaza'
   AWS_S3_REGION_NAME = 'eu-north-2'
   AWS_ACCESS_KEY_ID = os.environ.get('AWS_ACCESS_KEY_ID')
   AWS_SECRET_ACCESS_KEY = os.environ.get('AWS_SECRET_ACCESS_KEY')
   AWS_S3_CUSTOM_DOMAIN = f'{AWS_STORAGE_BUCKET_NAME}.s3.amazonaws.com'

   # Static and Media files
   STATICFILES_STORAGE = 'custom_storages.StaticStorage'
   STATICFILES_LOCATION = 'static'
   DEFAULT_FILE_STORAGE = 'custom_storages.MediaStorage'
   MEDIAFILES_LOCATION = 'media'

   # Override static and media URLS in production
   STATIC_URL = f'https://{AWS_S3_CUSTOM_DOMAIN}/{STATICFILES_LOCATION}/'
   MEDIA_URL = f'https://{AWS_S3_CUSTOM_DOMAIN}/{MEDIAFILES_LOCATION}/'

Ensure the custom_storages.py file has the following:
from django.conf import settings
from storages.backends.s3boto3 import S3Boto3Storage


class StaticStorage(S3Boto3Storage):
   location = settings.STATICFILES_LOCATION


class MediaStorage(S3Boto3Storage):
   location = settings.MEDIAFILES_LOCATION
Delete DISABLE_COLLECTSTATIC from the Config Vars of Heroku.

Add, commit and push all changed to Heroku.

Running This Project Locally
To run this project locally, you will need to use an IDE such as Gitpod, Visual Studio or PyCharm.

This guide assumes you are using Gitpod:

Install the Gitpod Browser Extensions for Chrome and restart your browser.

Log into Gitpod and navigate to the GoBooks Project GitHub repository.

Click the green "Gitpod" button at the top of the repository.

import os
os.enivron["DEVELOPMENT"] = "True"
os.environ["SECRET_KEY"] = Your Secret Key
os.environ["STRIPE_PUBLIC_KEY"] = Your Stripe Public Key
os.environ["STRIPE_SECRET_KEY"] = Your Stripe Secret Key
os.environ["STRIPE_WH_SECRET"] = Your Stripe WH Secret Key
Ensure that all the requirements are downloaded by using the following command: pip3 install -r requirements.txt

Migrate models to the database with: python3 manage.py makemigrations and python3 manage.py migrate

Load data fixtures using python3 manage.py loaddata <fixture> ensuring fixtures are loaded in the following order:

categories
products
Create a new superuser using python3 manage.py createsuperuser and entering a email, username and password.

Run the app in your browser by inputting the following command: python3 manage.py runserver



# Acknowledgements

A huge thank you to the Tutor Support for helping me spot an error in my code 
that wouldn't let me render the edit word functionality - 
It's always the silly things that catch me out!