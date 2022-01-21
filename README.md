# Configure-PostgreSQL-ThingsBoard-database

I installed things board community version in `Dell Server` locally and use `PostgreSQL` database.
In working period I generate some question and try to make a note for future understanding.

```bash
ThingsBoard is able to use SQL or hybrid database approach.
```
- After Installing the Thingsboard PE on Ubuntu machine: What is necessary to back up the whole machine or only the database?

- After installation the thingsboard on our `Ubuntu-machine` we can log thingsboard service.
```
$ less /var/log/thingsboard/thingsboard.log
```
- After that press `Ctrl+n` to view the latest input and check it.

## Backup Database
```
Make a backup folder for the database.
```
- Create a backup folder
```
$ mkdir backup
```
- Enter the backup folder.
```
$ cd backup
```
- Now, we can copy everything to the current folder.
```
$ sudo cp /etc/thingsboard/conf/* ./
```
By `*asterisk` we can copy everything from previous folder to the new folder.

- To check the copy file
```
$ ll 
```
<img src= "ScreenShort01.png" width=800>

- Basically, we need `thingsboard.yml` and `thingsboard.conf` files.

- After the backup procedure, we need to stop the things board service.

## Configuration

- Service management commands:
```
sudo service postgresql stop
sudo service postgresql start
sudo service postgresql restart
```
- To check the status
```
$ sudo service thingsboard status
```

<img src= "ScreenShort02.png" width=800>

- Enter the database to check the free space of database.

- Use `psql-console` to enter the database
```
$ psql -U postgres -h localhost
```
- Now we will get the details of database.
```
\l+
```

<img src= "ScreenShort03.png" width=1000>

- check the disk space, logout from database and write this command.
```
$ df -h /
```
- Make sure we have enough space to place a backup of the database
`Check database size`
```
$ sudo -u postgres psql -c "SELECT pg_size_pretty( pg_database_size('thingsboard') );"
```

- Make sure our PostgreSQL database is running
```
$ pg_lsclusters
```
- If there is enough free space - make a backup.
```
$ pg_dump -U postgres -h localhost -d thingsboard > "specify the file"
```
- Enter the password of `postgres` not our machine.

- Finally, we can check the backup file which is created.
```
$ ll -h  
```
- Restore the folder for any trouble
```
$ pg_restore -U thingsboard -h localhost -d thingsboard > "File name"
```

- To copy the config file
```
$ cd /etc/thingsboard/conf
$ ll
$ sudo mv thingsboard.yml thingsboard.yml.invalid
$ sudo cp ~/backup/thingsboard.yml ./
```

- Now we can see the copy folder
```
$ ll
```
<img src= "ScreenShort4.png" width=800>

- After finishing the backup processing, to start the thingsoard service.
```
$ sudo service thingsboard start
```
## Midnight Commander

- We can use `midnight commander` compare between our things board files and our backup files. 
```
$ sudo mc
```

## File Storage
- Where are located the files with the application, like configuration files, rule chain, widget and dashboard so on?
- ThingsBoard has ability to store binary content (files) in the DataBase. Currently it is used to store report files generated by Generate Report Node. 
  Stored files are accessed by Send Email Node to create email attachments. Another way to send a file is the REST API Call Node. 
  User can access stored files using Files or Reports widgets which is part of Files Widgets Bundle.

- Enter the thingsboard config file
```
$ cd /etc/thingsboard/conf
$ ll
```
- To check the user share file of thingsboard and look what we have here
```
$ cd /usr/share/thingsboard
$ ll
```

- Enter the "bin" folder
```
$ cd bin
$ ll
```

<img src= "ScreenShort10.png" width=800>


<img src= "ScreenShort11.png" width=800>


- Basically it's executable and some instance and installed data etc. We have config file where we will see `data` folder and here we can see the certificate and some third       party related data.
 
- Enter the extension folder, which is use for custom developed role node like rule chains.
```
$ cd extensiions/
$ ll
```
<img src= "ScreenShort5.png" width=800>

## Clean Database

- How to clean a Database? Or How to purge all data older a specific date, like keep only the last six months data?
- To remove previous data from our database, we can use `PSQL console or Swagger`. Both have some [recommendable commands](https://www.postgresqltutorial.com/postgresql-cheat-sheet/).

## `PSQL console`

- First, open psql console and connect to thingsboard.
- Enter the password of the database and connect with thingsboard. 
```
\c thingsboard
```
- To see all tables,
```
\dt+
```
- And describe time-series,
```
\d ts_kv
select * from ts_kv limit 5;
```
<img src= "ScreenShort7.png" width=800>

- By [epoch time converter](https://www.epochconverter.com/), we can figure out the time and date. We can delete the data at our specific date.

<img src= "ScreenShort8.png" width=800>

`Key: We should make a backup file for the database and stop the thingsboard service before work.`

## `Swagger-ui`

- Use a brower to login the thingsboard [swagger service](http://localhost/swagger-ui/).
- Automatically it will open a pop-up and ask authorizations.

<img src= "ScreenShort6.png" width=800>

- Use bearer token: bearer <past your account token>

  `Key: We don't need to stop thingsboard service because swagger try to communicate with thingsboard server.`
 
## `Clean events`
  
- If we want to clean our role chains, we can clean "events" from database table. 
 ``` 
$ psql -U postgres -h localhost
```  
```  
\c thingsboard
\dt+
```  
<img src= "ScreenShort9.png" width=800> 
   

🚩 Connect with me on social
- LinkedIn: [LinkedIn](https://www.linkedin.com/in/ariful-islam-arif-2987b51a3/)
- Twitter: [Twitter](https://twitter.com/arifulislam301)
- Instagram: [Instagram](https://www.instagram.com/ariful_mr_islam/)

🔔 Subscribe to my YouTube channel: [YouTube](https://www.youtube.com/channel/UCED68cm6nHaAlAk0h9I3yAQ)

