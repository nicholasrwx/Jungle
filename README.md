# Jungle

A mini e-commerce application built with Rails 4.2 for purposes of teaching Rails by example.

## Setup Notes
- If there is a dependency that needs to be upgraded and the installation fails, run `bundle update dependency_name`.
  It will upgrade the dependency and continue installing the rest where it left off. Keep doing this for every dependency it fails on.
  Simply running `bundle update` will introduce breaking changes. The `Puma` Gem usually needs to be updated when going through the install.
  Possibly `rmagick` as-well.
- Publishable Key and Secret Key are the only vars in .env that need a value. They do not need to be in quotes.
- You need to enable strip testing capability in stripe account for test cards to work
- I believe you need to login as the super user postgres `sudo su - postgres` to login to the database and setup another user.
  Once this is done the created user should be able to login no problems as a regular user.
  Its a good idea to test the connection as a regular user afterwards.
- Ruby 2.3.5, rails, and some dependencies make use of openssl 1.1.1 so Ubuntu 18.04 is necessary unless you want to mess around with dependency issues.
- Ruby 2.3.5 works well if you use the right linux version, openssl1.1, and update packages on an only whats necessary basis.
- If you already have git setup on your system, wsl should be able to use it no problem.

## Additional Dependencies:
- make
- pacman
- brew
- gcc
- libssl-dev
- gpg
- gnupg2 ( used for rvm gpg keys )
- build-essential
- libmagickwand-dev libmagickcore-dev ( required for gem - rmagick 5.5.0 )
- node 14.21.3 ( used by rails when running rake command )
- wsl - Ubuntu 18.04 ( for openssl 1.1 required by ruby, rails, and some deps )

## Running RoR on Windows 11
Install windows subsystem for linux:
- `wsl --install -d Ubuntu-18.04` // matches the project as we need openssl 1.1 for ruby 2.3.5
- Restart system
- open powershell and run `wsl`
- `sudo apt-get update`
- `sudo apt-get upgrade`
- openssl version ( ensure openssl is version 1.1 )

Removing windows subsystem for linux:
- `wsl --unregister <distro_name>` 					        // generally ubuntu
- `C:\Users\<YourUsername>\AppData\Local\Packages` 	// find distro folder and delete. This can contain a virtual hard drive for the system.
- `Restart Windows`

Ruby on Rails doesn't run all too well on windows.
There are dependency issues, so it is best to install wsl then install ruby and rails in this linux environment.

## Ruby on Rails Setup:
- Install RVM using guide here - [rvm.io](https://rvm.io/)
- `rvm install 2.3.5` // required to install application dependencies
- `rmv install 3.x`   // required to install rails 4.2

## Postgres Setup:
- download postgresql deb or tar ( if source list is broken and can't do it through apt )
- install using deb file or extract tar file with `tar -xvzf postgresql-9.6.20.tar.gz`
- follow tar installation instructions
- switch to postgres super user `sudo su - postgres`
- login to postgres `psql -U postgres`
- setup database role with login capabilities `CREATE USER development;`
- create database `jungle_development`
- create database `jungle_test`
- logout with `\q`
- sign out of super user
- check postgres is running `sudo systemctl status postgresql`
- test connection `psql -U development -d jungle_development`

## Rails Setup:
- Use Ruby 3.x
- Install rails 4.2 with RVM - [rvm.io](https://rvm.io/)
- Switch back to Ruby 2.3.5

## Application Setup
1. Run `bundle install` to install dependencies
2. Create `config/database.yml` by copying `config/database.example.yml`
3. Create `config/secrets.yml` by copying `config/secrets.example.yml`
4. Run `bin/rake db:reset` to create, load and seed db
5. Create .env file based on .env.example
6. Sign up for a Stripe account
7. Put Stripe (test) keys into appropriate .env vars
8. Run `bin/rails s -b 0.0.0.0` to start the server

## Stripe Testing

Use Credit Card # 4111 1111 1111 1111 for testing success scenarios.

More information in their docs: <https://stripe.com/docs/testing#cards>

## Dependencies

* Rails 4.2 [Rails Guide](http://guides.rubyonrails.org/v4.2/)
* PostgreSQL 9.x
* Stripe
