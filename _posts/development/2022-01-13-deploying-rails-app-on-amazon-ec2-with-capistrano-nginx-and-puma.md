---
layout: post
title:  "Deploying a Rails App on Amazon EC2 with Capistrano, Nginx, and Puma"
date:   2022-01-13 15:50:05 -0700
categories: [Development]
path: "development"
tags: ["Ruby on Rails"]
---
 In this tutorial, the stack I’ll be using is:
- Ubuntu 20.04 LTS
- Ruby, version 3.0.2
- Rails, version 6.1.4.1
- Rbenv
- PostgresQL
- Nginx
- Puma, version 4.3.9
- Capistrano
- NodeJS
- Github

First of all, create an Ubuntu Amazon EC2 Instance.

### Install curl, nodejs and required libraries.
```sh
# Terminal: Production
sudo apt update
sudo apt install curl
sudo apt install zlib1g-dev build-essential libssl-dev libreadline-dev
sudo apt install libyaml-dev libsqlite3-dev sqlite3 libxml2-dev
sudo apt install libxslt1-dev libcurl4-openssl-dev
sudo apt install software-properties-common libffi-dev nodejs
```

### Install yarn

```sh
# Terminal: Production
curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update && sudo apt install yarn
```

### Install rbenv

```sh
# Terminal: Production
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
cd ~/.rbenv && src/configure && make -C src
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
~/.rbenv/bin/rbenv init
# Follow instruction to add `eval "$(rbenv init - bash)"` to ~/.bashrc
source ~/.bashrc
type rbenv
```

### Install ruby-build

```sh
# Terminal: Production
git clone https://github.com/rbenv/ruby-build.git
PREFIX=/usr/local sudo ./ruby-build/install.sh
```

### Install ruby (version 3.0.2)

```sh
# Terminal: Production
rbenv install 3.0.2
rbenv global 3.0.2
```

### Install rails (version 6.1.4.1)

```sh
# Terminal: Production
gem install rails -v 6.1.4.1
rbenv rehash
rails -v
```

### Install Postgresql

```sh
# Terminal: Production
sudo apt install postgresql postgresql-contrib
sudo apt install libpq-dev
```

### Working with database

```sh
# Terminal: Production
sudo -u postgres createuser --interactive
  --> Create new user, it will ask for enter username
sudo -u postgres createdb <dbname>
  --> Create new database
sudo -u postgres psql
  --> use psql to set password and add user to database
postgres=# alter user <username> with encrypted password '<password>';
postgres=# grant all privileges on database <dbname> to <username>;
postgres=# \q
```

### Edit pg_hba.conf file to allow login with password
```sh
# Terminal: Production
sudo nano /etc/postgresql/12/main/pg_hba.conf
  local   all             postgres                            peer
  --> change peer to md5
sudo service postgresql restart
```

### Install Nginx
```sh
# Terminal: Production
sudo apt install nginx
```

### Create github repo and config deploy key
```sh
# Terminal: Production
ssh-keygen -t rsa
cat ~/.ssh/id_rsa.pub
```

#### Follow [these instructions](https://docs.github.com/en/developers/overview/managing-deploy-keys) to add the newly created key to your GitHub project.

### Adding Capistrano to your project

```sh
# Gemfile
# The Puma gem may already exist in your Gemfile. If not, add it
gem 'puma'

# If you already have a development group, you can add this into it
group :development do
  gem 'capistrano',         require: false
  gem 'capistrano-rvm',     require: false
  gem 'capistrano-rails',   require: false
  gem 'capistrano-bundler', require: false
  gem 'capistrano3-puma',   require: false
end
```
```sh
# Terminal: Development
bundle
cap install
```

#### This creates:
- Capfile, used to load some pre-defined scripts (selecting the right version of Ruby, pre-compiling assets, installing new gems, and more).
- config/deploy.rb, which holds configuration and environment variables

Update these files with the links below:
- [Capfile](https://gist.github.com/bnguyenb/c3dfe65152d6527db936646ad3be5930){:target="_blank"}
- [deploy.rb](https://gist.github.com/bnguyenb/02783b0e42f57ee535a93938699218d1){:target="_blank"}

```sh
# Terminal: Development
cap production deploy:initial
```

### Nginx configuration
Create file config/nginx.conf and update with this link:
[nginx.conf](https://gist.github.com/bnguyenb/5ec641ed8744ddaf8b6dc21ebc80e740){:target="_blank"}

```sh
# Terminal: Development
cap production deploy
```

```sh
# Terminal: Production
sudo rm /etc/nginx/sites-enabled/default
sudo ln -nfs "/home/ubuntu/apps/[APP_NAME]/current/config/nginx.conf" "/etc/nginx/sites-enabled/[APP_NAME]"
sudo service nginx restart
```

You’re all done! Now, anytime you want to push an update, all you have to do is commit your changes to your repo, then run:

```sh
# Terminal: Development
cap production deploy
```
#### I also created a video to show it. You can check it out on Youtube here:

<iframe width="560" height="315" src="https://www.youtube.com/embed/3OJcUvnixS8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br />