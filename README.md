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
``ChallengeResponseAuthentication no`` to ``yes``   
Restart sshd service   
``systemctl restart sshd.service``   

# Grant special access to bypass two factor 
Edit:   
`` nano /etc/security/access.conf``   
and add dependig on your case:   

Allow specific IP   
``+:ALL:192.160.1.1``   
Allow entire network   
``+:ALL:192.168.1.1/24``   
Allow specific user from secific IP   
``+:john:192.168.1.1``   

Add:   
``auth [success=1 default=ignore] pam_access.so accessfile=/etc/security/access.conf``  
in:
``/etc/pam.d/sshd``   
just above:   
``auth required pam_google_authenticator.so``

Logout and try to login again   
Enjoy
