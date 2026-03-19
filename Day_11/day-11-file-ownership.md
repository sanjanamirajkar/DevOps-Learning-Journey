# Day 11 – File Ownership Challenge (chown & chgrp)

Today’s goal was to understand Linux file ownership, modify owners and groups, and apply recursive ownership changes like a DevOps engineer.

---

## ✅ Task 1: Understanding Ownership

### Step 1: Check file ownership
```
ls -l
```
### Example Output:
```
-rw-r--r-- 1 ubuntu ubuntu  0 Feb 18 devops-file.txt
```
### Below are Format:
-rw-r--r-- 1 owner group size date filename

## 🔎 Difference Between Owner and Group

- Owner: The user who owns the file and has primary control over it.

- Group: A collection of users who share access permissions to the file.

Owner permissions apply to a single user, while group permissions apply to multiple users.


## ✅ Task 2: Basic chown Operations
### Step 1: Create file
```
touch devops-file.txt
```
### Step 2: Check current owner
```
ls -l devops-file.txt
```
### Step 3: Change owner to tokyo
```
sudo chown tokyo devops-file.txt
```
### Step 4: Change owner to berlin
```
sudo chown berlin devops-file.txt
```
### Step 5: Verify changes
```
ls -l devops-file.txt
```

### Explanation:
chown changes file ownership to another user. sudo is required because ownership modification needs administrative privileges.

## ✅ Task 3: Basic chgrp Operations
### Step 1: Create file
```
touch team-notes.txt
```
### Step 2: Check current group
```
ls -l team-notes.txt
```
### Step 3: Create group
```
sudo groupadd heist-team
```
### Step 4: Change file group
```
sudo chgrp heist-team team-notes.txt
```
### Step 5: Verify
```
ls -l team-notes.txt
```

### Explanation:
chgrp changes only the group ownership of a file.

## ✅ Task 4: Change Owner & Group Together
## Step 1: Create file
```
touch project-config.yaml
```
### Step 2: Change owner and group together
```
sudo chown professor:heist-team project-config.yaml
```
### Step 3: Create directory
```
mkdir app-logs
```
### Step 4: Change directory owner and group
```
sudo chown berlin:heist-team app-logs
```
### Verify
```
ls -l
```

### Explanation:
chown owner:group filename allows changing both user and group in one command.

## ✅ Task 5: Recursive Ownership
### Step 1: Create directory structure
```
mkdir -p heist-project/vault
mkdir -p heist-project/plans
touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```
### Step 2: Create group
```
sudo groupadd planners
```
### Step 3: Apply recursive ownership
```
sudo chown -R professor:planners heist-project/
```
### Step 4: Verify changes
```
ls -lR heist-project/
```

### Explanation:
The -R flag applies ownership changes to all files and subdirectories inside the main directory.

## ✅ Task 6: Practice Challenge
### Step 1: Create users (if not already created)
```
sudo useradd tokyo
sudo useradd berlin
sudo useradd nairobi
```

### Step 2: Create groups
```
sudo groupadd vault-team
sudo groupadd tech-team
```

### Step 3: Create directory
```
mkdir bank-heist
```
### Step 4: Create files
```
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

### Step 5: Set different ownership
```
sudo chown tokyo:vault-team bank-heist/access-codes.txt
sudo chown berlin:tech-team bank-heist/blueprints.pdf
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```
### Step 6: Verify
```
ls -l bank-heist/
```

### 📌 Files & Directories Created
devops-file.txt
team-notes.txt
project-config.yaml
app-logs/
heist-project/
bank-heist/

### 📌 Ownership Changes Summary (Example)
devops-file.txt → berlin
team-notes.txt → :heist-team
project-config.yaml → professor:heist-team
heist-project/ → professor:planners (recursive)
access-codes.txt → tokyo:vault-team
blueprints.pdf → berlin:tech-team
escape-plan.txt → nairobi:vault-team

### 📌 Commands Used
ls -l
chown
chgrp
chown -R
groupadd
useradd
mkdir
touch

### What I Learned

File ownership controls who manages and modifies files in Linux.

chown changes owner, chgrp changes group, and chown owner:group changes both.

Recursive ownership (-R) is essential for managing entire project directories.

Proper ownership is critical for DevOps tasks like deployments and shared workspaces.

Always verify ownership changes using ls -l.