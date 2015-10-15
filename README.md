# Skelix OS

Attempt to clean up the code of Skelix Operating System.

Origin: <http://skelix.net/skelixos/index_en.html>

Initially taken from: <https://github.com/shineyear/skelix_os/tree/ccfa60864defe199cb7ea7a8b2c9e72b12a913e4>

Requirements:

    sudo apt-get install build-essential qemu

Usage:

    cd directory-with-makefile
    make
    qemu final.img

Done:

- remove and gitignore output files
- factor out COPYING

TODO:

-   get all working... :-) Must add 32-bit flags to all compilation commands so it works on 64-bit computers.
-   factor out Makefiles:
    - don't hard code object files...
-   fix compiler warnings
