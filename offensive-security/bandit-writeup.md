# OverTheWire Bandit Walkthrough

## Objective
The Bandit wargame is designed to teach the basics of Linux, command-line usage, and fundamental security concepts through hands-on challenges.

## Levels Covered
Level 1 → Level 10

---

## Level 1 → Level 2

### Goal
Find the password for the next level.

### Approach
The file name started with a dash (-), which gets interpreted as an option by commands.

To fix this, I used `./` to clearly specify that it's a file in the current directory.

### Command Used

cat ./-filename


### Key Learning
- Files starting with `-` can be interpreted as command options
- Using `./` ensures the file is treated as a path

---

## Level 2 → Level 3

### Goal
Find the password for the next level.

### Approach
The file name had spaces along with special characters. To handle that, I used quotes along with `./` so the command treats the entire name as a single file.

### Command Used

cat "./filename with spaces"


### Key Learning
- File names with spaces must be handled using quotes or escaping
- Proper file referencing is important in Linux

---

## Level 3 → Level 4

### Goal
Find the password for the next level.

### Approach
The file was inside a directory named `inhere`. I changed into that directory and listed all files, including hidden ones, to find the correct file.

### Command Used

cd inhere
ls -a
cat .hiddenfile


### Key Learning
- Hidden files start with `.`
- `ls -a` is used to view hidden files

---

## Level 4 → Level 5

### Goal
Find the password for the next level.

### Approach
There were multiple files in the directory, but only one was human-readable. I used `cat *` to quickly read all files. I also realized a loop could be used, but `cat *` was simpler here.

### Command Used

cat *


### Key Learning
- Wildcards (`*`) can be used to access multiple files
- Efficient file scanning helps in enumeration

---

## Level 5 → Level 6

### Goal
Find the password for the next level.

### Approach
The file had specific conditions: human-readable, 1033 bytes in size, and not executable. I used the `find` command with filters to narrow it down.

### Command Used

find . -type f -size 1033c ! -executable


### Key Learning
- `find` is powerful for locating files with specific attributes
- File size and permissions can be used as filters

---

## Level 6 → Level 7

### Goal
Find the password for the next level.

### Approach
The file was somewhere on the server with specific ownership and size conditions. I used the `find` command again, this time filtering by user, group, and size.

### Command Used

find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null


### Key Learning
- Files can be filtered based on ownership and size
- Redirecting errors (`2>/dev/null`) helps clean output

---

## Level 7 → Level 8

### Goal
Find the password for the next level.

### Approach
The password was in `data.txt` next to the word "millionth". I used `grep` to search for that specific keyword.

### Command Used

grep "millionth" data.txt


### Key Learning
- `grep` is useful for searching specific patterns in files
- Helps quickly locate relevant data

---

## Level 8 → Level 9

### Goal
Find the password for the next level.

### Approach
The password was the only line that appeared once in the file. I first sorted the file and then used `uniq -u` to find the unique line.

### Command Used

sort data.txt | uniq -u


### Key Learning
- `sort` is often required before using `uniq`
- `uniq -u` shows unique lines

---

## Level 9 → Level 10

### Goal
Find the password for the next level.

### Approach
The password was hidden in a readable string among a lot of binary data, and it was preceded by "=" characters. I used `strings` to extract readable content and then filtered it using `grep`.

### Command Used

strings data.txt | grep "="


### Key Learning
- `strings` extracts readable text from binary files
- Combining commands using pipes is powerful

---

## Overall Learnings

- Basic Linux navigation and file handling
- Working with hidden files and special filenames
- Using commands like `find`, `grep`, `sort`, and `uniq`
- Understanding file permissions and ownership
- Combining commands using pipes for efficient analysis
