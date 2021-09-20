# Two Factor Authentication for SSH on CentOS-8
  
``dnf install openssh-server``   
``dnf install qrencode-libs.x86_64``   
``yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm``   
``yum install google-authenticator``  
```google-authenticator```   
Scan the QR Code with your preffered authenticator app   
Backup secrets   

Edit:   
``nano /etc/pam.d/sshd``   

 Add the following lines to the bottom of the file   
 
``session   optional     pam_reauthorize.so prepare``   
``auth required pam_google_authenticator.so nullok``   
# Edit the SSH configuration file   
``nano /etc/ssh/sshd_config`` 

Search and change:   
``ChallengeResponseAuthentication yes``  
Restart sshd service   
``systemctl restart sshd.service``   

Logout and try to login again   
Enjoy
