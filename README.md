# Statically Linked Catalog SDL3 Demo

Very special thanks to [Grady Link](https://github.com/gradylink) for writing this demo for me!

Test the demo:

```sh
git clone https://github.com/samuelvenable/Statically-Linked-Catalog-SDL3-Demo \
~/Statically-Linked-Catalog-SDL3-Demo && cd ~/Statically-Linked-Catalog-SDL3-Demo \
&& mkdir build && cd build && cmake .. && make && ./demo
```

This will work cross-platform, even on platforms where statically linking is more difficult such as Linux or BSD.

`cl-bootstrap.cmake` needs to be included in your project but can mostly be ignored and does not require modification.

The only thing to really note is this needs to be added before `add_executable()` or `add_library()` in your `CMakeLists.txt`:

```cmake
include(${CMAKE_CURRENT_SOURCE_DIR}/cl-bootstrap.cmake)
cl_repo()

set(CATALOG_REQ_TYPE PREFER_STATIC)
```

`PREFER_STATIC` will use static dependencies when available. Use `STATIC` instead to attempt to refuse dynamic linking.

...and then after `add_executable()` or `add_library()` you need:

```cmake
cl_add_dep(demo SDL3)
```
