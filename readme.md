TryHackMe | Blue Writeup

Platform		: Kali Linux
Language		: English
Software used 	: Nmap 7.91
				  Metasploit v6.0.33-dev- 

This room is about Eternal Blue Exploit that has been discovered in 2017 and this exploit is used later by the cyber criminal to make WannaCrypt Ransomware

# Task 1 Recon

1. Scan the machine

`HINT`

2. How many ports are open with a port number under 1000?

` ¯\_(ツ)_/¯ `

3. What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)

` ¯\_(ツ)_/¯ `

# Task 2 Gain Access

`Hint` is enough, Im write this writeup as a guide not an answer. If you still confused, redo the [Metasploit room](https://tryhackme.com/room/rpmetasploit)

Dont know if this a fix, but IF you keep `fail` when running the exploit, try change `LHOST` to VPN IP connected to TryHackMe openvpn

# Task 3 Escalate

1. If you haven't already, background the previously gained shell (CTRL + Z). Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? (Exact path, similar to the exploit we previously selected) 

Either use (CTRL+Z) or for some reason by pressing (CTRL+Z) is also clossing metasploit, try to re-run exploit, `WIN`, and instead of (CTRL+Z) type `backgound`

Im using tips from [here](https://www.hackingarticles.in/command-shell-to-meterpreter/), IF you get stuck in message `[*] Stopping exploit/multi/handler` try to press `Enter` few times

2. Select this (use MODULE_PATH). Show options, what option are we required to change?

` ¯\_(ツ)_/¯ `

3. Set the required option, you may need to list all of the sessions to find your target here. 

` ¯\_(ツ)_/¯ `


4. Run! If this doesn't work, try completing the exploit from the previous task once more.

` ¯\_(ツ)_/¯ `

5. Once the meterpreter shell conversion completes, select that session for use.

` ¯\_(ツ)_/¯ `

6. Verify that we have escalated to NT AUTHORITY\SYSTEM. Run getsystem to confirm this. Feel free to open a dos shell via the command 'shell' and run 'whoami'. This should return that we are indeed system. Background this shell afterwards and select our meterpreter session for usage again. 

try type `shell` and type`whoami` once the terminal change to `C:\Windows\system32> `

7. List all of the processes running via the 'ps' command. Just because we are system doesn't mean our process is. Find a process towards the bottom of this list that is running at NT AUTHORITY\SYSTEM and write down the process id (far left column).


There are a lot of process running by user `NT AUTHORITY\SYSTEM`, pick one. I choose `spoolsv.exe`


8. Migrate to this process using the 'migrate PROCESS_ID' command where the process id is the one you just wrote down in the previous step. This may take several attempts, migrating processes is not very stable. If this fails, you may need to re-run the conversion process or reboot the machine and start once again. If this happens, try a different process next time. 


# Task 4 Cracking

1. Within our elevated meterpreter shell, run the command 'hashdump'. This will dump all of the passwords on the machine as long as we have the correct privileges to do so. What is the name of the non-default user? 


2. Copy this password hash to a file and research how to crack it. What is the cracked password?

The hash is consist of `NAME:NUMBER:1HASH:2HASH:::`. Use [Crackstation](https://crackstation.net/) to crack the password. Not found? Which Hash to pick? Try use each hash independently.

# Task 5 Find Flags!

1. Flag1? This flag can be found at the system root. 

In bash we use `cat` to print what in the file, in shell use `type`

2. Flag2? This flag can be found at the location where passwords are stored within Windows.


> Errata: Windows really doesn't like the location of this flag and can occasionally delete it. It may be necessary in some cases to terminate/restart the machine and rerun the exploit to find this flag. This relatively rare, however, it can happen. 


3. flag3? This flag can be found in an excellent location to loot. After all, Administrators usually have pretty interesting things saved. 

The answer for both number 2 and 3 can be found quickly if we can search file with name flag and formated in txt. Google `how to find files in windows terminal`