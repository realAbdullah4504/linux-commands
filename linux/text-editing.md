# Text Editing

## Nano Editor

### Nano Shortcuts

#### Navigation

- `Alt + /` - Go to bottom of file
- `Alt + \` - Go to top of file
- `Alt + g` - Go to specific line number
- `Ctrl + y` - Page up
- `Ctrl + v` - Page down

#### Text Manipulation

- `Alt + k` - Mark text
- `Ctrl + w` - Search text
- `Alt + r` - Find and replace
- `Ctrl + d` - Delete text

#### Cursor Movement

- `Ctrl + a` - Move cursor to start of line
- `Ctrl + e` - Move cursor to end of line
- `Alt + <` - Move cursor back fast
- `Alt + >` - Move cursor forward fast

#### Text Deletion

- `Ctrl + u` - Delete everything before cursor
- `Ctrl + k` - Delete everything after cursor
- `Alt + backspace` - Remove text fast (like tab)

#### Advanced Features

- `Ctrl + x + e` - Open text in editor to modify command

## Sed Commands

### Basic Text Replacement

```bash
# Replace text in file
sudo sed -i 's#dbPath: /var/lib/mongo#dbPath: /data/mongodb#' /etc/mongod.conf

# Replace paths in files
sudo sed - 's#/var/log/good#/data/good#' ./test.txt

# Remove indentation
sed 's/^[[:space:]]*//' input_script.sh > output_script.sh

# Remove leading spaces and tabs
sed -i 's/^[ \t]*//' filename
```

### Advanced Sed Operations

```bash
# Delete lines matching pattern
sed -i '/pattern/d' filename

# Insert text at line number
sed -i '10i\new line of text' filename

# Append text at end of file
sed -i '$a\new line of text' filename
```

## File Writing Methods

### Using Cat with Here Document

#### Write to File (Overwrite)

```bash
cat <<EOF > myfile.txt
This is first line.
This is second line.
EOF
```

#### Append to File

```bash
cat <<EOF >> myfile.txt
Another line added.
EOF
```

### Using Echo

#### Simple Write

```bash
echo "content" > filename.txt
```

#### Append Content

```bash
echo "content to append" >> filename.txt
```

#### Variable Handling

```bash
echo "Variable \$name will not expand" > myscript.txt
echo "Variable $name will expand" > myscript.txt
```

### Using Tee Command

#### Write and Display

```bash
echo "Overwritten content" | tee myfile.txt
```

#### Multiline with Tee

```bash
cat <<EOF | tee myfile.txt
This is another way to write content.
It supports multiline input.
EOF
```

#### Append with Tee

```bash
echo "Content to append" | tee -a filename
```

#### Write to Privileged Files

```bash
echo "abc" | sudo tee -a /etc/apache2/apache2.conf
```

## File Content Comparison

### Compare Files

```bash
diff file1.txt file2.txt
diff -u file1.txt file2.txt  # Unified format
```

### Side by Side Comparison

```bash
sdiff file1.txt file2.txt
```

## Text Processing

### Count Lines, Words, Characters

```bash
wc filename.txt
wc -l filename.txt  # Lines only
wc -w filename.txt  # Words only
wc -c filename.txt  # Characters only
```

### Sort Text

```bash
sort filename.txt
sort -r filename.txt  # Reverse order
sort -u filename.txt  # Unique lines
```

### Remove Duplicate Lines

```bash
uniq filename.txt
sort filename.txt | uniq  # Sort first, then remove duplicates
```

### Search Text Patterns

```bash
grep "pattern" filename.txt
grep -r "pattern" /path/to/directory  # Recursive search
grep -i "pattern" filename.txt  # Case insensitive
grep -n "pattern" filename.txt  # Show line numbers
```

## Text Conversion

### Convert File Formats

```bash
dos2unix filename.txt  # Convert DOS line endings to Unix
unix2dos filename.txt  # Convert Unix line endings to DOS
```

### Change File Encoding

```bash
iconv -f UTF-8 -t ASCII filename.txt > output.txt
```

## Text Extraction

### Extract Columns

```bash
cut -d',' -f1,3 filename.csv  # Extract columns 1 and 3
awk '{print $1, $3}' filename.txt  # Using awk
```

### Extract Lines

```bash
sed -n '10,20p' filename.txt  # Lines 10-20
head -n 20 filename.txt | tail -n 10  # Lines 11-20
```

## Text Replacement in Multiple Files

### Find and Replace Recursively

```bash
find . -name "*.txt" -exec sed -i 's/old_text/new_text/g' {} \;
```

### Using grep and sed

```bash
grep -rl "old_text" /path/to/directory | xargs sed -i 's/old_text/new_text/g'
```

## Advanced Text Editing

### Using awk

```bash
# Print specific columns
awk '{print $1, $3}' filename.txt

# Conditional printing
awk '$3 > 100 {print $1, $3}' filename.txt

# Sum columns
awk '{sum += $3} END {print sum}' filename.txt
```

### Using perl for Complex Operations

```bash
perl -pi -e 's/old_text/new_text/g' filename.txt
```

## Text Formatting

### Join Lines

```bash
paste -sd '' filename.txt  # Join all lines into one
tr -d '\n' < filename.txt  # Remove newlines
```

### Split Long Lines

```bash
fold -w 80 filename.txt  # Wrap at 80 characters
```

## File Content Analysis

### Show File Type

```bash
file filename.txt
```

### Hex View

```bash
hexdump -C filename.txt
xxd filename.txt
```

### Show Non-printable Characters

```bash
cat -A filename.txt
```
