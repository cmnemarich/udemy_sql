# Basic PostGreSQL Commands

## Accessing postgres
You can access postgres one of two ways:
 1. Switching to the `postgres` user and entering the PostGreSQL prompt.
 2. Entering commands as the `postgres` user directly from your regular account.

For the first method, start by switching to the `postgres` account using the following command:
  `$ sudo -i -u postgres`
Then enter the PostGreSQL prompt using this command:
  `$ psql`

For the second method, you can access the postgres prompt using `sudo` as such:
  `$ sudo -u postgres psql`

## Exiting out of PostGreSQL prompt
`postgress=# \q`

If you used the first method above, you can return to using your regular user account with the following command:
`postgres@server:~$ exit`

## Creating a new role
 1. While logged in as the postgres account:
  `postgres@server:~$ createuser --interactive`

 2. Using `sudo`:
  `sudo -u postgres createuser --interactive`

Once you have entered one of the above commands, you will then be prompted with some choices:
```
Output
Enter name of role to add: sammy
Shall the new role be a superuser? (y/n) y
```

## Creating a database
Postgres will make the assumption that for any role used to log in, that role will have a database with the same name which it can access.

E.g. if the user you created in the last section is called **sammy**, that role will attempt to connect to a database which is also called "sammy" by default. You can create the appropriate database with the `createdb` command.

1. While logged in as the postgres account:
 `postgres@server:~$ createdb sammy`

2. Using `sudo`:
 `sudo -u postgres createdb sammy`

## Opening a Postgres prompt with the new role
To log in with `ident` based authentication, you'll need a Linux user with the same name as your Postgres role and database.

If you don't have a matching Linux user available, you can create one with the `adduser` command:
`$ sudo adduser sammy`

Once you have this new account, you can switch over and connect to Postgres...
```
$ sudo -i -u sammy
$ psql
```
...or inline as follows.
```
$ sudo -u sammy psql
```

If you want your user to connect to a different database, you can specify the database like so:
`$ psql -d postgres`

Once logged in, you can check your currect connection information by typing:
`sammy=# \conninfo`

```
Output
You are connected to database "sammy" as user "sammy" via socket in "/var/run/postgresql" at port "5432"
```
