# Step 1 – Hello World: Your First Script

Every programming journey begins with a "Hello, World!" program. In Bash, a script is simply a plain text file containing a series of commands that the shell will execute in order.

## The shebang line

The very first line of any Bash script should be the **shebang** (`#!`) followed by the path to the interpreter:

```bash
#!/bin/bash
```

This tells the operating system which program should be used to run the file.

## Create your first script

Use the `cat` command with a **here-document** to create the file in one step:

```bash
cat << 'EOF' > hello.sh
#!/bin/bash
echo "Hello, World!"
EOF
```{{execute}}

## Make the script executable

By default, a newly created file cannot be executed. Use `chmod` to add execute permission:

```bash
chmod +x hello.sh
```{{execute}}

## Run the script

```bash
./hello.sh
```{{execute}}

You should see:

```
Hello, World!
```

## How it works

| Part | Meaning |
|------|---------|
| `#!/bin/bash` | Shebang — tells the OS to use `/bin/bash` |
| `echo` | Prints text to standard output |
| `./hello.sh` | `.` means "current directory"; needed because the current directory is not in `$PATH` by default |

## Quick check

Run the following command to confirm the script exists and is executable:

```bash
ls -l hello.sh
```{{execute}}

The output should include an `x` in the permission bits (e.g. `-rwxr-xr-x`).
