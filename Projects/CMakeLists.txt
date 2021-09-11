cmake_minimum_required(VERSION 3.21)
project(Projects C)

set(CMAKE_C_STANDARD 99)
set( CMAKE_C_FLAGS "-O2 -g -Wall -ffunction-sections")
add_executable(Projects main.c)
