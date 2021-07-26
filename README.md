# DDNS functionality for Hover domains
======================================

This is a fork of a previous project that aims to remove the unnecessary cruft
for those who want it to *just work*.

Most of the instructions below are edited from
[the original](https://github.com/texasaggie97/hover-dns-updater/).


About
=====
The Hover dns updater will update the Hover DNS entries for one or more
DNS records based on the external IP address. This can occur one time or run
continuously, checking after a certain amount of time, using systemd.


Installation
============

Prerequisites:
--------------
- [Python 3](https://www.python.org/downloads/)
- pip3: ```sudo apt-get install -y python3-pip```
  - requests: ```sudo pip3 install --upgrade requests```

Hover DNS IDs:
--------------
- Login to [Hover.com](https://hover.com)
- In the same browser go to
  https://www.hover.com/api/domains/YOURDOMAIN.COM/dns - replacing
  YOURDOMAIN.COM with the domain you want to update
- This will return a json file containing a list of ```entries```
- Look for the DNS records you want to keep up to date and make a note of the
  associated ```id```s (```dns1234567```)

Install Service:
-----------------------
- Copy ```INSTALL.sh```, ```hover-dns-updater.service```,
  and ```hover-dns-updater.py``` to a directory on your system
- Run ```./INSTALL.sh```
  - This will install and enable (but not start), the hover-dns-updater service
- Run ```sudo nano /etc/hover-dns-updater/hover-dns-updater.json```
  (or replace ```nano``` with the editor of your choice)
  - Fill in your hover username and password
  - Add the dns ids you noted above
  - Optionally: enter a log file name
  - Optionally: change the poll time, in seconds (default 10 minutes)

- After the configuration file is updated, start the service
  with ```sudo service hover-dns-updater start```
- Optionally: verify the service started correctly
  with ```sudo service hover-dns-updater status```


License
=======

**hover-dns-updater** is licensed under an GPL-style license ([see
LICENSE](https://github.com/texasaggie97/hover-dns-updater/blob/master/LICENSE)).
Other incorporated projects may be licensed under different licenses.
