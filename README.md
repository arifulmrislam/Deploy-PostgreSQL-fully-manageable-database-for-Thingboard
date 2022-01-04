# Configure-PostgreSQL-ThingsBoard-database
```bash
ThingsBoard is able to use SQL or hybrid database approach
```
- After Installing Thingsboard PE on Ubuntu, What is necessary to backup the whole machine or only database?

- After installation the thingsboard on our machine we can log thingsboard service.
```
$ less /var/log/thingsboard/thingsboard.log
```
- After that press `Ctrl+n` to view the latest input and check it.

# Backup Database

```
Make a backup of the database.
```

- Create backup folder
```
$ mkdir backup
```
- Enter the backup folder
```
$ cd backup
```
- Now, we will copy everythings to the current folder.
```
$ sudo cp /etc/thingsboard/conf/* ./
```
`*asterisk` means we copy everythings.

- To view the copy file
```
$ ll 
```
<img src= "ScreenShort1.png" width=800>
