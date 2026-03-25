# Step 3 – User Input

Scripts become much more powerful when they can interact with the user. The `read` command pauses execution and waits for the user to type something.

## Basic `read`

```bash
read variable_name
```

The text the user types (up to a newline) is stored in `variable_name`.

## Prompting the user

Use the `-p` flag to display a prompt on the same line:

```bash
read -p "Enter your name: " username
```

## Silent input (passwords)

Use `-s` to suppress echoing of typed characters — useful for passwords:

```bash
read -s -p "Enter password: " secret
```

## Try it out

```bash
cat << 'EOF' > ask_name.sh
#!/bin/bash
read -p "What is your name? " name
echo "Nice to meet you, ${name}!"
EOF
chmod +x ask_name.sh
./ask_name.sh
```{{execute}}

When prompted, type your name and press **Enter**.

## Reading multiple values

`read` can assign words to multiple variables in one call:

```bash
cat << 'EOF' > multi_read.sh
#!/bin/bash
read -p "Enter first and last name: " first last
echo "First : ${first}"
echo "Last  : ${last}"
EOF
chmod +x multi_read.sh
./multi_read.sh
```{{execute}}

## Default values

Use parameter expansion to provide a default when the variable is empty:

```bash
cat << 'EOF' > default_value.sh
#!/bin/bash
read -p "Enter your city (default: London): " city
city="${city:-London}"
echo "City: ${city}"
EOF
chmod +x default_value.sh
./default_value.sh
```{{execute}}

Try pressing **Enter** without typing anything to see the default take effect.
