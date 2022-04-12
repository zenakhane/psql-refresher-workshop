# psql refresh workshop


PostgreSQL refresh workshop - postgresql is a modern sql database.

The aim of this workshop is to:

* ensure psql is installed on your PC,
* you can create a psql database at [elephantsql.com](elephantsql.com)
* and that you can connect to it from your local machine using `psql`,
* as bonus we will also see if you can create a psql database locally.

You should be able to run sql `insert, update, delete & select` queries on the database.

> *Note:* we assume you already know some SQL but need a bit of a refresher. And yes PostgreSQL might be new to you as well.

Here are some sql statement examples:

```sql
select * from garment where id = $1
delete from garment where id = $1
update garment set description = $1 where id = $2
insert into garment (description, username, email, password, first_name, last_name) values ($1, $2, $3, $4, $5)

select gender, count(*) group by gender
```

## Run the tests, fix them


Install all the project dependencies using this command:

```
npm install
```

Run the tests using:

```
npm test
```

Fix all the failing tests. An refresh your sql knowledge in the process.

You will need postgresql installed locally see the instructions below to do it


## Installing postgresql

### Installing Postgres on Windows

Download Postgesql from [this link](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads) and install it.

Specify a password of `pg123` when prompted - this is for the `postgres` user.

### Installing Postgres on Linux

To install postgres on Linux use these commands:

```
sudo apt-get update
sudo apt-get install postgresql postgresql-contrib
```

After the installation you should have the `psql` command available on your system in the terminal console.

## Use these pg-promise methods

We will be using the [pg-promise](https://www.npmjs.com/package/pg-promise) module to access PostgreSQL from NodeJS in this workshop.

On `pg-promise` use these methods:

* `db.none` - for updates, deletes or inserts
* `db.one`  - for queries that returns one things, it will return an object, or a single variable
* `db.many` - for queries that returns many things, in the form of a list.

The above methods all return promises

```js
await db.none(sql);

const rows = await db.many(sql, [param1]);

// or

db.many(sql, [param1]).then(result => console.log(result));
```

Once a database is created click on the database on the Instances screen.
This will take you to the Details screen - see the url on that page and put it in a `.env` file in the route of your project.

```
DATABASE_URL=<your db url here>
```

Connect to your database using psql in the terminal run this command:

```
psql <your db url here>
```

Create the garment table in the new database using the `\i sql/garments.sql` command in `psql`.

## Using a local database

To create a local postgresql database follow the instructions below.

Connect to the database using the postgresql user:

```
sudo -u postgres psql;
```

Once done with that create a database & user:

```
create database garment_app;
create role gary login password 'gar123';
grant all privileges on database garment_app to gary;
```

Add the following entry to you `.env` file in the root of your project.

```
DATABASE_URL=postgres://gary:gar123@localhost:4567/garment_app
```