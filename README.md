# smart-rm

A wrapper for `rm` to make it smarter and safer.

## Features

- **Preview before deletion**: Shows up to 20 entries that will be deleted
- **Smart file discovery**: Uses [`fd`](https://github.com/sharkdp/fd)/[`fdfind`](https://github.com/sharkdp/fd) when available, falls back to `find`
- **Minimal interference**: Behaves exactly like `rm` but with a safety check, you can use all `rm` options
- **Easy bypass**: Set environment variable to skip checks when needed

## Dependencies

- **Required**: `bash`, `rm` (standard on all Unix-like systems)
- **Optional**: [`fd`](https://github.com/sharkdp/fd) or [`fdfind`](https://github.com/sharkdp/fd) (faster file discovery, falls back to `find`)

## Installation

1. Download the script:

   ```bash
   curl -O https://raw.githubusercontent.com/yilinfang/smart-rm/main/smart-rm
   chmod +x smart-rm
   ```

2. Move to a directory in your PATH:

   ```bash
   sudo mv smart-rm /usr/local/bin/
   ```

3. (Optional) Create an alias in your shell configuration:

```bash
echo 'alias srm="smart-rm"' >> ~/.bashrc
# or
echo 'alias rm="smart-rm"' >> ~/.bashrc # Not recommended
```

## Usage

Use `smart-rm` exactly like you would use `rm`:

```bash
smart-rm file.txt
smart-rm -rf directory/
smart-rm *.log
smart-rm -i file1.txt file2.txt
```

### Example Output

```plaintext
$ smart-rm -rf old_project/
The following entries will be deleted:
old_project/src
old_project/docs
old_project/tests
old_project/.git
old_project/README.md
old_project/package.json
... and 15 more entries
Total: 21 entries
Are you sure you want to proceed? (y/N):
```

## Bypass Safety Check

When you need to skip the confirmation (e.g., in scripts), set the environment variable:

```bash
I_UNDERSTAND_WHAT_I_AM_DOING=1 smart-rm -rf directory/
```

Or export it for multiple operations:

```bash
export I_UNDERSTAND_WHAT_I_AM_DOING=1
smart-rm file1.txt
smart-rm file2.txt
unset I_UNDERSTAND_WHAT_I_AM_DOING
```

## License

MIT License
