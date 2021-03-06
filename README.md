# Evax Assets Compressor

![Evax compressor logo](http://farm8.staticflickr.com/7166/6505430865_1f9f232e8c_o_d.png)


*Evax compressor make you feel lighter*

Evax is a simple asset packaging library for Ruby, providing JavaScript/CSS concatenation and compression using UglifyJS and a really simple regex based CSS compressor. Just because enough is enough.

The idea behind it is to have a really **simple library to compress your assets** in the simplest way without any weird dependency (who said Java?). There are nice assets packaging systems out there but they have too many options for some cases.

Create a YAML file describing assets, Evax will take it and compress the javascript and stylesheets files to the *output directory* of your choice. Done.

## Instalation

    gem install evax

## Dependencies

As *Evax* has a dependency in *uglifier* who has a dependency in *execjs* it is needed to have a proper **JS runtime** installed in your system. Pick one from the [execjs README page](https://github.com/sstephenson/execjs)

## Usage

### assets.yml

    compress:    off # default on
    output_path: tmp/

    javascripts:
      js_package_one:
        - test/fixtures/javascripts/one.js
        - test/fixtures/javascripts/two.js
        - test/fixtures/javascripts/three.js
      js_package_two:
        - test/fixtures/javascripts/four.js

    stylesheets:
      css_package_one:
        - test/fixtures/stylesheets/one.css
        - test/fixtures/stylesheets/two.css
      css_package_two:
        - test/fixtures/stylesheets/three.css
        - test/fixtures/stylesheets/four.css

### Command Line

    evax /path/to/assets.yml /base/path

### Rails

Add **evax** to your Gemfile:

    gem 'evax'

Create a Rake task for running it, e.g.:

    namespace :evax do
      ASSETS_PATH = "#{Rails.root}/config/assets.yml"
      BASE_PATH   = Rails.root

      desc 'Build assets'
      task :build do
        Evax.new( ASSETS_PATH, BASE_PATH ).build
      end
    end
