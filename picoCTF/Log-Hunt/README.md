# picoCTF - Log Hunt

## Log

A **log** is a record file generated while a system or program is running.  
It is used to check **what happened, when it happened, and how it happened**.

### Uses
- **Problem tracking (Debugging)**
- **Security analysis** (who accessed the system and when)
- **System management** (server status, resource usage)
- **Audit** (can later be used as evidence)

### Components
- **Timestamp** (time)
- **Log level**
- **Message**

### Log Levels
- **DEBUG** : Detailed information for debugging  
- **INFO** : Information about normal operations  
- **WARN** : Potential problem situations  
- **ERROR** : An error has occurred  
- **FATAL** : A critical error where the program can no longer continue  

### Additional Characteristics
- Often stored as **text files**
- **Continuously appended**
- The same message may appear **multiple times**
- One event may be **split across multiple lines**

Commonly used tools in log analysis:
- grep
- sort
- uniq
- awk

---

## Problem Situation

It appears that part of the server logs has been leaked, and fragments of the flag are scattered throughout the log file, with some appearing repeatedly. Analyze the provided log file and reconstruct the original flag.

---

## Solution

### <GUI>
Using **Ctrl + F**, you can search for specific strings to find the hidden flag.

However, it is inefficient because repeated logs must be checked one by one.

### <CLI>
Use the **grep** command to extract parts of the log file containing specific strings. Since some logs appear repeatedly, removing duplicates reveals the correct flag.

grep flag server.log
grep flag server.log | awk '!seen[$0]++'
grep flag server.log | sort | uniq

---

## Answer
picoCTF{us3_y0urlinux_sk1lls_cedfa5fb}

---

Log analysis showed that filtering only the necessary information and removing duplicates is important.



