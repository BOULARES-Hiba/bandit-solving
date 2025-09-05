# Bandit Walkthrough

This repository contains a comprehensive walkthrough for solving the Bandit wargame hosted by OverTheWire. Bandit is designed to teach fundamental Linux command-line skills and security concepts through progressive challenges.

## Table of Contents
- [Overview](#overview)  
- [Prerequisites](#prerequisites)  
- [Level Solutions](#level-solutions)  
  - [Level 0 → 1](#level-0--1)  
  - [Level 1 → 2](#level-1--2)  
  - [Level 2 → 3](#level-2--3)  
  - [Level 3 → 4](#level-3--4)  
  - [Level 4 → 5](#level-4--5)  
  - [Level 5 → 6](#level-5--6)  
  - [Level 6 → 7](#level-6--7) 
  - [Level 7 → 8](#level-7--8)
  - [Level 8 → 9](#level-8--9)
  - [Level 9 → 10](#level-9--10)
  - [Level 10 → 11](#level-10--11)


## Overview

The Bandit wargame teaches essential Linux command-line skills through a series of levels where each solution provides the password for the next level. This walkthrough covers the foundational levels that introduce core concepts including file navigation, handling special characters, and using advanced search commands.

## Prerequisites

- Basic understanding of SSH connections
- Access to a terminal or SSH client
- Connection to bandit.labs.overthewire.org on port 2220

## Level Solutions

### Level 0 → 1

**Objective:** Find the password for the next level stored in a file called readme in the home directory.

**Commands:**
```bash
ls -al
cat readme
```

**Solution:** The `ls -al` command displays all files in the current directory with detailed information. The `cat readme` command outputs the contents of the readme file.

**Password:** `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

### Level 1 → 2

**Objective:** The password is stored in a file called `-` located in the home directory.

**Commands:**
```bash
ls -al
cat ./-
```

**Solution:** Files beginning with a dash require special handling since the shell interprets `-` as a command option. Using `./` before the filename explicitly references it as a file in the current directory.

**Password:** `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`

### Level 2 → 3

**Objective:** The password is stored in a file called `--spaces in this filename--` located in the home directory.

**Commands:**
```bash
pwd
cat "/home/bandit2/--spaces in this filename--"
```

**Solution:** Filenames containing spaces must be enclosed in quotes or escaped with backslashes to be properly interpreted by the shell.

**Password:** `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`

### Level 3 → 4

**Objective:** The password is stored in a hidden file in the inhere directory.

**Commands:**
```bash
ls -la
cd inhere
ls -la
cat "...Hiding-From-You"
```

**Solution:** Hidden files in Linux begin with a dot (.) and require the `-a` flag with `ls` to be visible. The file `...Hiding-From-You` is hidden and contains the password.

**Password:** `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`

### Level 4 → 5

**Objective:** The password is stored in the only human-readable file in the inhere directory.

**Commands:**
```bash
cd inhere
file ./*
cat -- "-file07"
```

**Solution:** The `file` command identifies file types. Most files contain binary data, but `-file07` contains ASCII text. The `--` parameter tells `cat` to treat everything following as filenames, preventing interpretation of the leading dash as an option.

**Password:** `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`

### Level 5 → 6

**Objective:** Find a file that is human-readable, 1033 bytes in size, and not executable.

**Commands:**
```bash
find . -type f -size 1033c ! -executable
```

**Solution:** The `find` command with multiple criteria locates files matching specific attributes. The `-type f` parameter specifies regular files, `-size 1033c` finds files exactly 1033 bytes, and `! -executable` excludes executable files.

**Password:** `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`

### Level 6 → 7

**Objective:** Find a file somewhere on the server with specific ownership and size properties.

**Commands:**
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
```

**Solution:** This search spans the entire filesystem (`/`) looking for files owned by user `bandit7` and group `bandit6` that are exactly 33 bytes. The `2>/dev/null` redirects error messages to prevent permission denied errors from cluttering the output.

**Password:** `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`


### Level 7 → 8

**Objective:** The password is stored in `data.txt` next to the word `"millionth"`.

**Commands:**
```bash
grep "millionth" data.txt
```

**Solution:** The `grep` command searches for text patterns within files. This command locates the line containing "millionth" and displays the entire line, which includes the password adjacent to the search term.

**Password:** `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`


### Level 8 → 9

**Objective:** The password is stored in data.txt and is the only line of text that occurs only once.
**Commands:**
```bash
 data.txt | uniq -u
```
**Solution:** The `sort` command arranges all lines alphabetically, then pipes the output to uniq -u, which displays only unique lines that appear exactly once. This combination identifies the single non-duplicate line containing the password.

**Password:**  `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`


### Level 9 → 10

**Objective:** The password is stored in data.txt in one of the few human-readable strings, preceded by several '=' characters.
**Commands:**
```bash 
strings data.txt | grep "===="
```
**Solution:** The `strings` command extracts printable character sequences from binary files. The output is piped to grep to filter for lines containing multiple equal signs, which helps identify the password among the human-readable strings.

**Password:** `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey`

### Level 10 → 11

**Objective:**  The password is stored in data.txt, which contains base64 encoded data.
**Commands:**
```bash 
base64 -d data.txt
```
**Solution:**  The `base64` command with the -d flag decodes base64-encoded content back to its original form. This reveals the plaintext password that was encoded in the data.txt file.

**Password:** `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`

### Level 11 → 12

**Objective:** The password for the next level is stored in the file data.txt, where all lowercase (a–z) and uppercase (A–Z) letters have been rotated by 13 positions (ROT13).

**Commands:**
```bash 
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

```
**Solution:**  The `tr` command translates characters. The sets 'A-Za-z' and 'N-ZA-Mn-za-m' shift each letter by 13 positions, effectively decoding ROT13. This reveals the plaintext password.

**Password:** `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`