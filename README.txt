Mongoid::Grid / Rack::Grid

  Mongoid::Grid is a plugin for mongoid that uses GridFS.  Heavily inspired
  by grip (http://github.com/jnunemaker/grip)

  Rack::Grid is used to serve a GridFS file from rack.  Mostly copied
  from http://github.com/skinandbones/rack-gridfs

  Download the source at
  http://github.com/dusty/mongoid_grid


Installation

  Put the libraries in your project however you want.

  # gem install mongoid_grid

  Or, make your own gem.

  # git clone http://github.com/dusty/mongoid_grid
  # cd mongoid_grid
  # gem build mongoid_grid.gemspec

  Then require the libraries you want to use.

  require 'mongoid/grid'
  require 'rack/grid'


Usage

  class Monkey
    include Mongoid::Document
    include Mongoid::Grid
    field :name
    attachment :image
  end

  m = Monkey.create(:name => 'name')

  # To add an attachment
  m.image = File.open('/tmp/me.jpg')
  m.save

  # To remove an attachment
  m.image = nil
  m.save

  # To get the attachment
  m.image.read

  # To use Rack::Grid with Sinatra

  configure do
    use Rack::Grid, :database => 'my_db'
  end

  <img src="<%= m.image_url %>" alt="<%= m.image_name %>" />


