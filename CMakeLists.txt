cmake_minimum_required(VERSION 3.4.0)
project(StreamPilot C)

file(DOWNLOAD https://raw.githubusercontent.com/nicbarker/clay/refs/heads/main/clay.h ${PROJECT_SOURCE_DIR}/external/clay/clay.h)

include_directories(external)

add_executable(StreamPilot main.c)
