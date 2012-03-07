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

### Add rspec-rails, annotate, postgreSQL gems to Gemfile. Specify versions for all gems.
The use of the 'pg' gem assumes that you are planning on deploying to heroku.

Also included in the production group is the 'thin' gem. This is the server preferred by Heroku. it is commented out whilst you are working in the rails development environment - Windows doesn't like it! Remember to uncomment it when pushing your project up to heroku.

    source 'https://rubygems.org'

    gem 'rails', '3.2.1'

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

      gem 'uglifier', '>= 1.0.3'
    end

    gem 'jquery-rails'

### Bundle install
>\> bundle

### Tell rails to use RSpec
>\> rails g rspec:install

## Customise config/environments/production.rb for Heroku
> config.assets.compile=true

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

### Improve .gitignore
See Resources\git\gitignore\ for example .gitignore files, or use the general purpose one provided below:

    # Ignore bundler config
    /.bundle

    # Ignore the default SQLite database.
    /db/*.sqlite3

    # Ignore all logfiles and tempfiles.
    /log/*.log
    /tmp

    # Ignore other unneeded files.
    doc/
    *.swp
    *~
    *#
    .project
    .DS_Store

    # Compiled source
    *.com
    *.class
    *.dll
    *.exe
    *.o
    *.so

    # Packages
    # it's better to unpack these files and commit the raw source
    # git has its own built in compression methods
    *.7z
    *.dmg
    *.gz
    *.iso
    *.jar
    *.rar
    *.tar
    *.zip

    # Logs and databases
    *.log
    *.sql
    *.sqlite

    # OS generated files
    .DS_Store*
    ehthumbs.db
    Icon?
    Thumbs.db

### Commit change
>\> git commit -am "Improve .gitignore"

### Create GitHub Repository

### Push project up to GitHub
>\> git remote add origin git@github.com:\<username\>/\<gitHub_RepoName\>.git

>\> git push origin master

## Heroku

### Create Heroku app
>\> heroku create --stack cedar

### Uncomment 'thin' gem in Gemfile.

    group :production do
      gem 'thin'
    end

### Check Heroku configuration
>\> heroku info --app <appname>

For more config information:

>\> heroku config

### Configure Heroku to use Ruby 1.9.3 (if using Rails 3.2)
>\> heroku plugins:install https://github.com/heroku/heroku-labs.git  
>=> heroku-labs installed
>
>\> heroku labs:enable user_env_compile -a \<appname\>  
>=> ----> Enabling user_env_compile for \<appname\>... done  
>=> WARNING: This feature is experimental and may change or be removed without notice.
>
>\> heroku config:add RUBY_VERSION=ruby-1.9.3-p0  
>=> Adding config vars and restarting app... done, v8  
>=>   RUBY_VERSION => ruby-1.9.3-p0
>
>\> heroku config:add PATH=bin:vendor/bundle/ruby/1.9.1/bin:/usr/local/bin:/usr/bin:/bin  
>=> Adding config vars and restarting app... done, v9  
>=>   PATH => bin:vendor/bundl...in:/usr/bin:/bin

### Push Application to Heroku
>\> git push heroku master

### Run database migrations (Optional)
>\> heroku run rake db:migrate

### Initialize application database (Optional)
>\> heroku run rake db:seed

### Open Heroku site
>\> heroku open

## Rename your app
>\> heroku rename \<newname\>

## Heroku: Enabling Email with Sendgrid
### Enable free Sendgrid add-on
>\> heroku addons:add sendgrid:starter  
>=> Adding sendgrid:starter to <appname>... done.

TODO

## Heroku: Enabling Email with Gmail
###Customise config/environments/production.rb:

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

### Set Gmail username and password as Heroku environment variables:
>\> heroku config:add GMAIL_USERNAME=username@gmail.com GMAIL_PASSWORD=password

## Heroku: Setting up a custom domain
### Change DNS
    a.ns.zerigo.net
    b.ns.zerigo.net
    c.ns.zerigo.net
    d.ns.zerigo.net
    e.ns.zerigo.net

### Enable custom domains
>\> heroku addons:add custom_domains:basic

### Enable the Zerigo DNS add-on
>\> heroku addons:add zerigo_dns:basic

### Set domain names
>\> heroku domains:add \<mydomain.com\>  
>\> heroku domains:add \<www.mydomain.com>

## Heroku: Setting up mail servers
[Heroku](http://www.heroku.com/) \> Login \> My Apps \> \<appname\> \> Resources \> Add Ons \> Zerigo DNS \> Configure

### MX Records:
Host: \<blank\>  
Type: MX  
Priority: 0  
Refresh period: 10 minutes  
Data: \<mailexchangeuri>  

### A Record:
Host: mail  
Type: A  
Data: \<ip\>  

### Helpful information
[Support - Zerigo DNS](https://www.zerigo.com/docs/managed-dns)  
[Zerigo - Creating your first domain](https://www.zerigo.com/docs/managed-dns/creating_your_first_domain)  
[Heroku - Custom Domains](http://devcenter.heroku.com/articles/custom-domains)  
[Heroku - Installing Zerigo DNS](http://devcenter.heroku.com/articles/zerigo_dns)  
