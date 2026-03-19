# Day 12 Breather & Revision (Days 01–11)....

## My Goals and Plan Check....

- I revisited my Day 01 plan.

- My goal is still clear. build strong Linux + Git foundations before moving to advanced DevOps tools.

- I realized consistency matters more than speed.

- I will focus more on hands on repetition instead of just reading notes.

- Small tweak Spend 10 15 minutes daily revising old commands.

## Processes & Services Practice...

I run some commands from last days.
```
ps aux | head
systemctl status ssh
journalctl -u ssh --no-pager
```
Cmd Overview Explain:

ps aux shows running processes with CPU and memory usage.

systemctl status quickly tells whether a service is active, failed, or inactive.

journalctl -u <service> gives detailed logs for troubleshooting.

This helped me understand how to quickly check system health.

# File Skills Practice...

Practiced a few basic operations.
```
echo "Test line" >> demo.txt
chmod 744 demo.txt
ls -l demo.txt
cp demo.txt backup.txt
mkdir test-folder
```
## What I Run cmd more :..

- >> appends safely without overwriting.

- chmod 744 gives full access to owner, read only to others.

- ls -l helps verify permissions immediately.

## Cheat Sheet Refresh

From my earlier commands, the 5 I would use first during an issue:
```
ls -l #Check permissions quickly

ps aux #See running processes

systemctl status #Check service health

journalctl -u #Read service logs

chmod #Fix permission issues
```
These feel most practical in real troubleshooting.

## User & Group Practice

I recreated a small scenario:
```
sudo useradd testuser
sudo chown testuser demo.txt
id testuser
ls -l demo.txt
```
Explain cmd:

- 'id' confirms user and group.

- 'ls -l' confirms ownership change.

- This made ownership concepts clearer.

## Mini Self-Check
**1) Which 3 commands save the most time?**
```
ls -l #Instantly shows permissions and ownership.

systemctl status #Quick service health check.

ps aux #Helps find running processes fast.
```
**2) How do you check if a service is healthy?**

First commands I run:
```
systemctl status <service>
ps aux | grep <service>
journalctl -u <service>
```

**3) How to safely change ownership and permissions?**

Always verify before and after:
```
ls -l file.txt
sudo chown user:group file.txt
sudo chmod 644 file.txt
ls -l file.txt
```
Check twice before applying changes.

**4) Focus for next 3 days**

- I want to focus on networking now and complete Linux Cmd Deeply.

- Also I will practice users & group management.

- And if time allows I will also watch One-shot videos on youtube as will.

## Overall is.....

Revision builds confidence.

Core Linux commands are becoming more natural.

I feel more comfortable checking services and file permissions.