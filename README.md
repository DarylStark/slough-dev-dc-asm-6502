# Slough - Dev Container - ASM 6502

Docker image for a development container for 6502 Assembly projects.

## About Slough

This container is part of the **Slough** project by Daryl Stark. The Slough project aims to deliver consistent development tooling through dev containers, providing standardized development environments across different projects and platforms.

## Using This Container as a Dev Container

### Image Tag

The image for this container is available as:

```
dast1968/slough-dev-dc-asm-6502:1.0.0
```

### Setting Up in VS Code

1. Install the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) in VS Code
2. Create a `.devcontainer/devcontainer.json` file in your project root:

```json
{
    "name": "6502 Assembly Development",
    "image": "dast1968/slough-dev-dc-asm-6502:1.0.0",
    "customizations": {
        "vscode": {
            "extensions": []
        }
    }
}
```

3. Open the command palette (F1 or Ctrl+Shift+P / Cmd+Shift+P)
4. Select "Dev Containers: Reopen in Container"
5. VS Code will download the image and start your development environment

### Setting Up in Other IDEs

For other IDEs that support dev containers (like JetBrains IDEs with the Dev Containers plugin), use the same image tag: `dast1968/slough-dev-dc-asm-6502:1.0.0`

## Tips for Working with Dev Containers

### General Tips

- **First-time setup**: The first time you open a dev container, it may take a few minutes to download the image
- **Persistence**: Files in your project directory are persisted, but files outside the workspace are not
- **Extensions**: Install your favorite VS Code extensions inside the container for the best experience

### Windows-Specific Tips

- **WSL2 Required**: Dev Containers work best with Docker Desktop using the WSL2 backend
- **File Performance**: For best performance on Windows, clone your repository inside WSL2 (e.g., in `~/projects/`) rather than in the Windows filesystem (`/mnt/c/`)
- **Line Endings**: Configure Git to use LF line endings to avoid issues:
  ```bash
  git config --global core.autocrlf input
  ```
- **Docker Desktop**: Make sure Docker Desktop is running before opening VS Code
- **WSL2 Integration**: Enable WSL2 integration in Docker Desktop settings for your distribution

## Container Configuration

### User Information

- **Username**: `developer`
- **Home Directory**: `/home/developer`
- **Sudo Access**: Available without password (no password required for `sudo` commands)
- **Shell**: Bash with custom prompt (Starship) configured

### Pre-configured Files

The following files are available in the home directory:

- `/home/developer/linker_config_example.cfg` - Example linker configuration for 6502 projects
- `/home/developer/README.md` - Quick reference guide for assembly commands

## Installed Tools

This container includes the following tools for 6502 Assembly development:

### cc65 Toolchain

The primary toolset for 6502 development, including:

- **ca65**: The 6502 assembler
- **ld65**: The linker for 6502 object files
- **cc65**: C compiler targeting 6502 (can compile C to 6502 assembly)

#### Basic Usage

Assemble and link a 6502 assembly file:

```bash
# Assemble the source file
ca65 file.s -o file.o

# Link the object file
ld65 -o out.bin file.o -C /home/developer/linker_config_example.cfg
```

#### Advanced Usage

Using multiple source files:

```bash
# Assemble multiple files
ca65 main.s -o main.o
ca65 utils.s -o utils.o

# Link them together
ld65 -o program.bin main.o utils.o -C /home/developer/linker_config_example.cfg
```

Using debug symbols:

```bash
# Assemble with debug info
ca65 -g file.s -o file.o

# Link with debug info
ld65 -g -o out.bin file.o -C /home/developer/linker_config_example.cfg
```

### py65mon

An interactive 6502 simulator and monitor for testing your assembled programs.

#### Usage

```bash
# Start the monitor
py65mon

# Load a binary file
py65mon -m 65c02 -r out.bin

# Common commands inside py65mon:
# - g <address>  : Go (run from address)
# - d <address>  : Disassemble
# - m <address>  : Memory dump
# - r            : Show registers
# - q            : Quit
```

### hexedit

A hex editor for viewing and editing binary files.

#### Usage

```bash
# Open a binary file in hexedit
hexedit out.bin

# Inside hexedit:
# - Tab: Switch between hex and ASCII
# - Ctrl+X: Exit and save
# - Ctrl+C: Exit without saving
```

### Build Essential Tools

Standard build tools including:

- **make**: Build automation
- **gcc**: GNU C compiler (for building tools, not for 6502 target)
- **g++**: GNU C++ compiler

### UV Package Manager

Modern Python package manager pre-installed:

```bash
# Update uv
uv self update

# Install Python tools
uv tool install <package-name>
```

## Example Workflow

1. Create your assembly file (e.g., `hello.s`)
2. Assemble it:
   ```bash
   ca65 hello.s -o hello.o
   ```
3. Link it:
   ```bash
   ld65 -o hello.bin hello.o -C /home/developer/linker_config_example.cfg
   ```
4. Test it in the simulator:
   ```bash
   py65mon -r hello.bin
   ```
5. Inspect the binary if needed:
   ```bash
   hexedit hello.bin
   ```

## Additional Resources

- [cc65 Documentation](https://cc65.github.io/doc/)
- [6502 Instruction Set Reference](http://www.6502.org/tutorials/6502opcodes.html)
- [py65 Documentation](https://py65.readthedocs.io/)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## Author

Created by Daryl Stark as part of the Slough project.
