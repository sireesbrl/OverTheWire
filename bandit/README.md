# Bandit

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

## Level 0

### Connect

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

### Solution

```bash
cat readme
```

---

## Level 1

### Connect

```bash
sshpass -p "$(cat 1)" ssh bandit1@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
cat ./-
```

---

## Level 2

### Connect

```bash
sshpass -p "$(cat 2)" ssh bandit2@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
cat ./--spaces\ in\ this\ filename--
```

---

## Level 3

### Connect

```bash
sshpass -p "$(cat 3)" ssh bandit3@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
cat inhere/...Hiding-From-You
```

---

## Level 4

### Connect

```bash
sshpass -p "$(cat 4)" ssh bandit4@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
cd inhere/

for file in *; do
    file "./$file"
done

cat ./-file07
```

---

## Level 5

### Connect

```bash
sshpass -p "$(cat 5)" ssh bandit5@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
find . -readable -size 1033c

cat maybehere07/.file2
```

---

## Level 6

### Connect

```bash
sshpass -p "$(cat 6)" ssh bandit6@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null

cat /var/lib/dpkg/info/bandit7.password
```

**Note:** `2>/dev/null` redirects error messages to `/dev/null`.

---

## Level 7

### Connect

```bash
sshpass -p "$(cat 7)" ssh bandit7@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
grep "millionth" data.txt
```

Useful command:

```bash
wc -l data.txt
```

---

## Level 8

### Connect

```bash
sshpass -p "$(cat 8)" ssh bandit8@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
sort data.txt | uniq -c | grep -v "10"
```

**Explanation**

- `sort` sorts the lines alphabetically.
- `uniq -c` counts consecutive duplicate lines.
- `grep -v` inverts the match.

---

## Level 9

### Connect

```bash
sshpass -p "$(cat 9)" ssh bandit9@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
strings data.txt | grep "="
```

Equivalent:

```bash
cat data.txt | strings | grep "="
```

---

## Level 10

### Connect

```bash
sshpass -p "$(cat 10)" ssh bandit10@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
base64 -d data.txt
```

---

## Level 11

### Connect

```bash
sshpass -p "$(cat 11)" ssh bandit11@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
rot13 < data.txt
```

---

## Level 12

### Connect

```bash
sshpass -p "$(cat 12)" ssh bandit12@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
xxd -r data.txt data

gunzip data.gz

bzip2 -d data.bz2

tar -xvf data
```

Use the `file` command to determine the file type:

```bash
file filename
```

Rename the file with the appropriate extension before extracting it if necessary.

---

## Level 13

### Connect

```bash
sshpass -p "$(cat 13)" ssh bandit13@bandit.labs.overthewire.org -p 2220
```

### Copy the private key

```bash
sshpass -p "$(cat 13)" scp -P 2220 \
bandit13@bandit.labs.overthewire.org:~/sshkey.private .
```

### Restrict permissions

```bash
chmod 600 sshkey.private
```

### Login with the key

```bash
ssh -i sshkey.private \
bandit14@bandit.labs.overthewire.org \
-p 2220
```

### Retrieve the password

```bash
cat /etc/bandit_pass/bandit14
```

---

## Level 14

### Connect

```bash
sshpass -p "$(cat 14)" ssh bandit14@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
nc localhost 30000
```

Enter the current password when prompted.

---

## Level 15

### Connect

```bash
sshpass -p "$(cat 15)" ssh bandit15@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
openssl s_client -connect localhost:30001
```

Enter the current password after the TLS connection has been established.

---

## Level 16

### Connect

```bash
sshpass -p "$(cat 16)" ssh bandit16@bandit.labs.overthewire.org -p 2220
```

### Solution

Find the open ports:

```bash
nmap localhost -p 31000-32000
```

Identify the TLS service:

```bash
nmap localhost -p 31046,31518,31691,31790,31960 -sV -T4
```

#### Option 1: Interactive

```bash
openssl s_client -connect localhost:31790 -quiet
```

Paste the current password when prompted.

#### Option 2: Save the key directly

```bash
mkdir -p /tmp/srs

cat /etc/bandit_pass/bandit16 \
| openssl s_client -connect localhost:31790 -quiet \
> /tmp/srs/sshkey.private
```

Copy the key to your local machine:

