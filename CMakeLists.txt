cmake_minimum_required(VERSION 3.5)
project(luajit)

add_custom_target(
  luajit ALL
  COMMAND make -C src
  COMMAND cp src/luajit ./
  COMMAND cp src/libluajit.so ./
)

add_custom_target(
  luajit_clean CLEAN
  COMMAND make clean -C src
  COMMAND rm -rf luajit
  COMMAND rm -rf libluajit.so
)
