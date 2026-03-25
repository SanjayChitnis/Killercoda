# Step 2 – Variables

Variables let you store values and reuse them throughout a script. Bash variables are **untyped** — they hold strings by default, but can be used as numbers when needed.

## Defining a variable

Assign a value with `=`. **No spaces** around the `=` sign:

```bash
name="Alice"
age=30
```

## Using a variable

Reference a variable by prefixing its name with `$`:

```bash
echo $name
echo "My name is $name and I am $age years old."
```

Wrapping the variable name in curly braces (`${name}`) is a good habit — it avoids ambiguity when the variable name is followed immediately by other characters:

```bash
echo "Hello, ${name}!"
```

## Try it out

Create and run a script that uses variables:

```bash
cat << 'EOF' > variables.sh
#!/bin/bash
greeting="Hello"
name="World"
version=1

echo "${greeting}, ${name}!"
echo "Script version: ${version}"

# Arithmetic with $(( ))
x=10
y=3
echo "Sum: $((x + y))"
echo "Product: $((x * y))"
echo "Quotient: $((x / y))"
echo "Remainder: $((x % y))"
EOF
chmod +x variables.sh
./variables.sh
```{{execute}}

## Special variables

Bash also provides several built-in special variables:

| Variable | Meaning |
|----------|---------|
| `$0` | Name of the script |
| `$1`, `$2`, … | Positional arguments passed to the script |
| `$#` | Number of arguments |
| `$@` | All arguments as separate words |
| `$?` | Exit status of the last command (`0` = success) |
| `$$` | PID of the current shell |

## Try passing arguments

```bash
cat << 'EOF' > greet.sh
#!/bin/bash
echo "Script name : $0"
echo "First arg   : $1"
echo "Second arg  : $2"
echo "Total args  : $#"
EOF
chmod +x greet.sh
./greet.sh Bash Scripting
```{{execute}}
