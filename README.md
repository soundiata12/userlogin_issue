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


