# GTK 4 Setup and Installation

The code in this repository was written and tested in a Debian system. Installing the necessary packages and libraries was as simple as running:

```
sudo apt update && sudo apt install libgtk-4-dev
```

That will even configure the `pkg-config` utility program.
```
pkg-config --cflags gtk4
pkg-config --libs gtk4
```

The output of those commands are useful flags for compiling the GTK app later on.

## Source Code
### Example Hello World App
Source code: [`hello-world.c`](./hello-world.c)

This source code comes origianlly from the [GTK documentation](https://docs.gtk.org/gtk4/getting_started.html). I hand-typed the source code from the guide to have a better understanding of this first hello world app. Most of the work was actually setting up the environment.

As the guide instructs, compiliing the code can be done using the following command.
```
gcc $(pkg-config --cflags gtk4) -o hello-world.out hello-world.c $(pkg-config --libs gtk4)
```

## Problems Encountered
This section contains some very specific problems I encountered in my environment. They may not apply to you, but I use them as reference for the future.

### Using C++ Extension Package in Visual Studio Code
Before starting to code, as soon as I got the first C file opened, there was a `the language server crashed` error. After attempting different solutions, installing a previous version of the C/C++ Visual Studio extension worked. I find the intellisense particularly useful when learning new frameworks.

### Intellisense Recognizing GTK Headers
After the intellisense started working again, header files would not be recognized.
```c
#include <gtk/gtk.h>
```

That's because the C/C++ Visual Studio extension didn't have the path to the include libraries. The best way to have no problems with the header files and intellisense was to add the path in the `.vscode/c_cpp_properties.json` file. To get the paths, use the `pkg-config` utility program.
```
pkg-config --cflags gtk4
```

Then, add all the include paths in the `c_cpp_properties.json` file. My configuration file looks like this:
```json
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**",
                "/usr/include/gtk-4.0",
                "/usr/include/pango-1.0",
                "/usr/include/glib-2.0",
                "/usr/lib/aarch64-linux-gnu/glib-2.0/include",
                "/usr/include/harfbuzz",
                "/usr/include/freetype2",
                "/usr/include/libpng16",
                "/usr/include/libmount",
                "/usr/include/blkid",
                "/usr/include/fribidi",
                "/usr/include/cairo",
                "/usr/include/pixman-1",
                "/usr/include/gdk-pixbuf-2.0",
                "/usr/include/aarch64-linux-gnu",
                "/usr/include/graphene-1.0",
                "/usr/lib/aarch64-linux-gnu/graphene-1.0/include"
            ],
            "defines": [],
            "compilerPath": "/usr/bin/gcc",
            "cStandard": "c17",
            "cppStandard": "gnu++17",
            "intelliSenseMode": "linux-gcc-arm64"
        }
    ],
    "version": 4
}
```