# Krypton

## Prerequisites

Install the required tools:

```bash
sudo apt install sshpass
sudo apt install hxtools
```

(Optional) Store passwords in numbered files:

```bash
echo "password" > 1
echo "password" > 2
...
```

---

## Level 0

### Decode the initial password

```bash
echo S1JZUFRPTklTR1JFQVQ= | base64 -d
```

**Note:** Save the decoded password into file `1`.

---

## Level 1

### Connect

```bash
sshpass -p "$(cat 1)" ssh krypton1@krypton.labs.overthewire.org -p 2231
```

### Solution

```bash
cat /krypton/krypton1/krypton2
```

Decode the output using either:

- `rot13` (from **hxtools**)
- An online ROT13 decoder

**Note:** Save the decoded password into file `2`.

---

## Level 2

### Connect

```bash
sshpass -p "$(cat 2)" ssh krypton2@krypton.labs.overthewire.org -p 2231
```

### Setup

Create a temporary working directory and link the key file:

```bash
workdir=$(mktemp -d)
cd "$workdir"

ln -s /krypton/krypton2/keyfile.dat
chmod 777 .
```

### Determine the Caesar Shift

Encrypt a known plaintext:

```bash
 echo "ABCDEFGHIJKLMNOPQRSTUVWXYZ" > letters
 /krypton/krypton2/encrypt letters
```

The readable output reveals the key is **ROT12**.

### Decrypt the Password

Read the ciphertext:

```bash
cat /krypton/krypton2/krypton3 | tr [M-ZA-L] [A-Z]
```

The **ROT12** output is the password for the next level.

**Notes**

- Save the decrypted password into file `3`.
