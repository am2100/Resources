# Quick Rails Site Framework setup.

Nb. Beyond the fact that this works for my Windows XP system, I can offer you no guarantees!

## Rename application.html.erb
    application.html.haml

## Add Base Haml
    !!! 5
    %html
      %head
        = google_verification_code if current_page?(action: 'home')
        = tag('meta', name: "keywords", content: yield(:keywords))
        = tag('meta', name: "description", content: yield(:description))
        %title= full_title(yield(:title))
        = render 'layouts/stylesheets'
        = javascript_include_tag "application"
        = csrf_meta_tags
        = render 'layouts/google_analytics'
      %body
        #wrapper
          = render 'layouts/header'
          = render 'layouts/primary_nav'
          = yield
          = render 'layouts/footer'
        #legal
          = raw copyright
          = link_to 'Design: XJJZ | Designed Communications', 'http://xjjz.co.uk/'
          = debug(params) if Rails.env.development?

## Create partials
### _footer.html.haml
    #footer
      %ul.horizontal-nav
        %li
          = link_to 'Home', root_path
        %li
          = link_to 'Page 1', page_1_path
        %li
          = link_to 'Contact', contact_path

### _google_analytics.html
    -# TODO Add analytics code last thing

### _header.html.haml
    #header
      %h1
        MySite.com
      %h2
        My Strap Line

### _primary_nav.html.haml
    %ul.horizontal-nav
      %li
        = link_to 'Home', root_path
      %li
        = link_to 'Page 1', page_1_path
      %li
        = link_to 'Contact', contact_path

### _stylesheets.html.haml
    = stylesheet_link_tag 'application', :media => 'screen'
    /[if lt IE 9]
      = stylesheet_link_tag 'ie8'
    /[if lt IE 8]
      = stylesheet_link_tag 'ie7'
    /[if lt IE 7]
      = stylesheet_link_tag 'ie6'

## Create additional stylesheet files
    ie8.css
    ie7.css
    ie6.css

## Create lib/stylesheets directory and add:
    reset.css

## Create SCSS files
### _clearfix.scss
    .clearfix:after {
      content:".";
      display:block;
      height:0;
      clear:both;
      visibility:hidden;
    }

    .clearfix {
      display:inline-table;
    }

    * html .clearfix {
      height:1%;
    }
    .clearfix{
      display:block;
    }

### _colors.scss
    $project-light: #e6e6e6;
    $project-pale: #cfcfcf;
    $project-mid: #b2b2b2;
    $project-dark: #333;

## Create css.scss files
    layout.css.scss
    text.css.scss

### Create wireframe_layout.css.scss
    @import "colors";
    @import "clearfix";

    html{
      background: $project-light;
    }

    html, body
    {
      height: 100%;
    }

    body
    {
      width: 960px;
      margin: 0 auto;
    }

    img{
      padding: 10px;
      border: 1px solid $project-mid;
    }

    #wrapper {
      background: #fff;
      border: 1px solid $project-mid;
    }

    #header {
      border-bottom: 1px solid $project-mid;
      padding: 20px 40px;
    }

    .horizontal-nav {
      padding: 20px 40px 13px 40px;
      border-bottom: 1px solid $project-mid;

      li {
        list-style-type: none;
        display: inline-block;
        
        a {
          border: none;
          border-right: 1px solid $project-mid;
          display: inline-block;
          padding: 0 10px;
          color: $project-dark;
          text-decoration: none;

          &:hover, &:focus {
            color: $project-mid;
          }
        }

        span {
          border-right: 1px solid $project-dark;
          padding: 0 10px;
        }

        .selected {
          color: $project-mid;
        }
      }

      .no-border {
        a, span {
	  border-right: none;
        }
      }
    }

### Create wireframe_text.css.scss
    @import "colors";

    body {
      font-family: sans-serif;
      font-size:62.5%;
      color: #000;

      a {
        font-family: sans-serif;
        color: $project-dark;
        text-decoration:none;
        border-bottom: solid 1px $project-mid;

        &:hover, &:focus {
          color: $project-mid;
          border-bottom: solid 1px $project-light;
        }
      }

      blockquote {
        font-size: 1.4em;
        line-height: 1.4;
      }

      dt, dd {
        font-size: 1.4em;
        font-family: sans-serif;
        line-height: 1.285;
      }

      dt {
        font-size: 1.8em;
        font-family: sans-serif;
      }

      form {
        font-size: 1.4em;
        line-height: 1.2;

        input {
          margin: 0 0 20px 0;
        }

        input[type="submit"] {
          margin-bottom:0;
        }
      }

      h1{
        font-size: 3.2em;
      }

      h2 {
        font-size:3em;
        line-height: 1.2;
      }

      h3 {
        font-size: 2.4em;
        font-family: sans-serif;
        line-height: 1.2;
        margin-bottom: 0.75em;
      }

      h4 {
        font-size: 1.8em;
        font-family: sans-serif;
        margin-bottom: 0.45em;
      }

      h5 {
        font-size: 1.4em;
        font-family: sans-serif;
        line-height: 1.285;
        margin-bottom: 0.45em;
        font-weight: bold;
      }

      p {
        margin-bottom: 1em;
        font-size: 1.4em;
        font-family: sans-serif;
        line-height: 1.285;
      }

      strong {
        font-family: sans-serif;
        font-weight: bold;
      }

      table {
        font-size: 1.2em;

        th {
          font-weight: bold;
        }

        th, td {
          vertical-align: top;
          padding: 7px 10px 7px 0;
        }

        tr {
          border-bottom: dotted 1px $project-mid;
        }
      }

      ul {
        font-size: 1.4em;
        font-family: sans-serif;

        li {
          list-style-type: none;
          /* background: url("list-dot.gif") 0px 0.6em no-repeat;*/
          padding-left: 1em;
          margin-bottom: 0.5em;
        }
      }

      ul.horizontal-nav {
    
        li {
          background: none;
          padding-left: 0;
        }
      }
    }

## Setup application.css
     *= require reset
     *= require wireframe_text
     *= require wireframe_layout

## Add Application Helpers
    module ApplicationHelper

      # Returns the full title on a per-page basis
      def full_title(page_title)
        base_title = "Client Name" # TODO Add Client Name 
        if page_title.empty?
          base_title
        else
          "#{base_title} | #{page_title}"
        end
      end

      # Returns the copyright with this years date
      def copyright
        year = Time.now.strftime("%Y")
        "&copy; #{year} My Client" # TODO Add Client Name
      end

      def google_verification_code
        tag('meta',
          name: "google-site-verification",
          content: "" # TODO Add verification code
        )
      end
    end

## Add title, keyword and description placeholders at top of all public page views
    = provide(:title, 'Page Title') # TODO Add page title
    = provide(:keywords, '')        # TODO Add page keywords
    = provide(:description, '')     # TODO Add page description

>\> CommandLine

