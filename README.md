# Ruby on Rails / Create React App / ActiveAdmin stack

Credit to [this post's](https://dev.to/heroku/a-rock-solid-modern-web-stackrails-5-api--activeadmin--create-react-app-on-heroku-jfm) author, [Charlie Gleason](https://dev.to/superhighfives) for the hard work in getting this all set up. Here I've just taken his hard work and made it in to a template for next time I want to create a project like this. Please feel free to take this, and check out his tutorial for a great write up on how to get this set up from scratch.

This version uses gem 'pg' for easy development/deployment to Heroku. I assume you're using yarn - you'll need to adjust my yarn commands to your preferred program if you're not. 

Additionally, comes preinstalled with axios, redux, and react-router for just... ease of getting going.

Already set up for single page apps - will allow your SPA to handle 404 errors
and, of course, allow people to save links inside your app.

## Setup

* Clone this repo
* `bundle`
* `rake db:create`
* `rake db:seed` to create a default user
* `yarn --cwd client` to install dependencies


Versions:
Ruby version - 2.5.1
Rails version - 5.2.1

## Running Development Servers

`bin/rake start` starts up a rails server and a create react app server and opens a browser. Should be ready to roll!

## Very basics of ActiveAdmin

To get started with activeadmin, at the very basic end of the spectrum - you'll need to generate the ability for ActiveAdmin to mess with your stuff. Which is the whole point, right?

Tell active admin about a model:
`bin/rails generate active_admin:resource Modelname`

Then, permit ActiveAdmin to modify your fields in `app/admin/modelname.rb`
``` ruby
ActiveAdmin.register Drink do
  permit_params :title, :description, :steps, :source
end
```
Hit `http://localhost:3001/admin` to access the ActiveAdmin side. Use admin@example.com and the best password ever: password for development

## Deployment

Create an app on heroku,:

```
heroku apps:create

heroku buildpacks:add heroku/nodejs --index 1
heroku buildpacks:add heroku/ruby --index 2

git add .
git commit -vam "Initial commit"
git push heroku master

heroku run rake db:seed
```
