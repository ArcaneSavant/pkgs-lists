<!-- cspell:words ArcaneSavant pkgs-lists pacman -->

# pkgs-lists

Using curl, awk, xargs, and system package management, pkgs-lists provides lists of packages to make it easier to install those packages in bulk on Linux.

## Installation Methods

### Using a Remote URL

```bash
xargs -a <(curl -s <remote_url> | awk '! /^ *(#|$)/') -r -- sudo apt install
```

> [!IMPORTANT]
> Replace <remote_url> with the actual URL containing package names.

### Using a Local File

```bash
xargs -a <(awk '! /^ *(#|$)/' "<file_path>") -r -- sudo apt install
```

> [!IMPORTANT]
> Replace <file_path> with the path to your local package list file.

## Explanation

1. `curl` downloads a file from a specified remote URL (when applicable).
1. `awk` filters the contents of the file to remove comments and blank lines.
1. `xargs` passes each remaining line as a package name to the system package manager (`apt` in this case).
1. Finally, the system package manager installs the packages passed to it by `xargs`.
   If you're using a different package manager, such as `dnf`, `zypper`, `pacman`, etc., be sure to replace `apt install` with the appropriate command for your system.

## Use Cases

This approach is particularly useful when dealing with a large number of packages or when repeating the installation process frequently.
You can keep a central list of packages and easily install them across multiple systems by re-running the installation command.
It's also beneficial when documenting dependencies and maintaining clarity about the intended software environment.

## Benefits

The approach of mass installing packages from a text file while preserving comments has several benefits.

- It offers flexibility in list sources (remote URLs or local files).
- It automates the installation process, saving you time and effort compared to manually installing each package individually.
- You can easily recreate the same package environment on different systems by running the command again.
- Comments in the file explain why specific packages are included, providing valuable documentation for your system setup.

## License

This is free and unencumbered software released into the public domain.
For more information, please refer to the [LICENSE](./LICENSE).
