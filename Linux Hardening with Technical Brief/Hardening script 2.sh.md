

\#\!/bin/bash

\# Variable for the report output file, choose a **NEW** output file name  
REPORT\_FILE="**bcs2\_project1.txt**" 

\# Output the sshd configuration file  
echo "Gathering details from sshd configuration file"  
\# Placeholder for command to get the sshd configuration file

echo "sshd configuration file:$(**cat /etc/ssh/sshd**)" \>\> $REPORT\_FILE  
printf "\\n" \>\> $REPORT\_FILE

\# Update packages and services  
Echo “Updating packages and services”

\# Placeholder for command to update packages

**sudo apt update**

\# Placeholder for command to upgrade packages

**sudo apt upgrade \-y**

echo "Packages have been updated and upgraded" \>\> $REPORT\_FILE  
printf "\\n" \>\> $REPORT\_FILE

\# Placeholder for command to list all installed packages

echo "Installed Packages:$(**apt list \--installed**)" \>\> $REPORT\_FILE  
printf "\\n" \>\> $REPORT\_FILE

echo “Printing out logging configuration data”

\# Placeholder for command to display logging data

echo "journald.conf file data: $(**cat /etc/systemd/journald.conf**)" \>\> $REPORT\_FILE  
printf "\\n" \>\> $REPORT\_FILE

\# Placeholder for command to display logrotate data

echo "logrotate.conf file data:$(**cat /etc/logrotate.conf**)" \>\> $REPORT\_FILE  
printf "\\n" \>\> $REPORT\_FILE

echo "Script execution completed. Check $REPORT\_FILE for details."

