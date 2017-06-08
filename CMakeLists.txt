# This CMakeLists.txt has been first taken from LuaDist
# Copyright (C) 2007-2011 LuaDist.
# Created by Peter Drahoš
# Redistribution and use of this file is allowed according to the terms of the MIT license.
# Debugged and (now seriously) modified by Ronan Collobert, for Torch7

# This file has been modified for use with Marcin's LuaJIT

cmake_minimum_required(VERSION 3.5)
project(luajit)

add_custom_target(
  luajit ALL
  COMMAND make -C src
)

SET(INSTALL_INCLUDE_SUBDIR "include" CACHE STRING "installation include subdirectory name")

SET(INSTALL_BIN_SUBDIR "bin" CACHE STRING "installation executable subdirectory name")
SET(INSTALL_LIB_SUBDIR "lib" CACHE STRING "installation library subdirectory name")
SET(INSTALL_LUA_PATH_SUBDIR "share/lua/5.1/" CACHE STRING "lua path subdirectory name")
SET(INSTALL_LUA_LIB_SUBDIR "lib" CACHE STRING "installation lua lib subdirectory name")
SET(INSTALL_LUA_CPATH_SUBDIR "${INSTALL_LUA_LIB_SUBDIR}/lua/5.1/" CACHE STRING "lua cpath subdirectory name")

INSTALL(FILES src/luaconf.h src/lua.h src/lauxlib.h src/lualib.h
              src/lua.hpp src/luajit.h
  DESTINATION "${INSTALL_INCLUDE_SUBDIR}")

INSTALL(PROGRAMS
  src/luajit
  DESTINATION "${INSTALL_BIN_SUBDIR}")

INSTALL(FILES
  src/libluajit.a src/libluajit.so
  DESTINATION "${INSTALL_LIB_SUBDIR}")

INSTALL(FILES
  src/jit/bc.lua src/jit/v.lua src/jit/dump.lua src/jit/dis_x86.lua src/jit/dis_x64.lua src/jit/dis_arm.lua
  src/jit/dis_ppc.lua src/jit/dis_mips.lua src/jit/dis_mipsel.lua src/jit/bcsave.lua src/jit/bc.lua src/jit/p.lua 
  src/jit/zone.lua src/jit/vmdef.lua
  DESTINATION "${INSTALL_LUA_PATH_SUBDIR}/jit")

