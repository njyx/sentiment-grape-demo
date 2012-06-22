## 3scale Example Sentiment API - V1.0: Basic API Method Calls and Authentication

This is a very basic API that returns the sentiment value of a word or a sentence. You can define the sentiment value of any additional word that is not in the dictionary.

The API is meant to serve an example of how you can easily create an API, and how you can use the free 3scale platform to control, manage and monitor the operations of the API so that you only have to do the fun part.

The original sentiment values are taken from the dataset AFINN-111.txt from [Denmark Technical University](http://www2.imm.dtu.dk/pubdb/views/publication_details.php?id=6010) 

The API is built using the GRAPE API Framework (https://github.com/intridea/grape) and the 3scale API plugin for ruby (https://github.com/3scale/3scale_ws_api_for_ruby / https://support.3scale.net/libraries).

## This Version

This version contains 2 resources and 3 method calls each of which returns dummy content only. In addition it adds 3scale basic API call authentication to the system. 

## Adding 3scale

The demo uses 3scale authentication for API calls. To set this up you need a free account and key from http://www.3scale.net/. 

 * Create a free account. 

 * Navigate to the "Account" page (top right of the screen) to retrieve you provider key.

 * Navigate to the "Accounts" listing (main menu) to retrieve a sample _AppID_ and _AppKey_ for the example calls.

## Configuration (Generic)

Generic Setup is as follows: 

 * Ensure you have the right base Gems available:

	$ gem install grape
	$ gem install 3scale_client
	
   If you're using Bundler, add the gem to Gemfile (there is a sample Gemfile in the repository)
	
	gem 'grape'
	gem '3scale_client'
	
 * Also make sure you have some JSON helpers available 

	$ gem install json
	
   If you're using Bundler, add the gem to Gemfile (there is a sample Gemfile in the repository)
	
	gem 'json'

 * In app/sentimentapi.rb code ensure you're requiring the right gems:
 
	require 'grape'
	require 'json'
	require '3scale_client'
	
 * Start the API...

	$ exec rackup
	

## Configuration (Heroku)

If you're using Heroku, follow these instructions (based on https://devcenter.heroku.com/articles/quickstart, https://devcenter.heroku.com/articles/ruby):

 * Make sure you have the "Heroku toolbelt":https://toolbelt.heroku.com/ installed.

 * Login to Heroku

	$ heroku login
	
 * Check the Gemfile is present and correct (in the repository).

 * Check the Procfile is present and correct (in the repository). It should contain a line like:

	web: bundle exec rackup config.ru -p $PORT

 * Run this with foreman - by default it will run on port 5000

	$ foreman start
	
Once you have tested it works locally, you can deploy to Heroku in the normal way:

 * Add to Git:

	$ git init
	$ git add .
	$ git commit -m "init"
	
 * Create the app:

	$ heroku create
	
 * Push and Launch

	$ git push heroku master
	
 * Check it is running: 

	$ heroku ps
	
 * Check the logs:

	$ heroku logs
	
You can visit the app with "$ heroku open" - however, you will likely get a 404 error on the home page - you need to navigate to the right resource URLs (below). See the "Heroku ruby pages":https://devcenter.heroku.com/articles/ruby for more details on deployment and trouble shooting.

## Usage

Using one of the methods above, your API should now be ready for use. 

Call one method of the API with curl (or with your browser if you want)

	curl -X GET -g "http://localhost:8080/v1/words/fantastic.json

The above call returns 

	{"word:"fantastic","sentiment":4}






