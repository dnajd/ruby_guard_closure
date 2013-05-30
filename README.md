Ruby Guard Closure
================
Ruby using Guard to monitor javascript files. When a file changes it will compile them using google closure and generate a source map.

Getting Start
=============
Do the usual

     bundle install

Generate settings file with

     bundle exec rake init

Follow the instructions to edit the settings.yml file and finally run

	bundle exec rake

How it Works
============

Go edit a file in your watchdir and it will 

* minify all javascripts using closure
* generate a closure map file
* append the map directive to the end of the minified js file

You must enable source maps in chrome developer tools

* open developer tools
* click the gear in the lower right corner
* check the 'enable source maps' check box