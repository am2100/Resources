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
        #wrapper.page-shadow
          = render 'layouts/header'
          = render 'layouts/primary_nav'
          = yield
          = render 'layouts/footer'
        #legal
          = raw copyright
          = debug(params) if Rails.env.development?

## Create partials
### _footer.html.haml
    #footer
      = raw copyright
	:plain
	  Design:  <a href="http://xjjz.co.uk/">XJJZ | designed communications</a>

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

>\> CommandLine

