# autometal-piwik
  * https://github.com/Achillefs/autometal-piwik
  * http://humbuckercode.co.uk/licks/gems/piwik

## DESCRIPTION:
A simple Ruby client for the Piwik API. This gem is based on Rodrigo Tassinari de Oliveira's piwik gem (https://github.com/riopro/piwik). Since it hasn't been updated since 2008, I took the liberty to fork it, and finish it up.

## FEATURES/PROBLEMS:

  * Object-oriented interface to the Piwik API;
  * For now, only a small subset of the API is implemented (only basic actions)

## SYNOPSIS:
Piwik is an open source web analytics software, written in PHP. It provides an 
extensive REST-like API, and this gem aims to be a simple Ruby wrapper to access 
this API in a Ruby-friendly way. For example:

    require 'rubygems'
    require 'piwik'
    Piwik.auth_token = "i need to configure simple-piwik with my auth_token here"
    Piwik.piwik_url = "http://piwik.mypiwikdomain.org"
    site = Piwik::Site.load(1)
    => #<Piwik::Site:0xb74bf994 @name="Example.com", @config={:auth_token=>"some_auth_key", :piwik_url=>"http://your.piwi.install"}, @id=1, @main_url="http://www.example.com", @created_at=Tue Jul 15 18:55:40 -0300 2008>
    site.pageviews(:month, Date.today)
    => 3002378
    user = Piwik::User.load(1, 'http://piwik.mypiwikdomain.org', 'my_auth_key')
    => #<Piwik::User:0xb66bf544 @login="Example.com", @config={:auth_token=>"some_auth_key", :piwik_url=>"http://your.piwi.install"}, @id=1, @main_url="http://www.example.com", @created_at=Tue Jul 15 18:55:40 -0300 2008>

Configuring with initializer config/initializers/simple-piwik.rb :
  
    if Rails.env.production? 
      Piwik.piwik_url  # "http://piwik.mypiwikdomain.org"
      Piwik.auth_token # "2ad590308b1efa590a9a43ad86d3ac1s"
    elsif Rails.env.development?
      #this is currently set to the same as production
      Piwik.piwik_url  # "http://piwik.mypiwikdomain.org"
      Piwik.auth_token # "2ad590308b1efa590a9a43ad86d3ac1s"
    end

  * Piwik website (http://piwik.org)
  * Piwik API reference (http://dev.piwik.org/trac/wiki/API/Reference)

## REQUIREMENTS:

    activesupport, rest-client, json

## INSTALL:

    gem install simple-piwik

## CHANGELOG:
  * 0.6.0 
  Merged a few updates from [Mihael's fork](https://github.com/Achillefs/autometal-piwik/pull/5)
  Gem now works with Rails 3.x, and the credentials specification strategy changed slightly
  * 0.4.2
  Final fix for inconsistent API outputs caused by Rails using its own version of XmlSimple.
  * 0.4.1
  Quick fixed api result parsing in site creation. The API's responses are inconsistent, but I am not sure why.
  * 0.4.0
  Added Piwik::Trackable controller mixing, pretty much swiped off of halfdan's piwik analytics project (https://github.com/halfdan/piwik_analytics/). The version included in this plugin is not suitable for application tracking, and is instead geared towards tracking multiple websites stored as ActiveRecord models
  * 0.3.0
  UsersManager CRUD implementation, with tests
  * 0.2.3
  Started adding some tests
  * 0.2.0
  Reworked plugin to also look for a rails config file called piwik.yml, and not just the .piwik user prefs file.
  * 0.0.2 2008-07-22 (riopro)
  * Added specs for existing API methods
  * Created RubyForge project at http://rubyforge.org/projects/piwik/
  * 0.0.1 2008-07-21 (riopro)
  * major enhancement:
  * Initial release

## LICENSE:
(The MIT License)

Copyright © 2010-2013 Achillefs Charmpilas, Humbucker Ltd

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the ‘Software’), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED ‘AS IS’, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.