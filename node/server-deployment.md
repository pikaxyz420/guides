---
title: "Server Deployment With NodeJS"
---

#### [Home](https://pikaxyz420.github.io/guides/)

---

## Server Deployment With NodeJS

Deploying your server-side code with NodeJS

## Contents

- [Overview](#overview)
- [Questions](#questions)

## Overview

- Generate your local SSH-key
- Add your local SSH Key to your GitHub account
- Push your local repository to your remote repository in GitHub
- Select a cloud provider
- Provision a server instance
- Configure your server's network firewall
- Connect via SSH to your server
- Install NodeJS, NPM / Yarn, PM2
- Install databases
- Generate your server's SSH-key
- Add your server's SSH Key to your GitHub Account
- Clone your remote repository in GitHub to your server
- Install your project's dependencies
- Set-up your project's configuration
- Create your project's SSL certificates
- Bundle your project's client scripts
- Set-up your databases & tables
- Test your project's server scripts
- Run your project's server scripts with PM2



#### Generate your local SSH-key

```sh
ssh-keygen
```

- https://www.ssh.com/ssh/keygen/

#### Add your local SSH Key to your GitHub account

- https://github.com/settings/keys

#### Push your local repository to your remote repository in GitHub

- Create a new GitHub repository here: https://github.com/new

You have three (3) options here:

- Clone your newly-created GitHub repository

```sh
git clone https://github.com/YOUR_USERNAME/YOUR_PROJECT.git
```

- Create a new local git repository, then add your remote GitHub repository 

```sh
git init
git add README.md
git commit -m "first commit"
git branch -M master
git remote add origin https://github.com/YOUR_USERNAME/YOUR_PROJECT.git
git push -u origin master
```

- On your existing local git repository, add your remote GitHub repository

```sh
git remote add origin https://github.com/YOUR_USERNAME/YOUR_PROJECT.git
git branch -M master
git push -u origin master
```

#### Select a cloud provider

You can use the following:

- DigitalOcean
- Hetzner
- Vultr
- Linode
- Google Cloud Platform
- Microsoft Azure
- Amazon Web Services

#### Provision a server instance

- DigitalOcean: https://www.digitalocean.com/docs/droplets/how-to/create/
- Google Cloud Platform: https://cloud.google.com/compute/docs/quickstart-linux
- Microsoft Azure: https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal

#### Configure your server's network firewall

- DigitalOcean: https://www.digitalocean.com/docs/networking/firewalls/how-to/

#### Connect via SSH to your server

- DigitalOcean: https://www.digitalocean.com/docs/droplets/how-to/connect-with-ssh/

#### Install NodeJS, NPM / Yarn, PM2

- https://github.com/nodesource/distributions#installation-instructions
- https://classic.yarnpkg.com/en/docs/install/#debian-stable
- https://pm2.keymetrics.io/docs/usage/quick-start/

#### Install databases

- Install your PostgreSQL / MySQL, Redis, etc.

#### Generate your server's SSH-key

```sh
ssh-keygen
```

- https://www.ssh.com/ssh/keygen/

#### Add your server's SSH Key to your GitHub Account

- https://github.com/settings/keys

#### Clone your remote repository in GitHub to your server

```sh
git clone https://github.com/YOUR_USERNAME/YOUR_PROJECT.git
```

#### Install your project's dependencies

```sh
cd ./YOUR_PROJECT
npm install
```

#### Set-up your project's configuration

- Environment variables
- JSON config files

#### Create your project's SSL certificates

- https://certbot.eff.org/lets-encrypt/ubuntufocal-other

#### Bundle your project's client scripts

These could be your webpack, gulp, or rollup scripts

#### Set-up your databases & tables

Create your databases, create your tables, etc.

#### Test your project's server scripts

Something like:

```sh
node ./server/server.js
```

- Can you connect to your HTTP endpoint (port 80)?
- Can you connect to your HTTPS endpoint (port 443)?
- Is your site loading?
- Is your site serving files?
- Is your site serving GET and POST requests?
- Are your websocket connections OK?
- Is your HTTP endpoint redirecting to HTTPS?
- Is your SSL working, check with: https://www.ssllabs.com/ssltest/
- Is other stuff working, check with: https://observatory.mozilla.org/

#### Run your project's server scripts with PM2

```sh
pm2 start ./server/server.js
```

## Questions

Feel free to open an issue or submit a PR, Thank you!

---

#### [Home](https://pikaxyz420.github.io/guides/)
