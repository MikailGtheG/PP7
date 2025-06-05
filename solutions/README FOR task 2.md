# Task 2: Regex Search & Replace in Code

This README explains how to search and replace text in code using command-line tools like `grep`, `sed`, `awk`, and `vim`.  
The example replaces all `printf` calls with `debug_printf` in a C file.

---

## Step 1: Copy the File

```bash
cp solutions/sample.c solutions/debug_sample.c
```

We make a copy of the original file to work on.

---

## Step 2: Search with `grep`

```bash
grep -En "printf\s*\(" solutions/debug_sample.c
```

**What happens:**  
- `-E` enables extended regex.
- `-n` shows the line number.
- The regex `printf\s*\(` finds `printf` followed by optional spaces and `(`.

Use this to locate all lines with `printf()` function calls.

---

## Step 3: Replace with `sed` (in-place)

```bash
sed -E -i.bak 's/printf\s*/debug_printf/g' solutions/debug_sample.c
```

**What happens:**  
- `-E` enables extended regex.
- `-i.bak` edits the file in-place and creates a backup with `.bak`.
- `s/printf\s*/debug_printf/g` replaces every `printf` with `debug_printf` globally in each line.

After this, `solutions/debug_sample.c` is updated.

---

## Step 4: Extract with `awk`

```bash
awk '/debug_printf/ { print NR, $0 }' solutions/debug_sample.c
```

**What happens:**  
- `awk` looks for lines that contain `debug_printf`.
- `print NR, $0` prints the line number (`NR`) and the line itself (`$0`).

This is useful to confirm which lines were changed.

---

## Step 5: Vim Interactive

```bash
vim solutions/debug_sample.c
```

Inside Vim:

1. Press `/` and type `printf`, then hit `Enter` to search.
2. Use `n` to move to the next match.
3. Replace all with:

```vim
:%s/printf/debug_printf/g
```

4. Save and quit with:

```vim
:wq
```

---

## Step 6: Vim CLI (no UI)

```bash
vim -c ":%s/printf/debug_printf/g" -c ":wq" solutions/debug_sample.c
```

This runs the same replacement directly from the terminal without entering the Vim editor.

---

## Summary: When to Use What?

| Tool  | Use Case | Notes |
|-------|----------|-------|
| `grep` | To **find** lines with a pattern | Fast, shows line numbers |
| `sed`  | To **replace** text directly in files | Good for batch processing |
| `awk`  | To **extract** and format matched lines | Good for custom reports |
| `vim` (interactive) | For **manual review and editing** | Good when you want control |
| `vim` (CLI) | To **script Vim actions** | Combines power of Vim with automation |

Each tool is strong in different situations.  
Use `grep` to search, `sed` to edit, `awk` to filter, and `vim` when you need precision.

---
