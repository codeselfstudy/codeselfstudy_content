---
title: How to Deploy an Express App on Heroku with Postgres and Knex
date: 2018-05-23 15:33
category: Node.js
tags: Heroku, Postgres
author: Josh
path: "/blog/deploy-node-postgres-heroku/"
---

Here are some quick notes on creating and deploying a node app on Heroku with Knex and Postgres.

## Your Express App

You should have an [Express.js](https://expressjs.com/) application that uses [Postgres](https://www.postgresql.org/) and [Knex](http://knexjs.org/).

The Express application should be a Git repo. The root of the Git repo should be at the same level as your Express app. In other words, the `.git/` directory should be right next to the `package.json` file. You can view the hidden `.git/` directory with the command `ls -alF`.

The `knexfile.js` file should have entries something like this--the important part is the `production` setting:

```javascript
module.exports = {
    development: {
        client: 'pg',
        connection: {
            host: '127.0.0.1',
            user: process.env.TODO_DB_USER,
            password: process.env.TODO_DB_PW,
            database: 'todos_test'
        },
        migrations: {
            directory: __dirname + '/db/migrations',
        },
        seeds: {
            directory: __dirname + '/db/seeds/development',
        },
    },
    production: {
        client: 'pg',
        connection: process.env.DATABASE_URL,
        migrations: {
            directory: __dirname + '/db/migrations',
        },
        seeds: {
            directory: __dirname + '/db/seeds/production',
        },
    },
};
```

## Adding Heroku

Create the Heroku project with:

```
$ heroku create
```

The command line should display an app name (something like `happy-everglades-12345`). There will also be a URL with the app name as the subdomain.

### Adding Postgres to Heroku

Add a Postgres database to Heroku:

```
$ heroku addons:create heroku-postgresql:hobby-dev
```

You should see a database URL something like this:

```text
Created postgresql-colorful-54321 as DATABASE_URL
```

Save that database name. (If you forget it, you can find it again by typing `heroku pg:info`.)

Find your Postgres database URL, where `<database_name>` is the database URL from the previous step:

```
$ heroku pg:credentials:url <database_name>
```

You should see a "Connection URL" that looks something like this:

```text
postgres://wsjalkfjwimvlz:7984738297a897843297f8928378439e798437d84874937287832794382747@ec2-11-11-22-345.compute-1.amazonaws.com:5432/d8jeil4j3i2s70
```

Copy that onto your clipboard and then send it to Heroku as an environment variable named `DATABASE_URL`:

```
$ heroku config:set DATABASE_URL='<the_database_url_from_the_last_step>' -a <app_name>
```

Remember that `<app_name>` comes from the name of the Heroku app. You can always find it with `heroku info` and extracting it from the subdomain of the "Web URL field".

The `DATABASE_URL` name matches the database connection settings from the knexfile. Here's that section of the knexfile for reference:

```javascript
    production: {
        client: 'pg',
        // The next line is where the application will read that environment variable to connect to the database
        connection: process.env.DATABASE_URL,
        migrations: {
            directory: __dirname + '/db/migrations',
        },
        seeds: {
            directory: __dirname + '/db/seeds/production',
        },
    },
```

### Deploying the Code

Push your code to Heroku:

```
$ git push heroku master
```

### Running the Database Migrations

To run the migrations type:

```
$ heroku run knex migrate:latest
```

### Seeding the Database

Insert the seed data with:

```
$ heroku run knex seed:run
```

## Finishing Up

Open the app in the browser with:

```
$ heroku open
```

It should work. If not, leave a comment below. You can also view Heroku's Postgres documentation by running this command:

```
$ heroku addons:docs heroku-postgresql
```

If you're working with just a test application, you can destroy it when done by typing:

```
$ heroku apps:destroy -a <app_name>
```

P.S., if you're looking for information on using Knex, see [this YouTube tutorial](https://www.youtube.com/playlist?list=PL7sCSgsRZ-smPRSrim4bX5TQfRue1jKfw).
