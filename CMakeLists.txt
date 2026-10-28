cmake_minimum_required(VERSION 3.10)
project(catalog-sdl3-demo C)

set(SDL_X11_XSCRNSAVER OFF)
set(SDL_X11_XINPUT OFF)
set(SDL_X11_XFIXES OFF)
set(SDL_X11_XTEST OFF)

include("${CMAKE_CURRENT_SOURCE_DIR}/cl-bootstrap.cmake")
cl_repo()

set(CATALOG_REQ_TYPE PREFER_STATIC)
add_executable(demo main.c)
cl_add_dep(demo SDL3)
