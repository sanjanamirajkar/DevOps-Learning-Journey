# Day 09 Challenge – Linux Users, Groups & Shared Directories

This task covers **creating users and groups**, managing group memberships, configuring shared directories, and testing access permissions like a DevOps engineer.

---

## Task 1: Create Users

Created four users with home directories:

- `tokyo`
- `berlin`
- `professor`
- `nairobi`

**Verification:** Checked `/etc/passwd` to confirm users exist and their home directories are created.

```
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m professor
sudo useradd -m nairobi
Set Passwords for Users:
```
```
sudo passwd tokyo
sudo passwd berlin
sudo passwd professor
sudo passwd nairobi
```
**Explanation:**
useradd -m creates a new user along with a home directory. passwd sets a secure password for the user.

## Task 2: Create Groups
Created groups for organizing users:

developers
admins
project-team
```
sudo groupadd developers
sudo groupadd admins
sudo groupadd project-team
```
**Explanation:**
Groups help manage permissions for multiple users at once. Each group represents a team or role.

## Task 3: Assign Users to Groups

Assignments:
tokyo → developers + project-team
berlin → developers + admins
professor → admins
nairobi → project-team
```
sudo usermod -aG developers tokyo
```
```
sudo usermod -aG developers,admins berlin
```
```
sudo usermod -aG admins professor
```
```
sudo usermod -aG project-team nairobi
```
```
sudo usermod -aG project-team tokyo
```
**Explanation:**
usermod -aG adds a user to one or more groups without removing existing group memberships.

Verification:
```
groups tokyo
groups berlin
groups professor
groups nairobi
```

## Task 4: Shared Directory – Development Project
Created a shared folder for developers:
```
sudo mkdir /opt/dev-project
```
```
sudo chgrp developers /opt/dev-project
```
```
sudo chmod 775 /opt/dev-project
```
**Explanation:**
chgrp changes the group ownership of the folder.
chmod 775 allows the owner and group full access, while others can only read/execute.
This ensures developers can collaborate securely.

**Test Write Access:**
```
su tokyo
touch /opt/dev-project/tokyo.txt
```
```
su berlin
touch /opt/dev-project/berlin.txt
```
**Verification:** Files created successfully by group members confirm correct permissions.

## Task 5: Team Workspace
Created another shared folder for the project-team:
```
sudo mkdir /opt/team-workspace
sudo chgrp project-team /opt/team-workspace
sudo chmod 775 /opt/team-workspace
```
**Explanation:**
Allows collaboration for the project team, with read/write/execute access for group members.

**Test Write Access:**
```
su nairobi
touch /opt/team-workspace/nairobi.txt
```
**Verification:** File created successfully, confirming workspace permissions.

## **Users & Groups Summary**
**Users:**

tokyo, berlin, professor, nairobi
**Groups:**

developers, admins, project-team

**Group Assignments:**

tokyo: developers, project-team
berlin: developers, admins
professor: admins
nairobi: project-team
Directories Created:

/opt/dev-project
Permissions: 775 (drwxrwxr-x)

/opt/team-workspace
Permissions: 775 (drwxrwxr-x)

## Key Learnings
Managing User Privileges via Groups:
Using groups (developers, admins, project-team) simplifies access control and avoids setting permissions individually for each user.

Shared Workspace Permissions (775):
775 allows Owner and Group full control while restricting Others to read/execute only, ensuring collaboration and security.

Changing Group Ownership:
chgrp is used to assign the correct group ownership, which is essential for collaborative directories.

Verification Workflow:
Always confirm your changes using groups and ls -ld. Testing file creation as group members ensures permissions are correctly applied.