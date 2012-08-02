Initial Inertia in Rapid Prototyping, or; How To Build A Sophisticated Rails App, By Starting Off On The Right Foot, or; How To Win A WebApp Hackathon
===================================================================================================================
Use postgresql from the start, for Heroku compatibility.
--------------------------------------------------------

- Visit http://postgresapp.com/ & download the app.
- Install & run the app.
- Execute "$ psql -h localhost" to enter local psql terminal.
- Execute "=# select * from pg_roles;" to list the accounts w/ access privelages.
- Execute "$ rails new myApp -d postgresql" to create psql rails app.
- Fix db/database.yml to include your psql credentials -- 'username' and 'password'.
- Fit 'host: localhost' into db/database under 'test:' & 'production:'
- Note: Heroku is gonna throw database.yml away & use its own settings.
- Execute "$ rake db:create:all" to create your psql databases.


Use GitHub
----------
- $ gem install github
- $ gh create-from-local


Use RVM
-------


Use Powder
----------


Use [Rspec](https://github.com/rspec/rspec-rails/), [Fabrication](https://github.com/paulelliott/fabrication/) w/ [fFaker](http://faker.rubyforge.org/rdoc/) & [Capybara](https://github.com/jnicklas/capybara/) for solid TDD utility.
---------------------------------------------------------------------

- Throw these guys in your Gemfile :test, & :development groups: 'rspec-rails', 'capybara', 'fabrication' & 'ffaker' for plausible nonsense.
- $ bundle
- Execute "$ rails generate rspec:install" to add the spec directory and some skeleton files, including the "rake spec" task.
- To configure Rails 3 to produce fabricators when you generate models, add to your config/application.rb:

  config.generators do |g|
    g.test_framework      :rspec, fixture: true
    g.fixture_replacement :fabrication
  end
- Fit "require 'capybara/rspec'" into your spec_helper.rb, and don't forget that Capybara only looks into 'spec/requests' or 'spec/integration'


Tigthen that Loop with [Guard](https://github.com/guard/guard/)
----------------------------
- Add gem 'guard' to your :development group, & $ bundle.
- Generate an empty Guardfile with "$ guard init"
- [Optional: install growlnotify & gem 'growl']
- Always run guard with "$ bundle exec guard"


Let [Devise](https://github.com/plataformatec/devise/) & [CanCan](https://github.com/ryanb/cancan/) handle expected user behavior
-------------------------------------------------
- Add gems 'cancan' & 'devise' to your Gemfile & $ bundle
- $ rails generate devise:install
- Follow the instructions.  Something like this:
### config/environments/development.rb
  # Ensure you have defined default url options for Devise.
  config.action_mailer.default_url_options = { :host => 'localhost:3000' }
