Initial Inertia in Rapid Prototyping, or; How To Build A Sophisticated Rails App, By Starting Off On The Right Foot
===================================================================================================================
  ### Use postgresql from the start, for Heroku compatibility.
  - Visit http://postgresapp.com/ & download the app.
  - Install & run the app.
  - Execute "$ psql -h localhost" to enter local psql terminal.
  - Execute "=# select * from pg_roles;" to list the accounts w/ access privelages.
  - Execute "$ rails new myApp -d postgresql" to create psql rails app.
  - Fix db/database.yml to include your psql credentials -- 'username' and 'password'.
  - Fit 'host: localhost' into db/database under 'test:' & 'production:'
  - Note: Heroku is gonna throw database.yml away & use its own settings.
  - Execute "$ rake db:create:all" to create your psql databases.
  ### Use a tight testing suite from the start
  - Like this
  ### Don't reinvent the wheel: Devise, CanCan & Bootstrap
  - Some are harder than others to remove later.