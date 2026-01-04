# File Operations

## File Finding and Manipulation

### Find Commands

#### Count Files in Directory

```bash
find /home -type f | wc -l
```

#### Make All Shell Scripts Executable

```bash
find . -type f -name "*.sh" -exec chmod +x {} \;
```

#### Find and Move Files

```bash
find ~/.gf -type f -name "*.json" -exec mv {} ~/.gf \;
```

#### Remove Directories

```bash
find ~/.gf -mindepth 1 -type d -exec rm -rf {} +
```

### File Operations

#### Rename Directory

```bash
mv old_folder_name new_folder_name
```

#### Remove Indentation

```bash
sed -i 's/^[ \t]*//' filename
```

#### Remove Leading Spaces

```bash
sed 's/^[[:space:]]*//' input_script.sh > output_script.sh
```

## File Removal

### Remove Directory Contents

```bash
rm -rf /path/to/directory/*
```

### Remove All Files Including Hidden

```bash
rm -rf /path/to/directory/{*,.*}
```

## File Permissions

### Set File Permissions

```bash
chmod 400 ec2-key.pem
chmod 755 file.txt
```

### Permission Breakdown (755)

- **Owner**: Read + Write + Execute (7)
- **Group**: Read + Execute (5)
- **Others**: Read + Execute (5)

### Check File Ownership

```bash
ls -l /var/www/html
```

Example output:
```
-rw-r--r-- 1 root root 10671 Dec  9 11:36 index.html
```

- **Owner's Permissions**: rw- (read, write)
- **Group's Permissions**: r-- (read-only)
- **Others' Permissions**: r-- (read-only)

### Check Directory Ownership

```bash
ls -ld
```

## File Content Operations

### Append Content to Files

#### Using echo

```bash
echo 'NEW_VARIABLE=value' >> .env
```

#### Using cat

```bash
cat b.txt >> a.txt
```

### Write to Privileged Files

```bash
echo "abc" | sudo tee -a /etc/apache2/apache2.conf
```

### Remove Unused Packages

```bash
sudo apt autoremove -y
```

## File Compression

### Create Tar Archive

```bash
tar czf ../deploy.tar.gz .
```

### Create Zip Archive

```bash
sudo apt install zip
zip -r archive.zip folder_name/
```

## File Transfer

### Transfer Folder from Remote to Local

```bash
scp -i carlos_server.pem -r root@212.85.17.223:/root/rengine_backup /mnt/e/
```

### Transfer File from Local to Remote

```bash
scp -i "keypair.pem" ./article-db.articles.json ec2-user@ec2-3-7-69-212.ap-south-1.compute.amazonaws.com:/home/ec2-user/
```

## File Line Ending Conversion

### Convert DOS Line Endings to Unix

```bash
dos2unix id_rsa.pem
```

## Environment Variables in Files

### Variable Expansion Examples

```bash
# Standard variable reference
PROVIDER_ID="aws://${REGION}/${INSTANCE_ID}"
echo $PROVIDER_ID
# Output: aws://ap-south-1/123456

# With quoted suffix
PROVIDER_ID="aws://${REGION}/${INSTANCE_ID}\"spec\""
echo $PROVIDER_ID
# Output: aws://ap-south-1/123456"spec"

# With variable in suffix
PROVIDER_ID="aws://${REGION}/${INSTANCE_ID}\"${REGION}\""
echo $PROVIDER_ID
# Output: aws://ap-south-1/123456"ap-south-1"
```

### Variable Reference vs Command Substitution

- **$INSTANCE_ID**: Standard shell variable reference that accesses the stored value
- **$(INSTANCE_ID)**: Command substitution that tries to execute INSTANCE_ID as a command

## Environment Variables Management

### Set Environment Variable

```bash
export VARIABLE_NAME="value"
```

### Unset Environment Variable

```bash
unset VARIABLE_NAME
```

### View All Environment Variables

```bash
env
```