```bash
sshpass -p "$(cat 16)" scp -P 2220 \
bandit16@bandit.labs.overthewire.org:/tmp/srs/sshkey.private .
```

Restrict permissions:

```bash
chmod 600 sshkey.private
```

Login using the key:

```bash
ssh -i sshkey.private \
bandit17@bandit.labs.overthewire.org \
-p 2220
```

**Note:** `openssl s_client` must be run with the `-quiet` option. Also verify the key using `head` and `tail`.

---

## Level 17

### Connect

```bash
sshpass -p "$(cat 17)" ssh bandit17@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
diff passwords.old passwords.new
```

Copy the new password.

---

## Level 18

### Connect

```bash
sshpass -p "$(cat 18)" ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```

Copy the password.

---

## Level 19

### Connect

```bash
sshpass -p "$(cat 19)" ssh bandit19@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

---

## Level 20

### Connect

```bash
sshpass -p "$(cat 20)" ssh bandit20@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
cat /etc/bandit_pass/bandit20 | nc -l -p 1234 &
./suconnect 1234
```

Copy the password.

---

## Level 21

### Connect

```bash
sshpass -p "$(cat 21)" ssh bandit21@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
cd /etc/cron.d

cat cronjob_bandit22
cat /usr/bin/cronjob_bandit22.sh
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

Copy the password.

---

## Level 22

### Connect

```bash
sshpass -p "$(cat 22)" ssh bandit22@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
cd /etc/cron.d

cat cronjob_bandit23
cat /usr/bin/cronjob_bandit23.sh

myname=bandit23

echo "I am user $myname" | md5sum | cut -d' ' -f1

cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

---

## Level 23

### Connect

```bash
sshpass -p "$(cat 23)" ssh bandit23@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
cat > /tmp/srs.sh <<'EOF'
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/pass
EOF

chmod 777 /tmp/srs.sh
cp /tmp/srs.sh /var/spool/bandit24/foo/
```

Wait about a minute, then:

```bash
cat /tmp/pass
```

---

## Level 24

### Connect

```bash
sshpass -p "$(cat 24)" ssh bandit24@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
password=$(cat /etc/bandit_pass/bandit24)

for i in $(seq -w 0 9999); do
    echo "$password $i"
done | nc localhost 30002
```

Copy the password after the brute-force attack succeeds.

---

## Level 25

### Connect

```bash
sshpass -p "$(cat 25)" ssh bandit25@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
scp -P 2220 \
bandit25@bandit.labs.overthewire.org:~/bandit26.sshkey .

grep '^bandit26:' /etc/passwd

cat /usr/bin/showtext
```

---

## Level 26

### Connect

```bash
ssh -i bandit26.sshkey \
bandit26@bandit.labs.overthewire.org \
-p 2220
```

### Solution

- Resize the terminal so that `more` pauses.
- Press `v` to open Vim.

Inside Vim:

```vim
:set shell=/bin/bash
:shell
```

Then:

```bash
cat /etc/bandit_pass/bandit26

./bandit27-do cat /etc/bandit_pass/bandit27
```

---

## Level 27

### Connect

```bash
git clone ssh://bandit27-git@bandit.labs.overthewire.org:2220/home/bandit27-git/repo
```

Enter the **bandit27** password.

```bash
cat repo/README
```

---

## Level 28

### Connect

```bash
git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
```

Enter the **bandit28** password.

```bash
git -C repo log -p
```

---

## Level 29

### Connect

```bash
git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo
```

Enter the **bandit29** password.

```bash
git -C repo branch -a
git -C repo switch dev
git -C repo log -p
```

---

## Level 30

### Connect

```bash
git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo
```

Enter the **bandit30** password.

```bash
git -C repo tag
git -C repo show secret
```

---

## Level 31

### Connect

```bash
git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo
```

Enter the **bandit31** password.

```bash
echo "May I come in?" > repo/key.txt

git -C repo add -f key.txt
git -C repo commit -m "Add key.txt"
git -C repo push
```

---

## Level 32

### Connect

```bash
sshpass -p "$(cat 32)" ssh bandit32@bandit.labs.overthewire.org -p 2220
```

### Solution

```bash
$0

whoami

cat /etc/bandit_pass/bandit33
```

Copy the password.
