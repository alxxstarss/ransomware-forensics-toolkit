# Archive Management Toolbox

## Description

This folder contains 5 scripts to manage a workspace for analyzing backup archives potentially compromised by ransomware.

## File List

- `init-toolbox.sh` : Initializes the workspace
- `import-archive.sh` : Imports archives into the workspace
- `ls-toolbox.sh` : Lists imported archives
- `check-archive.sh` : Analyzes an archive and detects suspicious files
- `restore-toolbox.sh` : Restores a corrupted workspace

### Steps
```bash
# Make the scripts executable
chmod +x *.sh

# Initialize the workspace
./init-toolbox.sh  Creates the .sh-toolbox folder and the archives file.

# Import a single archive
./import-archive.sh client1.tar.gz

# Import multiple archives
./import-archive.sh client1.tar.gz client2.tar.gz

# Force overwrite
./import-archive.sh -f client1.tar.gz

#Listing archives
./ls-toolbox.sh

#Analyzing an archive
./check-archive.sh

#Restoring the workspace
./restore-toolbox.sh

#Workspace Structure
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

#Archive File Format
3
client1.tar.gz:20251127-120000:
client2.tar.gz:20251128-130000:AES256_KEY
client3.tar.gz:20251129-140000:
Format : [archive_name:import_date:decryption_key]

#Typical Workflow
# 1. Initialize
./init-toolbox.sh

# 2. Import archives
./import-archive.sh client1.tar.gz client2.tar.gz

# 3. Verify imports
./ls-toolbox.sh

# 4. Analyze an archive
./check-archive.sh

# 5. Restore if there's an issue
./restore-toolbox.sh

#Bonus Features
# 1. import-archive.sh : -f option to force overwrite, multiple file import support

# 2. ls-toolbox.sh : Detection of inconsistencies between files and archives

# 3. restore-toolbox.sh : Automatic workspace restoration

# 4. check-archive.sh : Search for healthy versions in other archives
