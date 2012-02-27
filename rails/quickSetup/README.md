# Quick Rails setup with git / heroku configuration

## Setup a new rails project without Test::Unit framework.
>\> rails new project_name -T

## Remove public/index.html

## Update Gemfile to include rspec-rails / annotate / postgreSQL & specify gem versions.

    source 'https://rubygems.org'

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

## Bundle install
> bundle

## Tell rails to use RSpec
> rails g rspec:install

## Initialise Git repo
>> git init
>> git add .
>> git commit -m "Initial commit."

## Improve README file
    # <Client name> | <Application name>
    ## Developed by [XJJZ | designed communications](http://xjjz.co.uk/)

    [Jim Noble](mailto:jimnoble@xjjz.co.uk)

## Rename README file
> ren [drive:][path]README.rdoc README.md

## Commit change
>> git commit -am "Improve README."

## Create GitHub Repository

## Push project up to GitHub
>> git remote add origin git@github.com:<uesrname>/<gitHub_RepoName>.git
>> git push origin master

## Customise config/environments/production.rb
> config.assets.compile=true

