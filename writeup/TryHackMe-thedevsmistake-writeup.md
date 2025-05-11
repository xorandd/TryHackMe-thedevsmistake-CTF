## Deploy machine

![deploy machine](images/1.png)

## Enumeration
By scanning open ports there are 3 open ports:
- FTP (21)
- SSH (22)
- HTTP (80)

![Nmap](images/2.png)

We can log in as Anonymous into FTP (no password required).

Downloaded file but here was nothing interesting (literally nothing)

![FTP](images/3.png)

Okay, now let's have a look at http site, there is deafult apache website but looking at source code we can see a hint:

![hin1](images/4.png)

Used `gobuster` to enumerate directories and found a new one

Inside that directory we got a possible username:

![gobuster1](images/5.png)

In that path we found possible username:

![james-username](images/6.png)

Since here wasn’t much else to look at I ran gobuster again on the new directory

![gobuster2](images/7.png)

This time only found an image, I downloaded it and used binwalk to extract any embedded files. It extracted a text file containing base64 encoded text, after decoding it we got a password

![james-password](images/8.png)

## User flag

Now we have everything to access ssh and capture user flag

![user-flag](images/9.png)

## Root flag

Found a cronjob running by root that runs every minute

![cronjob](images/10.png)

There is permission to edit the script running, so I added a reverse shell command to that script and started a listener waiting for the connection

![reverse-shell](images/11.png)

And finally

![root-flag](images/12.png)

