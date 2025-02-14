# userlogin_issue
Troubleshooting a user login issue.

Project of troubleshooting
Issue: 
user x complain that he can login on servera.exemple.
His mention that when hes trying to connect to the system the server is close immediatly.

My approch of this for this problem.

Step-1: Duplicate the step to undestind the root cause.

ssh x@servera.exemple.com - The output the connection close immiadiatly.

Step-2: Verify when was last x login to the system.

lastlon -u x@servera ---> last longin was success.

Step-3: Verify setring of user x password.

getent passwd x  ----> I came cross the propriety of user x is innacurate with shell /bin/false this is the issue. Good!

Step-4: Changing user x shell from /bin/false to /bin/bash. 

chsh -s /bin/bash x

-----------------------------------
Journalctl log command for troubleshooting

Collecting Information from journaldBefore diving into the logs, ask the user who reported the issue if they have made any recent changes to the system.

particularly if they installed any new packages or modified configurations.
 
This help me narrow down potential causes.

Step-1: Gathering  information from user who report the issue to know
if the user has install new package on the system. 
Step-1: 

Checking the last boot log FROM journactl with store log in the in the memory.
journalctl --list-boots  To get an overview of the system’s boot history

journalctl -b To view logs from the most recent boot

jourlnactl -ef ---> You can also follow real-time logs

Journalctl _SYSTEMD_UNIT=sshd.service  If the issue is related to SSH or a specific service, filter the logs using the unit name

journalctl -p emerg..err  to capture errors and emergency logs, you can filter by priority levels (emergency, error, warning

journalctl --since "2025-02-14 8:30:00"   to check logs from a specific time frame

journaldctl --since "2025-02-13" --until "2025-02-14"  or for a date range:

This command allowed me to narrow down the logs to the relevant time frame where the issue occurred.

I was able to identify a specific application service that was failing, and after investigating further,

the issue was resolved by:

Reconfiguring and restarting the problematic service

Removing a conflicting package

Adjusting system configuration to allow successful login attempts

