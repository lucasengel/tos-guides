# Immich on TOS

This guide will walk you through installing [Immich](https://immich.app) on your TOS device.

The following instructions were documented on TOS 5.1 but should work the same on TOS 6.

You don't need **any technical knowledge** to proceed, just follow the instructions as described below. We'll use the web UI for all the steps, no termina access is needed.

## Pre-requisites

- have a code editor, such as notepad (windows) or TextEdit (mac) or anything fancier at hand
- have access to your TOS web interface with your admin account
- at least 4gb of free space

## 1. DOWNLOAD NECESSARY FILES

Create a folder called `immich` on your machine and download the following files into it:

- https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml
- https://github.com/immich-app/immich/releases/latest/download/example.env

## 2. EDIT EXAMPLE.ENV FIELDS (optional)

Immich will live in a folder you specify in your NAS. You can opt to specify the locations of its database and the images folder. Any changes to this file are optional, though.

- open the `example.env` in your text editor
- remove the `#` before `TZ=` and replace everything after the `=` with a TZ Identifier from [this list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List)
- update the `DB_PASSWORD` field (you can generate a strong one using [pwgen](https://pwgen.io/en/))
- save and close the file

## 3. EDIT DOCKER-COMPOSE.YML

This may be not still be an issue by the time you're reading this. Unfortunately, the version of `docker compose` on TOS currently doesn't accept the property below.

- open the `docker-compose.yml` in your text editor
- under `services` `database` `healthcheck`, add a `#` before `start_interval`
- save and close the file

## 3. UPLOAD FILES TO YOUR NAS

- open your web UI and log in with the admin user
- open the `File Manager` app and find a location you'd like to have the app, anything will do
- move the `immich` folder from your computer to this location
- right click the `example.env` file and rename it to `.env`

## 5. INSTALL NECESSARY APPS

- open the `App Center` app and go to All on the right side
- search for Docker
- install `Docker Engine` and `Docker Manager`

## 6. DOCKER MANAGER

- open the `Docker Manager` app and go to Project on the right side
- click the plus sign on the top right corner
- use `Immich` as the `Project name`
- choose the folder from step 4 for the `Project path`
- `Local TNAS` is fine for the `Configuration file source`
- find the `docker-compose.yml` file for `Upload configuration file`
- click on `Verify YAML`, then `Apply`

You'll see a new entry called `Immich`. Wait until `Building...` turns into `Running...` and you're done!

## Accessing Immich

Immich uses port `2283` by default, if you haven't changed that in the `docker-compose.yml` file.

- on your browser, open your `http://<nas-ip-address>:2283/`
- on your immich mobile app, use `http://<nas-ip-address>:2283/api` as de server address
