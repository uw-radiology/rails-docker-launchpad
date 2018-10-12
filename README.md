# rails-docker-launchpad
A launchpad :rocket: to get you started with a new containerized :whale: rails 5 app!

## How to Use This

This repo contains a Dockerfile and docker-compose.yml file to get you started
with a pretty basic rails dev environment running in a docker container.

* It will create a new docker image with Ruby, Rails, and NodeJS.
* It will create a docker image with a postgres database.
* It will start both containers and link them in a docker network.

---

* Fork (or clone) this repository (or download the ZIP).
* Run `docker-compose up --build -d`
* Run `docker-compose run <app name> rails new . --force --database=postresql`
* Files created by docker are owned by root, so you'll probably have to adjust the file permissions or ownership.
  * `sudo chown -R $USER:$USER .` should solve the problem.
  * You might have to make the files in the database directory (`/tmp/db` by default) owned by user postres or change the permissions.
* This generates a new Gemfile. You'll want to run `docker-compose build` again.
* Replace the contents of `config/database.yml` with the following:
```
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password:
  pool: 5

development:
  <<: *default
  database: myapp_development


test:
  <<: *default
  database: myapp_testdefault: &default   
```
* Run `docker-compose up` again.
* Create the database. Run `docker-compose run app rake db:create`
* Rails should now serve up your app at http://localhost:3000
