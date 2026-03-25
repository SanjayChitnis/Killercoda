# Step 5 – Loops

Loops let you repeat a block of commands multiple times, either over a list of items or until a condition changes.

## `for` loop

Iterate over a list of words:

```bash
for item in list_of_items; do
    # commands
done
```

## `while` loop

Repeat as long as a condition is true:

```bash
while [ condition ]; do
    # commands
done
```

## `until` loop

Repeat **until** a condition becomes true (opposite of `while`):

```bash
until [ condition ]; do
    # commands
done
```

---

## Try it out – `for` loop over a list

```bash
cat << 'EOF' > for_list.sh
#!/bin/bash
for fruit in apple banana cherry mango; do
    echo "Fruit: ${fruit}"
done
EOF
chmod +x for_list.sh
./for_list.sh
```{{execute}}

## Try it out – `for` loop with a range

Use `{start..end}` brace expansion or the `seq` command:

```bash
cat << 'EOF' > for_range.sh
#!/bin/bash
echo "Counting up:"
for i in {1..5}; do
    echo "  ${i}"
done

echo "Counting down:"
for i in {5..1}; do
    echo "  ${i}"
done
EOF
chmod +x for_range.sh
./for_range.sh
```{{execute}}

## Try it out – `for` loop over files

```bash
cat << 'EOF' > for_files.sh
#!/bin/bash
echo "Shell scripts in the current directory:"
for file in *.sh; do
    echo "  ${file}"
done
EOF
chmod +x for_files.sh
./for_files.sh
```{{execute}}

## Try it out – `while` loop

```bash
cat << 'EOF' > countdown.sh
#!/bin/bash
count=5
echo "Countdown:"
while [ "$count" -gt 0 ]; do
    echo "  ${count}..."
    count=$((count - 1))
done
echo "Liftoff!"
EOF
chmod +x countdown.sh
./countdown.sh
```{{execute}}

## Loop control: `break` and `continue`

- **`break`** exits the loop immediately.
- **`continue`** skips the rest of the current iteration and moves to the next one.

```bash
cat << 'EOF' > loop_control.sh
#!/bin/bash
echo "Even numbers from 1 to 10 (skipping odd with continue):"
for i in {1..10}; do
    if [ $((i % 2)) -ne 0 ]; then
        continue   # skip odd numbers
    fi
    echo "  ${i}"
done

echo ""
echo "Numbers until we hit 7 (break at 7):"
for i in {1..10}; do
    if [ "$i" -eq 7 ]; then
        break   # stop the loop
    fi
    echo "  ${i}"
done
EOF
chmod +x loop_control.sh
./loop_control.sh
```{{execute}}
