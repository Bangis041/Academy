This machine is one of the first machines i got root access to. It was really fun and this is going to be like a walkthrough o it.
Advice to beginners just like me, I won't advise you follow this walkthrough back to back as it will really not help you progress well in your journey. You can just come here to check when you get stuck and have tried all possible things you know before.

First we load our machine and get our IP address. For that we use the command <ip a> and we copy our IP address. That will be the target IP. 


We start by doing the normal, scanning for ports to see which ports are opened and vulnerable. For this, I did <nmap -A -p- IP>

From the scan, we can see we had a number of opened ports. Port 21, 22 and 80. Port 21 looked interesting since it's the first and has a content we would like to view and also, anonymous FTP login allowed.
We go ahead to check out what ftp has for us. For that we use <ftp IP> and then we are able to list what files are there. FTP simply means file transfer protocol, it is used to download, upload, and transfer files from one location to another on the internet and between systems.
Here we downloaded the note.txt file using <get file-name> and then I viewed it on my attaker's machine. From the note.txt, we found out Grimmie was was a user and dev who uses same passwords everwhere hehe😂 and we also found an SQL database where we saw the student RegNo, passwords and all other things that can be used to login. It was also from 2020 and the message ws from jdelta.

After that we check outh the next port that might matter to us. SSH is not it so we move down to port 80.
Just paste the IP on your browser and check round for any useful information. After loading the website, there was no much information. we only knew what technology was behind it. Here we proceed to using a directory buster. I will be using gobuster in this instance. SYNTAX: <gobuster dir -u http://IP -w <wordlist>>.
Afer scanning we were able to get two directories. One interests me more and that is /academy. Why? Because I saw something that has to do with student in the note.txt file we saw from FTP. Now we search for http://IP/academy. After loading, we get to see a login page that requires us to use a REG NO and password. I did that and i got an error so i looked at the password again and realized it was not a password but a hash. Most students used weak passwords😂. I simply used https://crackstation.net to crack the password and it was "student" so i logged in and said to myself "I'm IN !!!" hehe


