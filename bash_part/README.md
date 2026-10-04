# Archive Management Toolbox

## Description

This folder contains 5 scripts for managing a working environment used to analyze backup archives potentially compromised by ransomware.

## File List

* `init-toolbox.sh`: Initializes the working environment
* `import-archive.sh`: Imports archives into the environment
* `ls-toolbox.sh`: Lists imported archives
* `check-archive.sh`: Analyzes an archive and detects suspicious files
* `restore-toolbox.sh`: Restores a corrupted environment

### Setup

```bash
# Make the scripts executable
chmod +x *.sh

# Initialize the environment
./init-toolbox.sh
```

## Usage

### 1. Initialization

```bash
./init-toolbox.sh
```

Creates the `.sh-toolbox` directory and the `archives` file.

### 2. Import Archives

```bash
# Import an archive
./import-archive.sh client1.tar.gz

# Import multiple archives
./import-archive.sh client1.tar.gz client2.tar.gz

# Force overwrite
./import-archive.sh -f client1.tar.gz
```

### 3. List Archives

```bash
./ls-toolbox.sh
```

Displays all imported archives along with their information.

### 4. Analyze an Archive

```bash
./check-archive.sh
```

* Selects an archive to analyze
* Temporarily extracts the archive
* Searches for the last admin login
* Identifies files modified after this login
* Searches for healthy versions in other archives

### 5. Restore the Environment

```bash
./restore-toolbox.sh
```

Automatically detects and fixes problems in the environment.

## Environment Structure

```text
bash_file/
├── init-toolbox.sh
├── import-archive.sh
├── ls-toolbox.sh
├── check-archive.sh
├── restore-toolbox.sh
└── .sh-toolbox/
    ├── archives
    ├── client1.tar.gz
    └── client2.tar.gz
```

## `archives` File Format

```text
3
client1.tar.gz:20251127-120000:
client2.tar.gz:20251128-130000:AES256_KEY
client3.tar.gz:20251129-140000:
```

Format:

```text
archive_name:import_date:decryption_key
```

## Typical Workflow

```bash
# 1. Initialize
./init-toolbox.sh

# 2. Import archives
./import-archive.sh client1.tar.gz client2.tar.gz

# 3. Verify imports
./ls-toolbox.sh

# 4. Analyze an archive
./check-archive.sh

# 5. Restore if necessary
./restore-toolbox.sh
```

## Bonus Features

* **import-archive.sh**: `-f` option to force overwriting, support for importing multiple files
* **ls-toolbox.sh**: Detects inconsistencies between the `archives` file and the actual archives
* **restore-toolbox.sh**: Automatically restores the working environment
* **check-archive.sh**: Searches for healthy versions in other archives
