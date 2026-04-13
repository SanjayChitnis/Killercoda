# Step 4 – Conditional Statements

Conditionals allow a script to make decisions and take different actions depending on whether a condition is true or false.

## Basic `if` syntax

```bash
if [ condition ]; then
    # commands run when condition is true
fi
```

## `if` / `else`

```bash
if [ condition ]; then
    # true branch
else
    # false branch
fi
```

## `if` / `elif` / `else`

```bash
if [ condition1 ]; then
    # branch 1
elif [ condition2 ]; then
    # branch 2
else
    # default branch
fi
```

## Common test operators

### String comparisons

| Expression | Meaning |
|-----------|---------|
| `[ "$a" = "$b" ]` | Equal |
| `[ "$a" != "$b" ]` | Not equal |
| `[ -z "$a" ]` | Empty string |
| `[ -n "$a" ]` | Non-empty string |

### Numeric comparisons

| Expression | Meaning |
|-----------|---------|
| `[ $a -eq $b ]` | Equal |
| `[ $a -ne $b ]` | Not equal |
| `[ $a -lt $b ]` | Less than |
| `[ $a -le $b ]` | Less than or equal |
| `[ $a -gt $b ]` | Greater than |
| `[ $a -ge $b ]` | Greater than or equal |

### File tests

| Expression | Meaning |
|-----------|---------|
| `[ -f "$path" ]` | Regular file exists |
| `[ -d "$path" ]` | Directory exists |
| `[ -e "$path" ]` | File or directory exists |
| `[ -r "$path" ]` | File is readable |
| `[ -x "$path" ]` | File is executable |

## Try it out – number comparison

```bash
cat << 'EOF' > check_number.sh
#!/bin/bash
read -p "Enter a number: " num

if [ "$num" -lt 0 ]; then
    echo "${num} is negative."
elif [ "$num" -eq 0 ]; then
    echo "You entered zero."
else
    echo "${num} is positive."
fi
EOF
chmod +x check_number.sh
./check_number.sh
```{{execute}}

## Try it out – file test

```bash
cat << 'EOF' > check_file.sh
#!/bin/bash
read -p "Enter a filename: " filepath

if [ -f "$filepath" ]; then
    echo "'${filepath}' is a regular file."
elif [ -d "$filepath" ]; then
    echo "'${filepath}' is a directory."
else
    echo "'${filepath}' does not exist."
fi
EOF
chmod +x check_file.sh
./check_file.sh
```{{execute}}

Try entering `hello.sh` (which you created in Step 1) and then `/etc` to see different outputs.
