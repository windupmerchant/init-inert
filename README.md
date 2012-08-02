Initial Inertia in Rapid Prototyping, or; How To Build A Sophisticated Rails App, By Starting Off On The Right Foot, or; How To Win A WebApp Hackathon
===================================================================================================================
*...do not be misled; these checklists are not a replacement for reading the DOC.*
Use postgresql from the start, for Heroku compatibility.
--------------------------------------------------------

- [Download the app.](http://postgresapp.com/)
- Install & run the app.
- Execute `$ psql -h localhost` to enter local psql terminal.
- Execute `=# select * from pg_roles;` to list the accounts w/ access privelages.
- Execute `$ rails new myApp -d postgresql` to create psql rails app.
- Fix db/database.yml to include your psql credentials -- 'username' and 'password'.
- Fit 'host: localhost' into db/database under 'test:' & 'production:'
- Note: Heroku is gonna throw database.yml away & use its own settings.
- Execute `$ rake db:create:all` to create your psql databases.


Use GitHub
----------
- `$ gem install github`
- `$ gh create-from-local`


Use RVM
-------


Use Powder
----------


Use [Rspec](https://github.com/rspec/rspec-rails/), [Fabrication](https://github.com/paulelliott/fabrication/) w/ [fFaker](http://faker.rubyforge.org/rdoc/) & [Capybara](https://github.com/jnicklas/capybara/) for solid TDD utility.
---------------------------------------------------------------------

- Throw these guys in your Gemfile's :test, & :development groups: 'rspec-rails', 'capybara', 'fabrication' & 'ffaker' for plausible nonsense.
- $ bundle
- Execute `$ rails generate rspec:install` to add the spec directory and some skeleton files, including the 'rake spec' task.
- To configure Rails 3 to produce fabricators when you generate models, add to your config/application.rb:

        config.generators do |g|
          g.test_framework      :rspec, fixture: true
          g.fixture_replacement :fabrication
        end

- Fit `require 'capybara/rspec'` into your spec_helper.rb, and don't forget that Capybara only looks into 'spec/requests' or 'spec/integration'


Tigthen that Loop with [Guard](https://github.com/guard/guard/)
----------------------------
- Add gems 'guard' & 'guard-rspec' to your :development group, & $ bundle.
- Generate an empty Guardfile with `$ bundle exec guard init rspec`
- [Optional: install growlnotify & gem 'growl']
- Always run guard with `$ bundle exec guard`
- Caution: Guard will, by default, watch directories that don't, by default, exist.


Let [Devise](https://github.com/plataformatec/devise/) & [CanCan](https://github.com/ryanb/cancan/) handle expected user behavior
-------------------------------------------------
- Add gems 'cancan' & 'devise' to your Gemfile & $ bundle
- `$ rails generate devise:install`
- Follow the in-consle instructions.

          /config/environments/development.rb:
          # Ensure you have defined default url options for Devise.
          config.action_mailer.default_url_options = { :host => 'localhost:3000' }

          /routes.rb:
          root :to => "home#index"

          /views/layouts/application.html.erb:
          <p class="notice"><%= notice %></p>
          <p class="alert"><%= alert %></p>

          /config/application.rb
          # to not access the DB or load models when precompiling your assets.
          config.assets.initialize_on_precompile = false

- Run `$ rails generate devise MODEL` to generate your first type of user.
- Run `$ rake db:migrate`
- Run `$ rails generate cancan:ability` AND then edit the resulting file so that it refers to your devise MODEL, and [grants it appropriate permissions](https://github.com/ryanb/cancan/wiki/defining-abilities).