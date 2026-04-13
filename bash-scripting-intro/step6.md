# Step 6 – Functions

Functions let you group a set of commands under a name so you can call them multiple times without repeating code.

## Defining a function

```bash
function_name() {
    # commands
}
```

Or using the `function` keyword (both forms are equivalent):

```bash
function function_name {
    # commands
}
```

> **Note:** A function must be defined **before** it is called.

## Calling a function

Simply write the function name (no parentheses when calling):

```bash
function_name
```

## Arguments

Functions receive arguments the same way scripts do — via `$1`, `$2`, `$#`, etc.:

```bash
greet() {
    echo "Hello, $1!"
}
greet "Alice"
```

## Return values

Bash functions do not return values the way functions in other languages do. They return an **exit status** (integer, `0`–`255`) via `return`. To return a string, use `echo` inside the function and capture the output with command substitution:

```bash
result=$(function_name)
```

---

## Try it out – basic function

```bash
cat << 'EOF' > functions.sh
#!/bin/bash

# Define a greeting function
say_hello() {
    echo "Hello, ${1:-World}!"
}

say_hello           # uses default "World"
say_hello "Alice"
say_hello "Bob"
EOF
chmod +x functions.sh
./functions.sh
```{{execute}}

## Try it out – function with return status

```bash
cat << 'EOF' > is_even.sh
#!/bin/bash

is_even() {
    if [ $(($1 % 2)) -eq 0 ]; then
        return 0   # success / true
    else
        return 1   # failure / false
    fi
}

for num in 1 2 3 4 5 6; do
    if is_even "$num"; then
        echo "${num} is even."
    else
        echo "${num} is odd."
    fi
done
EOF
chmod +x is_even.sh
./is_even.sh
```{{execute}}

## Try it out – function returning a string

```bash
cat << 'EOF' > get_timestamp.sh
#!/bin/bash

current_timestamp() {
    echo "$(date '+%Y-%m-%d %H:%M:%S')"
}

echo "Script started at: $(current_timestamp)"
echo "Doing some work..."
sleep 1
echo "Script ended at:   $(current_timestamp)"
EOF
chmod +x get_timestamp.sh
./get_timestamp.sh
```{{execute}}

## Putting it all together

Here is a mini-script that uses variables, input, conditionals, loops, **and** functions:

```bash
cat << 'EOF' > mini_app.sh
#!/bin/bash

# --- Functions ---
print_header() {
    echo "=============================="
    echo "  $1"
    echo "=============================="
}

is_positive() {
    [ "$1" -gt 0 ]
}

# --- Main ---
print_header "Number Analyzer"

read -p "How many numbers would you like to analyse? " count

total=0
for i in $(seq 1 "$count"); do
    read -p "  Enter number ${i}: " num
    total=$((total + num))
    if is_positive "$num"; then
        echo "    -> ${num} is positive"
    else
        echo "    -> ${num} is zero or negative"
    fi
done

echo ""
echo "Sum   : ${total}"
echo "Count : ${count}"
echo "Mean  : $(echo "scale=2; ${total} / ${count}" | bc)"
EOF
chmod +x mini_app.sh
./mini_app.sh
```{{execute}}
