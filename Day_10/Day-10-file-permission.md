# Day 10 – File Permissions & File Operations Challenge

Today’s focus was mastering file creation, reading files, understanding Linux permissions, and modifying them correctly.

---

## ✅ Task 1: Create Files

### 1️⃣ Create an empty file
```
touch devops.txt
```
Explanation: Creates an empty file named devops.txt.

### 2️⃣ Create file with content
```
echo "These are my DevOps notes" > notes.txt
```
Explanation: Creates notes.txt and writes content into it.

### 3️⃣ Create a script file using vim
```
vim script.sh
```
Inside vim:
```
echo "Hello DevOps"
```
Explanation: Created a simple shell script file.

### 🔎 Verify File Creation
```
ls -l
```
Observation (Example Output):
```
-rw-r--r--  devops.txt
-rw-r--r--  notes.txt
-rw-r--r--  script.sh
```

Understanding Default Permissions:

Owner → Read & Write
Group → Read only
Others → Read only
No execute permission yet

## ✅ Task 2: Read Files
### 1️⃣ Read notes.txt
```
cat notes.txt
```
Explanation: Displays file content in terminal.

### 2️⃣ Open script in read-only mode
```
vim -R script.sh
```
Explanation: Opens file in read-only mode to prevent accidental editing.

### 3️⃣ View first 5 lines of /etc/passwd
```
head -n 5 /etc/passwd
```
Explanation: Displays the first 5 lines of the file.

### 4️⃣ View last 5 lines of /etc/passwd
```
tail -n 5 /etc/passwd
```
Explanation: Displays the last 5 lines of the file.

### ✅ Task 3: Understand Permissions

Permission format:

rwxrwxrwx
owner group others
Values:

r = 4
w = 2
x = 1

Check permissions:
```
ls -l devops.txt notes.txt script.sh
```
🔎 Current Permissions (Example)
```
-rw-r--r-- devops.txt
-rw-r--r-- notes.txt
-rw-r--r-- script.sh
```
Meaning:
Owner → Can read & write
Group → Can read only
Others → Can read only
No one can execute

## ✅ Task 4: Modify Permissions
### 1️⃣ Make script executable
```
chmod +x script.sh
```
Verify:
```
ls -l script.sh
```
Now permissions:
```
-rwxr-xr-x script.sh
```
Run script:
```
./script.sh
```
Output:
```
Hello DevOps
```
### 2️⃣ Make devops.txt read-only
```
chmod -w devops.txt
```
Verify:
```
ls -l devops.txt
```
Now:
```
-r--r--r-- devops.txt
```
### 3️⃣ Set notes.txt to 640
```
chmod 640 notes.txt
```
Verify:
```
ls -l notes.txt
```
Now:
```
-rw-r----- notes.txt
```
Meaning:

Owner → Read & Write

Group → Read only

Others → No permission

### 4️⃣ Create project directory with 755
```
mkdir project
chmod 755 project
```
Verify:
```
ls -ld project
```
Now:
```
drwxr-xr-x project
```
Meaning:

Owner → Full access
Group → Read & Execute
Others → Read & Execute

## ✅ Task 5: Test Permissions

### 1️⃣ Try writing to read-only file
```
echo "Test" >> devops.txt
```
Result: Permission denied
Reason: Write permission was removed.

### 2️⃣ Try executing file without execute permission
If execute permission is removed:
```
chmod -x script.sh
./script.sh
```
Result: Permission denied
Reason: Execute (x) permission is required to run scripts.

## What I Learned

Linux permissions are based on owner, group, and others.

Execute (x) permission is mandatory to run scripts.

Numeric permissions (755, 640) make permission management easier.

Always verify changes using ls -l before testing access.

Removing write permission prevents file modification.