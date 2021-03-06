# PyMirai - The Mirai Botnet Source Code in Python

# This is a ongoing project! Nothing is final!

This is my efforts of reverse-engineering the Mirai botnet source code into Python. It's been two years since the original launch of the botnet and since that time I have yet to see anyone attempt to completely reverse engineer it outside of making it modified in it's native C and Go programming languages.

My reasons for reversing it into Python is simple

1. To improve it's adaptability in countering cybersecurity measures (by out-adapting the efforts of software engineers)
2. To add the function of "modulettes" that can be installed to further expand the original source code's capabilities
3. To help propagate the increasing number of Mirai copycats and variants by giving it a better platform to code on (debatable I know, other candidates include Ruby on RAILS, Java, etc.)
4. To add alternatives to the original botnet's C2 platform, that is, a alternative to Google GoLang, such as a Django-hosted server or something connected to a interactive JQuery/REACT Front-End to make it more usable to the end-user

# Wishlist - Features to be implemented as a improvement

1. Native HTTPS, SSL Support and DNS Resolution
2. Ability to resolve Dynamic DNS Addresses instead of simple IPv4 public addresses, allowing reconfigurable VPS C2 servers to be deployed with different IP addresses that the malware can still reach
3. Automated phishing campaigns against victim's machine in an effort to capture administrator login credentials to the router/switch
4. Web GUI, analytics, metrics, warnings, integrated SIEM of a InsightIDR-like format
5. Support for 10,000-line wordlists instead of 20 Most Commonly Used Passwords
6. C2 Cyber-Threat Analysis Detection and Early Warning System. Parses your Apache/Nginx Access logs for suspicious requests from places like 'malware-hunter.shodan.io'. Immediately warns user via email to break down the server and scoot!

# As of right now a incomplete project

Because of that a notable amount of the code is still in it's native C language, with a hastily and sloppily put together Pythonic equivalent that may or may not work. But... and this is why I expect rollout of a workable PyMirai to be fairly speedy...

1. Python is based on C, in fact, your .pyc files are generated containing C code each time it is run
2. For every library and module in C, there is almost assuredly, a equivalent module in Python for example, <code>#include <sys/socket.h></code> versus <code>import socket</code> and <code> socket(AF_INET,SOCK_STREAM,0) </code> is the same as <code> socket.socket(socket.AF_INET, socket.SOCK_STREAM, 0)
3. The original author makes extensive use of the struct structure, commonly misinterpreted as "a Class", when in fact, it can mean something else entirely (like a list, dictionary, or list of methods)
4. In my experience, ctopy is a terrible converter of C code to Python. A immediate evaluation after running <code> ctopy < file.c > file.c.py</code> shows that...
		a. The app failed to convert #include to import modules
		b. The whitespace is completely ruined
		c. Functions are not properly being called or declared
		d. Methods are not properly being referred or utilized
		e. Modules often fail to automatically find a equivalent (for example, for the resolv module, we can make use of Python-DNS)
5. There is quite a bit of odd programming logic and methods by the original author of Mirai, however, we do know he wrote it fairly hastily and didn't even consider it himself to be grade A work, but it worked for him. 
6. I seek to rectify and implement my own improvements (for example, togglable wordlists auto-converted into bytecode instead of a standard static 20-word combo wordlist would be a good start)



Just because I cooked up together a Pythonic equivalent of the code, it is not reflective of my understanding of it and it may not work. Hence, the code must be revised and migrated into the higher-level programming environment of Python.

But thankfully, since Mirai is originally written in C, direct translation of the code into Python should be fairly painless.

# To Do List

1. Convert C-header files (.h extensions) into compatible Pythonic libraries or modules that can be imported and utilized
2. Convert all unknown functions into Pythonic equivalents
3. Closely investigate syntax of Python-equivalent modules (for example to proper use the htons method, we need to create a simple function that does socket.htons(string) and returns it
4. Readapt the file-descriptor method of opening files that the original botnet code was designed to do. Or consider keeping it for the sake of cross-platform compatibility (with pyinstaller, this version of Mirai would only work on Windows, Linux, and Mac, and no IoT devices)
5. Properly identify all classes, functions, methods, data structures. For example, the "struct" syntax, followed by multiple variables and arguments to be declared in C strongly implies that it is a class.
6. Solve the issue of being unable to (in Python 2.7) convert text into byte-arrays. Byte-arrays is the preferred method of format for transmitting credentials (brute-forcing) for the original Mirai bot
7. Replace the clumsy 20-word guessing queue with a more efficient and customizable wordlist of tens of thousands of credential attempts and simply read it into a list and iterate through it (the bot/worm carries this wordlist, which has a marginal impact on overall file size)
8. Replace all C libraries with Python module equivalents
9. Add first modulette: Auto-generate router-phishing pages. It has to copy the brand and logo of the router itself after identifying MAC addr vendor. The worm should spawn these phishing pages periodically and listen for a response (credentials entered) in order to pwn the router

# Notes

Scattered throughout the directories are a few README.md and NOTES.md files. These are just "journal entries" of my findings during the reverse engineering process. Also, it may contain helpful clues, such as how to use CTypes to directly call functions from the original code.

I wrote these notes to document the code so I can come back to it later if I need it.
