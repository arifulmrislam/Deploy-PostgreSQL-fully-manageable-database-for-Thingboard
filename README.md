# Configure-PostgreSQL-ThingsBoard-database
```bash
ThingsBoard is able to use SQL or hybrid database approach
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
- Enter the backup folder
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
<img src= "ScreenShort1.png" width=800>

- Basically, we need `thingsboard.yml` and `thingsboard.conf` files.

- After the backup procedure, we need to stop the things board service.

## Configuration

- Service management commands:
```
sudo service postgresql stop
sudo service postgresql start
sudo service postgresql restart
```
- For check the status
```
$ sudo service thingsboard status
```

<img src= "ScreenShort2.png" width=800>





