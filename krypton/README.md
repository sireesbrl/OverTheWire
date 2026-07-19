# Krypton

## Prerequisites

Install the required tools:

```bash
sudo apt install sshpass hxtools
```

(Optional) Store each level's password in numbered files for easier login:

```bash
echo "password" > 1
echo "password" > 2
echo "password" > 3
...
```

---

## Level 0

### Decode the initial password

```bash
echo "S1JZUFRPTklTR1JFQVQ=" | base64 -d
```

Save the decoded password to file `1`.

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

The output is encoded with **ROT13**. Decode it using either:

- `rot13` (from `hxtools`)
- Any online ROT13 decoder

Save the decoded password to file `2`.

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

Comparing the plaintext and ciphertext shows the cipher uses **ROT12**.

### Decrypt the Password

```bash
cat /krypton/krypton2/krypton3 | tr '[M-ZA-L]' '[A-Z]'
```

The resulting plaintext is the password for the next level.

Save it to file `3`.

---

## Level 3

### Connect

```bash
sshpass -p "$(cat 3)" ssh krypton3@krypton.labs.overthewire.org -p 2231
```

### Solution

After performing frequency analysis, decrypt the ciphertext:

```bash
cat /krypton/krypton3/krypton4 | tr '[JDSQBKVIWGYUNCXMA]' '[THEAOWLVDNPSRIFUB]'
```

Save the decoded password to file `4`.

---

## Level 4

### Connect

```bash
sshpass -p "$(cat 4)" ssh krypton4@krypton.labs.overthewire.org -p 2231
cat /krypton/krypton4/krypton5
```

### Solution

Determine the Vigenère shifts at each position using frequency analysis to recover the key.

- Cipher: **Vigenère**
- Key: **FREKEY**

Decrypt the ciphertext using the recovered key to obtain the next password.

Save the password to file `5`.