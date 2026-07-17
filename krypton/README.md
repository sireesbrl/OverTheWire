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
echo S1JZUFRPTklTR1JFQVQ= > 0
base64 -d 0
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
/krypton/krypton2/encrypt /etc/issue
cat ciphertext
```

Brute-force all possible Caesar shifts:

```bash
cipher="GNGZFGXFEZXNMOWQZPUZGEQSUNEAZ"
alphabet="ABCDEFGHIJKLMNOPQRSTUVWXYZ"

for i in {0..25}; do
    rotated="${alphabet:$i}${alphabet:0:$i}"
    printf "ROT%-2d %s\n" "$i" \
        "$(echo "$cipher" | tr "$rotated" "$alphabet")"
done
```

The readable output reveals the key is **ROT12**.

### Decrypt the Password

Read the ciphertext:

```bash
cat /krypton/krypton2/krypton3
```

Brute-force the ciphertext:

```bash
cipher="OMQEMDUEQMEK"
alphabet="ABCDEFGHIJKLMNOPQRSTUVWXYZ"

for i in {0..25}; do
    rotated="${alphabet:$i}${alphabet:0:$i}"
    printf "ROT%-2d %s\n" "$i" \
        "$(echo "$cipher" | tr "$rotated" "$alphabet")"
done
```

The **ROT12** output is the password for the next level.

**Notes**

- The password can also be decoded using a ROT12 decoder.
- In this writeup, the brute-force approach was used to verify the correct shift.
- Save the decrypted password into file `3`.
