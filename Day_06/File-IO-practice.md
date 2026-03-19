# Day 6 – Linux File Handling Basics (DevOps)

This guide covers the basics of creating, editing, viewing, and searching files in Linux.  
These skills are essential for managing logs, configs, and scripts in a DevOps workflow.

---

## 1. Create a File

```
touch day6.txt
```
**Explanation:**
Creates a new empty file called day6.txt.
If the file already exists, its timestamp is updated without changing content.

## 2. Write to a File (Overwrite)
```
echo "Today is Day 6/90 of my DevOps journey" > day6.txt
```
**Explanation:**
- > writes the output to the file.
- Existing content is overwritten, so use with caution if you don’t want to lose data.

## 3. Append to a File
```
echo "Linux file handling practice" >> day6.txt
```
**Explanation:**
- >> adds text to the end of the file.
- Previous content remains intact, making it ideal for logs or notes.

## 4. Write and Display Output Using tee
```
echo "Redirection is powerful" | tee -a day6.txt
```
**Explanation:**
- tee writes output to a file and displays it on the terminal.
- -a ensures the content is appended, not overwritten.

## 5. View File Content
```
cat day6.txt
```
**Explanation:**
- Displays the complete content of the file in the terminal.
- Useful for quickly checking file content without opening an editor.

## 6. Add Multiple Lines Using EOF
```
cat <<EOF >> day6.txt
cat reads full file
head reads top lines
tail reads bottom lines
These skills help in DevOps
EOF
```
**Explanation:**
- EOF lets you input multiple lines at once.
- Appends all lines to the file without needing multiple echo commands.

## 7. View Top Lines (head)
```
head day6.txt
```
```
head -n 2 day6.txt
```
**Explanation:**
- By default, shows the first 10 lines of a file.
- Use -n to specify how many top lines to display.

## 8. View Bottom Lines (tail)
```
tail -n 3 day6.txt
```
## Explanation:
- Displays the last 3 lines of a file.
- Useful for monitoring logs or recent changes without opening the full file.

## 9. Search Text Using grep
```
cat day6.txt | grep head
```
**Explanation:**
- Filters file content to show only lines containing the word head.
- grep is a powerful tool for quickly finding patterns in files or logs.

## Summary

- Creating files: touch
- Writing & appending: > overwrites, >> appends
- Viewing content: cat, head, tail
- Searching: grep
- Multi-line input: EOF with cat
- Display + write: tee -a