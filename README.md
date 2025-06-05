# Slough - Dev Container - ASM 6502

Docker image for a development container for ASM 6502 projects.

This container contains all the tools you need to assemble a 6502 assembly file.

To assemble a 6502 asm file, use the following commands:

```bash
# Assemble
ca65 file.s -o file.o

# Link
ld65 -o out.bin file.o -C /home/developer/linker_config_example.cfg
```
