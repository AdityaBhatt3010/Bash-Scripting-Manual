# **Bash Scripting Basics Manual**  

## **1. Introduction to Bash Scripting**  
Bash (Bourne Again Shell) is a command-line interpreter that allows you to automate tasks, execute commands, and create scripts to streamline workflows.

### **Why Use Bash Scripting?**  
- Automate repetitive tasks  
- Run multiple commands in sequence  
- Process files and directories  
- Manage system tasks efficiently  

---

## **2. Writing and Running a Bash Script**  

### **Creating a Script File**  
1. Open a terminal and create a new file:  
   ```bash
   touch myscript.sh
   ```
2. Open the file in an editor:  
   ```bash
   nano myscript.sh
   ```
3. Add the following interpreter directive at the top of the script:  
   ```bash
   #!/bin/bash
   ```

### **Making the Script Executable**  
```bash
chmod +x myscript.sh
```

### **Running the Script**  
```bash
./myscript.sh
```

---

## **3. Basic Bash Syntax**  

### **Variables**  
```bash
NAME="John Doe"
echo "Hello, $NAME"
```

### **Reading User Input**  
```bash
echo "Enter your name:"
read NAME
echo "Hello, $NAME!"
```

### **Comments**  
```bash
# This is a single-line comment

: '
This is a 
multi-line comment
'
```

---

## **4. Conditional Statements**  

### **If-Else Statement**  
```bash
echo "Enter a number:"
read num

if [ "$num" -gt 10 ]; then
    echo "Number is greater than 10"
else
    echo "Number is 10 or less"
fi
```

### **Case Statement**  
```bash
echo "Enter a fruit:"
read fruit

case $fruit in
    apple) echo "You chose apple";;
    banana) echo "You chose banana";;
    *) echo "Unknown fruit";;
esac
```

---

## **5. Loops**  

### **For Loop**  
```bash
for i in 1 2 3 4 5; do
    echo "Number: $i"
done
```

### **While Loop**  
```bash
count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    ((count++))
done
```

---

## **6. Functions in Bash**  
```bash
greet() {
    echo "Hello, $1!"
}

greet "Alice"
```

---

## **7. Working with Files & Directories**  

### **Check If a File Exists**  
```bash
if [ -f "file.txt" ]; then
    echo "File exists"
else
    echo "File not found"
fi
```

### **Check If a Directory Exists**  
```bash
if [ -d "mydir" ]; then
    echo "Directory exists"
else
    echo "Directory not found"
fi
```

### **Reading a File Line by Line**  
```bash
while read line; do
    echo "$line"
done < file.txt
```

---

## **8. Arguments and Special Variables**  

### **Accessing Script Arguments**  
```bash
echo "First argument: $1"
echo "Second argument: $2"
```

### **Special Variables**  
- `$0` → Script name  
- `$#` → Number of arguments  
- `$@` → All arguments  
- `$$` → Process ID of the script  
- `$?` → Exit status of last command  

Example:
```bash
echo "This script's name is: $0"
echo "Number of arguments passed: $#"
```

---

## **9. Exit Status & Error Handling**  

### **Checking Command Success**  
```bash
mkdir mydir
if [ $? -eq 0 ]; then
    echo "Directory created successfully"
else
    echo "Failed to create directory"
fi
```

### **Using `set -e` to Stop on Errors**  
```bash
set -e
mkdir mydir
cd mydir
touch file.txt
```
This will stop execution if any command fails.

---

## **10. Scheduling Bash Scripts**  

### **Using Cron Jobs (Linux)**  
To run a script every day at 5 PM:  
```bash
crontab -e
```
Add this line:
```bash
0 17 * * * /path/to/myscript.sh
```

### **Using `at` Command**  
To run a script at a specific time:  
```bash
echo "/path/to/myscript.sh" | at 5pm
```

---

## **11. Useful Bash Commands for Scripting**  

| Command  | Description |
|----------|------------|
| `ls` | List directory contents |
| `pwd` | Show current directory |
| `cd` | Change directory |
| `mkdir` | Create a directory |
| `rm` | Remove files or directories |
| `cp` | Copy files |
| `mv` | Move/rename files |
| `echo` | Print text to the terminal |
| `cat` | Display file contents |
| `grep` | Search text in files |
| `awk` | Text processing tool |
| `sed` | Stream editor for modifying files |

---

## **12. Debugging Bash Scripts**  

### **Enable Debug Mode**  
Run the script with `-x` for debugging:
```bash
bash -x myscript.sh
```

### **Use `set -x` for Debugging Inside Script**  
```bash
set -x  # Enable debug mode
echo "Debugging this script"
set +x  # Disable debug mode
```

---

## **13. Example: A Simple Automation Script**  

```bash
#!/bin/bash
# Backup script

SOURCE_DIR="/home/user/documents"
BACKUP_DIR="/home/user/backup"
TIMESTAMP=$(date +%Y%m%d%H%M%S)
BACKUP_FILE="backup-$TIMESTAMP.tar.gz"

echo "Creating backup..."
tar -czf "$BACKUP_DIR/$BACKUP_FILE" "$SOURCE_DIR"

if [ $? -eq 0 ]; then
    echo "Backup successful: $BACKUP_DIR/$BACKUP_FILE"
else
    echo "Backup failed!"
fi
```

---

## **14. Advanced Concepts**  

### **Using Arrays in Bash**  
```bash
arr=("apple" "banana" "cherry")
echo "First fruit: ${arr[0]}"
```

### **Using `trap` for Cleanup**  
```bash
trap "echo 'Script interrupted!'; exit 1" SIGINT
```

---

## **15. Conclusion**  
Bash scripting is a powerful tool for automating tasks and managing system operations. With practice, you can create complex scripts to improve efficiency.
