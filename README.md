# Installation of Postgres on AWS EC2 Instance

## Step 1: Update Package Lists
Run the following command to update the package lists on your instance:
```
sudo yum update
```

## Step 2: Install PostgreSQL
Use the package manager to install PostgreSQL:
```
sudo yum install postgresql postgresql-server
sudo postgresql-setup initdb
```

## Step 3: Start and enable the PostgreSQL service
Start the PostgreSQL service and enable it to start on boot:
```
sudo systemctl start postgresql
sudo systemctl enable postgresql
sudo systemctl status postgresql
```

## Step 4: Enable postgres database to listen for requests from outside
take a backup of the below file:
```
sudo cp /var/lib/pgsql/data/postgresql.conf /var/lib/pgsql/data/postgresql.conf.bak
```

modify the file to accept connections from anywhere:
```
sudo vi /var/lib/pgsql/data/postgresql.conf
```

* type /listen_addresses and press Enter to search for the listen address parameter
* use x to delete the #
* change the value of listen_addresses to '*'
* save and exit the file

## Step 5: Change the password of the postgres user and Login using Postgres system account
```
sudo passwd postgres
su - postgres
```

## Step 6: Change the database postgres password
```
psql -c "ALTER USER postgres WITH PASSWORD 'postgres';"
exit
```

## Step 7: Allow remote connections
modify the following file to allow remote connections:
```
sudo vi /var/lib/pgsql/data/pg_hba.conf
```
* navigate to 'IPV4 local connections' at the end of the file
* use x to delete the existing address and i to insert 0.0.0.0/0 as the new address
* use x to delete the existing method and i to insert md5 as the new method


## Step 8: Restart the database
```
sudo systemctl restart postgresql
```


