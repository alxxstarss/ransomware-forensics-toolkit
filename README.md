# Ransomware Forensics & Recovery Toolkit

A comprehensive cybersecurity suite developed for post-incident investigation and data recovery after a ransomware attack. This repository contains both the **Bash management environment** and the **C cryptanalysis tools** created as part of an academic project.

---

## Repository Structure

```text
.
├── bash_part/            # Part 1: Automated environment & archive management
│   ├── init-toolbox.sh   # Environment initialization
│   ├── import-archive.sh # Safe archive ingestion
│   ├── ls-toolbox.sh     # Environment integrity check
│   ├── check-archive.sh  # Forensic log analysis & file detection
│   └── restore-toolbox.sh#  Auto-repair of corrupted environments
│
└── c_part/               # Part 2: Cryptanalysis & Vigenère cipher engine
    ├── cipher.c          # Encrypts base64 files using Vigenère
    ├── decipher.c        # Decrypts base64 files using a known key
    ├── findkey.c         # Known-plaintext key extraction
    ├── tools.c / tools.h # Shared cryptographic library
    ├── libcrypto.a       # Static library build
    └── Makefile          # Build automation
