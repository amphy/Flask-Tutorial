# Flask-Tutorial
This is a Flask Tutorial for creating Flask applications with Apache.

# Introduction
When I was first learning to create web applications, the world was a very large place. There are so many technologies out there that it can be hard to select just one. At the time, I knew little about web development; my server had an Apache server set up and the only way I had heard of using Apache before was with PHP. However, when working on an API challenge with a friend, whose specialty was Python, we had to find some way to use Python on the web which lead us to the discovery of two popular Python frameworks: Django and Flask. We ended up going with Flask.

However, the setup with Flask was very difficult. Since my webserver was an Apache server (and because I didn’t realize Flask itself could serve pages), I had to scour the web to find some way to configure my Flask setup to work with Apache. It was very difficult to find any documentation and ended with me having to work for hours before Flask was finally working with Apache. To help others avoid that, I wanted to create a tutorial that walked you step by step through creating a Flask application and serving it through Apache (if you chose that route). An alternative to this is to serve the Flask application through something like Heroku.

All of these instructions are for a Unix based system.

# Installing Flask

The first step is to install Flask from the official site. The documentation walks you through installing Flask. The docs recommend that you use a virtual environment when working with Flask on your system. If virtualenv is not installed on your system, you can use

$ sudo easy_install virtualenv
$ sudo pip install virtualenv
$ sudo apt-get install python-virtualenv

One of the three above options should work for installing virtualenv. Once that is done, we then make sure we are in the directory where our project will be and create a virtual environment

$ cd myApplication
$ virtualenv venv

This will create a virtual environment called venv in our myApplication directory. To activate your virtual environment, you can use

$ . venv/bin/activate
The next step is to then install Flask using pip. If you already have pip on your system, you can simply use

$ pip install Flask

Be sure to do this in the directory your application will be (for example, if your application is in a directory called “MyApplication”, be sure to install Flask within the “MyApplication” directory). You can find more information about pip here. After you have successfully installed Flask, it’s on to the next step.

# Configuring Apache

Because Flask can actually serve pages itself, there is some configuration that needs to be done in order to actually use Flask with Apache. In order to use Flask with Apache, you will first need to create a Web Server Gateway Interfact (WSGI) file. More information about WSGI can be found in its documentation.

The way I like to set up my projects is to have my main python script, my project folder, and my wsgi file to all have the same name. Within my WSGI file (in this example, called sampleapp.wsgi), I put the following

#!/usr/bin/python

import os
os.environ['PYTHON_EGG_CACHE'] = '/var/www/sampleapp/python-eggs'

activate_this = '/var/www/sampleapp/bin/activate_this.py'
execfile(activate_this, dict(__file__=activate_this))

import sys
sys.path.insert(0, '/var/www/sampleapp')
sys.path.append('/var/www/sampleapp')

from sampleapp import app as application
This file must be located within the same directory as the rest of your project. After setting up your WSGI file, the next step is to create a virtual host for Flask applications on your Apache server. Each time you create a new Flask application and want to serve it through Apache, you can edit this virtual host to include the new application.#!/usr/bin/python

import os
os.environ['PYTHON_EGG_CACHE'] = '/var/www/sampleapp/python-eggs'

activate_this = '/var/www/sampleapp/bin/activate_this.py'
execfile(activate_this, dict(__file__=activate_this))

import sys
sys.path.insert(0, '/var/www/sampleapp')
sys.path.append('/var/www/sampleapp')

from sampleapp import app as application
This file must be located within the same directory as the rest of your project. After setting up your WSGI file, the next step is to create a virtual host for Flask applications on your Apache server. Each time you create a new Flask application and want to serve it through Apache, you can edit this virtual host to include the new application.
