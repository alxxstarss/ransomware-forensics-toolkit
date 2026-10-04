# Encryption/Decryption - Vigenère Cipher

## Description

This folder contains 3 programs for handling files encrypted using the Vigenère cipher on Base64-encoded data. These tools are designed to analyze and recover files compromised during an attack.

## Technical Context

### Encryption Process

An encrypted file undergoes the following transformations:

1. Base64 encoding (using the `base64` command)
2. Encryption using the Vigenère cipher with a Base64-encoded key
3. Base64 decoding (optional, depending on usage)

## Project Structure

```text
projet-partieC/
 cipher.c          # Encryption program
 decipher.c        # Decryption program
 findkey.c         # Key recovery program
 tools.c           # Shared library
 tools.h           # Function headers
 Makefile          # Build automation
 README.md         # This file
```

## Installation

### Requirements

* GCC compiler
* Make
* Linux or macOS system

### Compilation

#### Using Makefile

```bash
# Compile all programs
make

# Compile a single program
make cipher
make decipher
make findkey

# Clean compiled files
make clean
```

## Usage

### 1. cipher Program - Encrypt a File

**Purpose:** Encrypts a Base64-encoded file using a provided key.

**Syntax:**

```bash
./cipher  clé_base64 fichier
```

### 2. decipher Program - Decrypt a File

**Purpose:** Decrypts a file encrypted with a known key.

**Syntax:**

```bash
./decipher clé_base64 fichier_chiffré
```

### 3. findkey Program - Recover the Key

**Purpose:** Compares a plaintext file with its encrypted version to recover the key that was used.

**Syntax:**

```bash
./findkey fichier_clair fichier_chiffré
```

## Post-Attack Recovery Workflow

### Scenario

You have:

* An archive containing healthy files (before the attack)
* An archive containing encrypted files (after the attack)
* The encryption key is unknown

### Recovery Steps

#### Step 1: Extract the Files

```bash
# Extract a healthy file from an archive
tar -xzf client1-sauvegarde.tar.gz data/rapport.txt
mv data/rapport.txt rapport_sain.txt

# Extract the same encrypted file
tar -xzf client2-compromis.tar.gz data/rapport.txt
mv data/rapport.txt rapport_chiffre.txt
```

#### Step 2: Encode the Files in Base64

```bash
# Encode the healthy file
base64 rapport_sain.txt > rapport_sain_b64.txt

# Encode the encrypted file
base64 rapport_chiffre.txt > rapport_chiffre_b64.txt
```

#### Step 3: Recover the Key

```bash
./findkey rapport_sain_b64.txt rapport_chiffre_b64.txt
```

**Result:**

```text
the recovered key is Q2xlU0FFMjAyNQ==
```

#### Step 4: Decrypt All Files

Now that we have the key, we can decrypt all compromised files.

```bash
# For each encrypted file
base64 fichier_chiffre.txt > fichier_chiffre_b64.txt
./decipher Q2xlU0FFMjAyNQ== fichier_chiffre_b64.txt
base64 -d fichier_chiffre_b64.txt > fichier_restaure.txt
```

All files are now restored.

## Important Notes

### Base64 Encoding Required

Files must be Base64-encoded before using these programs.

```bash
# Incorrect
./cipher CLE fichier.txt

# Correct
base64 fichier.txt > fichier_b64.txt
./cipher CLE fichier_b64.txt
```

### Base64-Encoded Key

The provided key must also be Base64-encoded.

```bash
# To obtain a Base64-encoded key
echo -n "SAE2025" | base64
# Result: U0FFMjAyNQ==
```
