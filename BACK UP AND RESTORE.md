- In Ubuntu we have :
   - rsync - an open source tool that allows for fast and secure backups whether to a local or remote location.
   - duplicity - a tool that allows u to encrypt the backed up data by rsync.
  - deja dup - similar to duplicity but has a GUI.
```
Darkkight101@htb[/htb]$ rsync -av /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

- So this command will back up the entire directory ***/path/to/mydirectory*** to a remote host ***backup_server*** .
- ***archive*** ***-a*** is used to preserve the original attributes of the file such as timestamps, permissions etc.
- ***verbose -v***  is used to output a detailed progression of the rsync operation.
* * *
## RESTORING BACKED UP DATA 
```
Darkkight101@htb[/htb]$ rsync -av user@remote_host:/path/to/backup/directory /path/to/mydirectory

```

* * *
## ENCRYPTED RSYNC
- We use ssh to encrypt and protect our data while it is being transferred to a back up server.\

```
Darkkight101@htb[/htb]$ rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory


```

* * *
- We can also add options to customize our transfer eg compression and incremental backups.
- Full backups are where u back up the full, complete data set.
- Incremental backups are a backup strategy where we only save the data that has changed since the last backup

```
Darkkight101@htb[/htb]$ rsync -avz --backup --backup-dir=/path/to/backup/folder --delete /path/to/mydirectory user@backup_server:/path/to/backup/directory
```
- **--backup** adds incremental backups in the **/path/to/backup/directory** folder.
- **-v** compresses the file for faster transfer.
- **--delete** removes files from the remote host that are no longer in the source directory.
- 
  