# 🐧 Ultimate Linux Cheat Sheet (CTF & Bash Master Edition)

## 📂 1. Navigation & System Exploration

|**Command**|**Definition**|**Hacker Use Case**|**Practical Example**|
|---|---|---|---|
|**`whoami`**|_Who am I_|Check your current privilege level or active user account.|`whoami`|
|**`pwd`**|_Print Working Directory_|Locate yourself on the system map. Outputs the absolute path.|`pwd`|
|**`ls`**|_List_|See visible files and folders inside your current directory.|`ls`|
|**`ls -la`**|_List Long All_|**Pro Tip:** Shows file permissions, sizes, owners, and hidden files (`.`).|`ls -la`|
|**`cd <folder>`**|_Change Directory_|Move inside a specific folder.|`cd operations`|
|**`cd ..`**|_Change Directory Back_|Go up one directory level (return to the parent folder).|`cd ..`|
|**`mkdir <name>`**|_Make Directory_|Create a brand new folder to organize your CTF evidence.|`mkdir evidence`|

## 📝 2. File Manipulation & Reading

|**Command**|**Definition**|**Hacker Use Case**|**Practical Example**|
|---|---|---|---|
|**`touch <file>`**|_Touch_|Creates an empty text file instantly.|`touch notes.txt`|
|**`cat <file>`**|_Concatenate_|Reads and outputs the entire content of a file to the terminal.|`cat secret.txt`|
|**`echo "<text>"`**|_Echo_|Prints text to the screen or pipes/redirects input data.|`echo "Hello World"`|
|**`rm <file>`**|_Remove_|Deletes a file permanently. **Warning:** There is no recycle bin!|`rm hint.txt`|
|**`rm -r <folder>`**|_Remove Recursive_|Deletes a folder along with everything inside it.|`rm -r operations`|

## ⚡ 3. Filtering & Data Analysis (Hacker Superpowers)

|**Command / Symbol**|**Name**|**Hacker Superpower**|**Practical Example**|
|---|---|---|---|
|**`grep "<word>"`**|_Global Regular Expression Print_|Finds a needle in a haystack. Filters lines matching a keyword.|`grep "CTF" server.log`|
|**`grep -i "<text>"`**|_Grep Ignore Case_|**Pro Tip:** Search for text ignoring uppercase/lowercase differences.|`grep -i "flag" log.txt`|
|**`wc -l`**|_Word Count Lines_|Counts how many lines are present in a text file or output.|`wc -l list.txt`|
|**`\|`**|_Pipe_|Connects the standard output of Command A into the input of Command B.|`cat log.txt \| grep "error"`|
|**`>`**|_Redirect_ (Overwrite)|Saves the command output into a new file, overwriting existing content.|`echo "data" > file.txt`|
|**`>>`**|_Append_|Appends text to the end of an existing file without deleting past data.|`echo "hint2" >> notes.txt`|

## 🌐 4. Networking & Connectivity (Reconnaissance)

|**Command**|**Definition**|**CTF / Pentesting Use Case**|**Practical Example**|
|---|---|---|---|
|**`ip a`** or **`ifconfig`**|_IP Address_|Discover your local IP address and active interfaces (e.g., VPN `tun0`).|`ip a`|
|**`ping -c 3 <IP>`**|_Packet Internet Groper_|Check if the target machine is active. `-c 3` sends exactly 3 packets.|`ping -c 3 10.10.10.5`|
|**`curl <URL>`**|_Client URL_|Interact with web servers from the CLI. Fetches raw HTML source code.|`curl http://target.local`|
|**`wget <URL>`**|_Web Get_|Download scripts, tools, or exploits directly from the web or your server.|`wget http://site.com/exploit.py`|
|**`ss -tuln`** or **`netstat -tuln`**|_Socket Statistics_|**Crucial Command:** Lists all open ports (TCP/UDP) listening on the machine.|`ss -tuln`|

## ⚙️ 5. Process Control & System Check (Post-Exploitation)

|**Command**|**Definition**|**Hacker Superpower**|**Practical Example**|
|---|---|---|---|
|**`uname -a`**|_Unix Name_|Prints exact Linux Kernel details. (Critical for choosing Privilege Escalation exploits).|`uname -a`|
|**`ps aux`**|_Process Status_|Displays a snapshot of every running process on the system.|`ps aux`|
|**`ps aux \| grep "python"`**|_Process Filtering_|**Pro Tip:** Look for hidden Python scripts running in the background.|`ps aux \| grep "python"`|
|**`top`** or **`htop`**|_Table of Processes_|Interactive, real-time task manager. Press `q` to exit.|`htop`|
|**`kill -9 <PID>`**|_Kill Process_|Forcefully terminates a specific process using its Process ID (`PID`).|`kill -9 1234`|

## 🛠️ 6. Permissions Management

| **Command**           | **Action**              | **When to use it?**                                                    | **Practical Example** |
| --------------------- | ----------------------- | ---------------------------------------------------------------------- | --------------------- |
| **`chmod +x <file>`** | _Change Mode + Execute_ | Grants execution permissions to a script or file.                      | `chmod +x exploit.py` |
| **`./<program>`**     | _Execute Current_       | Runs an executable script located inside your current folder.          | `./exploit.py`        |
| **`sudo <command>`**  | _SuperUser Do_          | Runs a command with administrative/root privileges. Requires password. | `sudo apt update`     |
 