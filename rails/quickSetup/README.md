# Quick Rails setup with optional git / heroku configuration
These instructions gleaned from various sources:

- Michael Hartl, Rails Tutorial
- RailsApp Project
- Kevin Skoglund

Thanks to you all!

Nb. Beyond the fact that this works for my Windows XP system, I can offer you no guarantees!

## Rails

### Setup a new rails project without Test::Unit framework.
>\> rails new project_name -T

### Remove public/index.html

### Add rspec-rails, annotate, postgreSQL gems to Gemfile. Specify versions for all gems.
The use of the 'pg' gem assumes that you are planning on deploying to heroku.

Also included in the production group is the 'thin' gem. This is the server preferred by Heroku. it is commented out whilst you are working in the rails development environment - Windows doesn't like it! Remember to uncomment it when pushing your project up to heroku.

    'https://rubygems.org'

    gem 'rails', '3.2.1'

    # Bundle edge Rails instead:
    # gem 'rails', :git => 'git://github.com/rails/rails.git'

    group :development do
      gem 'annotate', '~>2.4.1.beta'
    end

    group :development, :test do
      gem 'sqlite3', '1.3.5'
      gem 'rspec-rails', '2.8.1'
    end

    group :production do
      gem 'pg', '0.12.2'
      # gem 'thin'
    end

    # Gems used only for assets and not required
    # in production environments by default.
    group :assets do
      gem 'sass-rails',   '~> 3.2.3'
      gem 'coffee-rails', '~> 3.2.1'

      # See https://github.com/sstephenson/execjs#readme for more supported runtimes
      # gem 'therubyracer'

      gem 'uglifier', '>= 1.0.3'
    end

    gem 'jquery-rails'

    # To use ActiveModel has_secure_password
    # gem 'bcrypt-ruby', '~> 3.0.0'

    # To use Jbuilder templates for JSON
    # gem 'jbuilder'

    # Use unicorn as the web server
    # gem 'unicorn'

    # Deploy with Capistrano
    # gem 'capistrano'

    # To use debugger
    # gem 'ruby-debug19', :require => 'ruby-debug'

### Bundle install
>\> bundle

### Tell rails to use RSpec
>\> rails g rspec:install

## Git
### Initialise Git repo
>\> git init

>\> git add .

>\> git commit -m "Initial commit."

### Improve README file
    # <Client name> | <Application name>
    ## Developed by [XJJZ | designed communications](http://xjjz.co.uk/)

    [Jim Noble](mailto:jimnoble@xjjz.co.uk)

### Rename README file
>\> ren [drive:][path]README.rdoc README.md

### Commit change
>\> git commit -am "Improve README."

### Create GitHub Repository

### Push project up to GitHub
>\> git remote add origin git@github.com:\<username\>/\<gitHub_RepoName\>.git

>\> git push origin master

## Customise config/environments/production.rb for Heroku
> config.assets.compile=true

## Deploy the app to Heroku
>\> heroku create --stack cedar

>\> git push heroku master

>\> heroku open

# Setting up Heroku
## Add the 'thin' webserver gem to Gemfile for production apps
Add to Gemfile:

    group :production do
      gem 'thin'
    end

Nb. On Windows, you will need to comment this line out while working in Development environment.

## Check Heroku configuration
>\> heroku info --app <appname>

For more config information:

>\> heroku config

## Configure Heroku to use Ruby 1.9.3 (if using Rails 3.2)
>\> heroku plugins:install https://github.com/heroku/heroku-labs.git

>=> heroku-labs installed
>
>
>\> heroku labs:enable user_env_compile -a <appname>

>=> ----> Enabling user_env_compile for <appname>... done

>=> WARNING: This feature is experimental and may change or be removed without notice.
>
>
>\> heroku config:add RUBY_VERSION=ruby-1.9.3-p0

>=> Adding config vars and restarting app... done, v8

>=>   RUBY_VERSION => ruby-1.9.3-p0
>
>
>\> heroku config:add PATH=bin:vendor/bundle/ruby/1.9.1/bin:/usr/local/bin:/usr/bin:/bin

>=> Adding config vars and restarting app... done, v9

>=>   PATH => bin:vendor/bundl...in:/usr/bin:/bin

## Push Application to Heroku
>\> git push heroku master

## Run database migrations
If your application has any migrations.

>\> heroku run rake db:migrate

## Initialize application database
If you need to load database with data.

>\> heroku run rake db:seed

## Open Heroku site
>\> heroku open

# Enabling Email
## Enable free Sendgrid add-on
>\> heroku addons:add sendgrid:starter
>=> Adding sendgrid:starter to <appname>... done.

## Setting up Heroku to use GMail
Add the following to config/environments/production.rb:

    config.action_mailer.default_url_options = { :host => 'myapp.heroku.com' }
    config.action_mailer.delivery_method = :smtp
    config.action_mailer.perform_deliveries = true
    config.action_mailer.raise_delivery_errors = false
    config.action_mailer.default :charset => "utf-8"
    config.action_mailer.smtp_settings = {
      address: "smtp.gmail.com",
      port: 587,
      domain: "myapp.heroku.com",
      authentication: "plain",
      enable_starttls_auto: true,
      user_name: ENV["GMAIL_USERNAME"],
      password: ENV["GMAIL_PASSWORD"]
    }

Set Gmail username and password as Heroku environment variables:

>\> heroku config:add GMAIL_USERNAME=am2100xjjz@gmail.com GMAIL_PASSWORD=f4ABXn98

# Setting up a custom domain
## Change DNS
    a.ns.zerigo.net
    b.ns.zerigo.net
    c.ns.zerigo.net
    d.ns.zerigo.net
    e.ns.zerigo.net

## Enable custom domains
>\> heroku addons:add custom_domains:basic

## Enable the Zerigo DNS add-on
>\> heroku addons:add zerigo_dns:basic

## Set domain name
>\> heroku domains:add <mydomain.com>


