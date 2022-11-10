# installing and using postgres

## -postgres
```
sudo apt-get update
sudo apt install postgresql postgresql-contrib
```

## check postgres version
```
psql --version
```

.
___

# work

## - Login as user postgres
```
sudo --login -u postgres
```

## hekp
```
psql --help
```


## - Open ..
```
psql
```

.

## List databases
```
\l
```

## Create database, user, and grant privileges 
```
CREATE DATABASE db_name;
CREATE USER youruser WITH ENCRYPTED PASSWORD ‘yourpass’;
GRANT ALL PRIVILEGES ON DATABASE <yourdbname> TO <youruser>;
```


## Drop database
```
DROP DATABASE <db_name>;
```

## Connect to database
```
\c <db_name>
```

.
____
## Show relations
```
\d
```

## Show table
```
\d <table_name>
```

..
---

## Ok, now you can use different sql quieres
