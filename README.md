# Shell-Script-Project-Automated-Backup-System
Amazing project
Setup and Configuration:
Install rsync and SSH:
sudo apt update
sudo apt install rsync openssh-client openssh-server

Set Up SSH Key Authentication:
ssh-keygen -t rsa
ssh-copy-id user@remote_server

Script Development:
Define Variables:
#!/bin/bash
SOURCE_DIR="/path/to/source"
DEST_DIR="/path/to/destination"
REMOTE_USER="user"
REMOTE_HOST="remote_server"
REMOTE_DIR="/path/to/remote/backup"
LOG_FILE="/var/log/backup.log"

Write the Backup Script:
#!/bin/bash
rsync -avz --delete $SOURCE_DIR $REMOTE_USER@$REMOTE_HOST:$REMOTE_DIR >> $LOG_FILE 2>&1
if [ $? -eq 0 ]; then
    echo "Backup successful: $(date)" >> $LOG_FILE
else
    echo "Backup failed: $(date)" >> $LOG_FILE
fi

Scheduling Backups:
Configure cron Jobs:
crontab -e

Add the following line to schedule the backup script to run daily at 2 AM:
0 2 * * * /path/to/backup_script.sh

Testing and Monitoring:
Test the Script:
/path/to/backup_script.sh

Monitor Backups:
Check the log file for backup status:
tail -f /var/log/backup.log
