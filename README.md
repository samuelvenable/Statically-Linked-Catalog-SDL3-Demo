# Statically Linked Catalog SDL3 Demo

Very special thanks to [Grady Link](https://github.com/gradylink) for writing this demo for me!

Test the demo:

```sh
git clone https://github.com/samuelvenable/Statically-Linked-Catalog-SDL3-Demo ~/Statically-Linked-Catalog-SDL3-Demo
cd ~/Statically-Linked-Catalog-SDL3-Demo
cmake .
cmake --build .
cd build
./demo
```

This will work cross-platform, even on platforms where statically linking is more difficult such as Linux or BSD.

`cl-bootstrap.cmake` needs to be included in your project but can be ignored and does not need editing.

This needs to be added before `add_executable()` or `add_library()` in your `CMakeLists.txt`:

```cmake
include("${CMAKE_CURRENT_SOURCE_DIR}/cl-bootstrap.cmake")
cl_repo()

set(CATALOG_REQ_TYPE PREFER_STATIC)
```

`PREFER_STATIC` will use static dependencies when available. Use `STATIC` instead to refuse dynamic linking.

...and then after `add_executable()` or `add_library()` you need:

```cmake
cl_add_dep(MyProject SDL3)
```

For ***all*** platforms where SDL3's X11 code is compiled, you will need this at the top of your `CMakeLists.txt`:

```cmake
set(SDL_X11_XSCRNSAVER OFF)
```

For ***some*** platforms where SDL3's X11 code is compiled, (for example: `armhf`-based Linux), you also need:

```cmake
set(SDL_X11_XINPUT OFF)
set(SDL_X11_XFIXES OFF)
set(SDL_X11_XTEST OFF)
```

- For the SDL2 equivalent of this repository, please see my [Statically-Linked-Catalog-SDL2-Demo](https://github.com/samuelvenable/Statically-Linked-Catalog-SDL2-Demo) repository.
- For a more complex and practical use-case example, please see my [SDL3-ImGui-FileDialogs](https://github.com/samuelvenable/SDL3-ImGui-FileDialogs) repository.
