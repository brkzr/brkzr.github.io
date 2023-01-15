---
layout: note
title: "Linux CLI Tips"
date: 2023-01-15T12:00:00+00:00
tags: ["Linux","CLI"]
author: "brkzr"
description: Linux CLI Tips
---

# Linux CLI Tips
### Useful CLI Shortcus:

CTRL + L  Clear CLI Screen  
CTRL + C  SIGINT Signal Interrupt  
CTRL + D  ENDOFSTREAM Signal Interrupt  
CTRL + W  Delete Word  

---
### Little CLI Warm up 

```bash
pwd                     # print working directory

cd path                 # change working directory 
cd .                    # current folder  
cd ..                   # parent folder   
cd /                    # selected folder    
cd ~                    # home directory  

./my-proc               # run my-proc process

mkdir folderName        # create folder
touch file              # create file

echo "Hello" > fileName # Write Hello to file (> mean direction)
echo $?                 # exit code of last process
echo $PATH              # get path variable
echo output{01..12}.txt # echo multiple output file (output01.txt)
echo $(!!)              # echo last command

ls -lrt                             # content of directory
ls -lrt | wc -l                     # l = lines, c = bytes, w = words, m = characters
ls -lrt | awk '{print $9}'          # only 9. column
ls -lrt | awk '{print $9}' | uniq   # only 9. column with unique values

sudo chmod 600  fileName            # give permission to file
sudo chmod -R 755  fileName         # give permission to file and root files

ps aux | grep my-prog   # process status which process name is my-prog

kill -l                 # Signal List 
kill -INT <processID>   # terminate or signal a process (INT)
kill -KILL <processID>  # terminate or signal a process (KILL)

top                     # process viewer
htop                    # interactive process viewer
wc                      # print newline, word, and byte counts for each file (word count)
dd                      # convert and copy a file
hexdump
grep -E <regexExp>      # search string     
sed -E                  # powerful text stream editor -E = Extended 
printenv                # print environment variables

# text viewer 
cat fileName
more fileName 
less fileName

tail -10 fileName
head - 10 fileName
head -n 5 input.txt         # first 5 line of input.txt
tail -n 5 input.txt         # last 5 line of input.txt
tail -f log-file.txt        # -f = follow (tail not stop)
tail -f /dev/null           # unlimited listen :D 

## Terminal Arithmetic
echo $(( 3 + 5 )) # result is 8
expr 3 + 5        # result is 8 

# text editor
vi fileName
vim fileName
nano fileName
```

```bash
# Permissions (file type, user, group, other)
d rwx r-x r-x
- rw- r-- r--

N   Description                      ls   binary    
0   No permissions at all            ---  000
1   Only execute                     --x  001
2   Only write                       -w-  010
3   Write and execute                -wx  011
4   Only read                        r--  100
5   Read and execute                 r-x  101
6   Read and write                   rw-  110
7   Read, write, and execute         rwx  111

# File Types
-	Regular or ordinary file
d 	Directory file
l	Link file
b	Block special file
p	Named pipe file
c	Character special file
s	Socket file
```
---
### Redirection Commands. 

__>__     output redirection  
__<__     input redirection   
__>>__    append text to an existing file

---
###  File Descriptors (FD)
__Everything is a file (stream) in Linux !!!__    
__Every Unix process has the 3 standard file descriptor !!!__   

- 0  stdin (keyboard)
- 1  stdout (monitor / default)
- 2  stderr

```bash
./your-program < input.txt
./your-program < input.txt > output.txt
./your-program < input.txt 2> output.txt
./your-program < input.txt > output.txt 2>&1 # 2>&1 meaning is direct stdout to stdin 
```

## PART2 
---
```bash
# process detail files path (remember everthing is file)
cd /proc 
cd /proc/<processID>
cat environ ## process environments

# soft limit (exceed limit then log)  
# hard limit (exceed limit then kill)
cat limits 
```

 

```bash
# Adding a Directory to your $PATH
export PATH=$PATH:/directory/directory # correct way
export PATH=/directory/directory:$PATH # wrong  because it searches in the newly path first

cat /etc/enviroment
```
<pre>
# DEVICES
/dev/null       Reads from /dev/null always return end of file.
/dev/zero       Return bytes containing zero.
/dev/random     Random device
</pre>

```bash
ls -lrt > output_ls.txt     # write output to file
ls -lrt > /dev/null         # if result is important !!!
echo $?                     # write result to screen
```
```bash
curl -s www.google.com > /dev/null 2>&1 # only result is important
echo $?                                 # write result to screen
```

**find** search for files in a directory hierarchy
```bash
find . -name my-prog*
find . -type d  # d = directory, f = files, l symbolic link, c = character devices ...
find . -name *.txt | while read filename; do echo $filename; done  # write all txt to screen
```
**CURL**
```bash
curl https://demo.consul.io/v1/catalog/services?pretty
curl -s https://demo.consul.io/v1/catalog/service/web?pretty | jq '.[0].Address'
curl -s https://demo.consul.io/v1/catalog/service/web?pretty | jq '.[].Address'
curl -s https://demo.consul.io/v1/catalog/service/web?pretty | jq -r '.[].Address'

curl -s https://demo.consul.io/v1/catalog/service/web?pretty | jq -r '.[].Address' | whi
le read serverAddr; do curl -s $serverAddr > $serverAddr.txt; done
```

**dd** convert and copy a file
```bash
## dd  convert and copy a file
dd if=/dev/zero of=zero-file.txt bs=512 count=2
cat zero-file.txt
hexdump -v zero-file.txt

dd if=/dev/urandom of=random-file.txt bs=512 count=4
hexdump -v random-file.txt

zero devicedan null device a  sürekli kopyalama (result = cpu load)
dd if=/dev/zero of=/dev/null
```

**stress-ng** stress test libray
```bash
## 1 cpu %40 load
stress-ng -c 1 -l 40
htop
```

**cut vs awk**
- awk: pattern scanning and processing language
- cut - remove sections from each line of files
```bash

echo "john,doe,29,male" |cut -d, -f3
echo "john,doe,29,male" |cut -d, -f4,3
echo "john;doe;29;male" |cut -d\; -f4,3

echo "john,doe,29,male" | awk -F, '{print $3}'
echo "john,doe,29,male" | awk -F, '{print $1, $2 " is " $3 " years old." }'
```

**ifconfig**
```bash
ifconfig    #lo 127.0.0.1 = loopback interface
ifconfig en0 | head -5 | tail -1 | awk '{print ($2,$6)}'
```

**source**
```bash
# bash create a new child process for every process. with "source" command, new command runs with in main process !!! 
```