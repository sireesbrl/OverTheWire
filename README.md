# OverTheWire

## Prerequisites

Install the required tools:

```bash
sudo apt install sshpass
sudo apt install hxtools
```

(Optional) Store passwords in numbered files:

```bash
echo "password" > 0
echo "password" > 1
...
```

---

# Bandit

## Level 0

Connect:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Password:

```text
bandit0
```

Or use `sshpass`:

```bash
sshpass -p "$(cat 0)" ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Solution:

```bash
cat readme
```

---

## Level 1

Connect:

```bash
sshpass -p "$(cat 1)" ssh bandit1@bandit.labs.overthewire.org -p 2220
```

Solution:

```bash
cat ./-
```

---

## Level 2

Connect:

```bash
sshpass -p "$(cat 2)" ssh bandit2@bandit.labs.overthewire.org -p 2220
```

Solution:

```bash
cat ./--spaces\ in\ this\ filename--
```

---

## Level 3

Connect:

```bash
sshpass -p "$(cat 3)" ssh bandit3@bandit.labs.overthewire.org -p 2220
```

Solution:

```bash
cat inhere/...Hiding-From-You
```

---

## Level 4

Connect:

```bash
sshpass -p "$(cat 4)" ssh bandit4@bandit.labs.overthewire.org -p 2220
```

Commands:

```bash
cd inhere/

for i in $(ls); do
    file "./$i"
done

cat ./-file07
```

---

## Level 5

Connect:

```bash
sshpass -p "$(cat 5)" ssh bandit5@bandit.labs.overthewire.org -p 2220
```

Commands:

```bash
find . -readable -size 1033c

cat maybehere07/.file2
```

---

## Level 6

Connect:

```bash
sshpass -p "$(cat 6)" ssh bandit6@bandit.labs.overthewire.org -p 2220
```

Commands:

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null

cat /var/lib/dpkg/info/bandit7.password
```

**Note:** `2>/dev/null` redirects error messages to `/dev/null` (the Linux "black hole").

---

## Level 7

Connect:

```bash
sshpass -p "$(cat 7)" ssh bandit7@bandit.labs.overthewire.org -p 2220
```

Commands:

```bash
grep "millionth" data.txt
```

Useful:

```bash
wc -l data.txt
```

**Note:** `wc -l` counts the total number of lines.

---

## Level 8

Connect:

```bash
sshpass -p "$(cat 8)" ssh bandit8@bandit.labs.overthewire.org -p 2220
```

Commands:

```bash
sort data.txt | uniq -c | grep -v "10"
```

**Note:**

- `sort` sorts alphabetically.
- `uniq -c` counts consecutive duplicate lines.
- `grep -v` inverts the match.

---

## Level 9

Connect:

```bash
sshpass -p "$(cat 9)" ssh bandit9@bandit.labs.overthewire.org -p 2220
```

Commands:

```bash
strings data.txt | grep "="
```

Equivalent:

```bash
cat data.txt | strings | grep "="
```

---

## Level 10

Connect:

```bash
sshpass -p "$(cat 10)" ssh bandit10@bandit.labs.overthewire.org -p 2220
```

Solution:

```bash
base64 -d data.txt
```

---

## Level 11

Connect:

```bash
sshpass -p "$(cat 11)" ssh bandit11@bandit.labs.overthewire.org -p 2220
```

Solution:

```bash
cat data.txt | rot13
```

**Alternative:** Use an online ROT13 decoder if `hxtools` is unavailable.

---

## Level 12

Connect:

```bash
sshpass -p "$(cat 12)" ssh bandit12@bandit.labs.overthewire.org -p 2220
```

Commands:

```bash
xxd -r data.txt data

gunzip data.gz

bzip2 -d data.bz2

tar -xvf data
```

**Note:**

Use `file` to determine the file type.

```bash
file filename
```

Rename the file with the correct extension if necessary before extracting.

---

## Level 13

Connect:

```bash
sshpass -p "$(cat 13)" ssh bandit13@bandit.labs.overthewire.org -p 2220
```

Copy the private key:

```bash
sshpass -p "$(cat 13)" scp -P 2220 \
bandit13@bandit.labs.overthewire.org:~/sshkey.private .
```

Restrict permissions:

```bash
chmod 600 sshkey.private
```

Login using the key:

```bash
ssh -i sshkey.private \
bandit14@bandit.labs.overthewire.org \
-p 2220
```

Retrieve the password:

```bash
cat /etc/bandit_pass/bandit14
```

---

## Level 14

Connect:

```bash
sshpass -p "$(cat 14)" ssh bandit14@bandit.labs.overthewire.org -p 2220
```

Command:

```bash
nc localhost 30000
```

**Note:** Enter the current password when prompted.

---

## Level 15

Connect:

```bash
sshpass -p "$(cat 15)" ssh bandit15@bandit.labs.overthewire.org -p 2220
```

Command:

```bash
openssl s_client -connect localhost:30001
```

**Note:** Enter the current password after the TLS connection is established.

---

## Level 16

Connect:

```bash
sshpass -p "$(cat 16)" ssh bandit16@bandit.labs.overthewire.org -p 2220
```

Scan for open ports:

```bash
nmap localhost -p 31000-32000
```

Identify TLS services:

```bash
nmap localhost -p 31046,31518,31691,31790,31960 -sV -T4
```

Connect:

```bash
openssl s_client -connect localhost:31790
```

**Note:** Currently not working.