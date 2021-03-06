
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

PROJECT(zlib)

IF(MSVC)
	ADD_DEFINITIONS(-D_CRT_SECURE_NO_DEPRECATE=1)
	ADD_DEFINITIONS(-D_CRT_SECURE_NO_WARNINGS=1)
	ADD_DEFINITIONS(-D_CRT_NONSTDC_NO_DEPRECATE=1)
ENDIF()

INCLUDE(CheckIncludeFile)
CHECK_INCLUDE_FILE("unistd.h" HAVE_UNISTD_H)
CHECK_INCLUDE_FILE("stdarg.h" HAVE_STDARG_H)

IF(HAVE_UNISTD_H)
	ADD_DEFINITIONS(-DHAVE_UNISTD_H=1)
ENDIF()

IF(HAVE_STDARG_H)
	ADD_DEFINITIONS(-DHAVE_STDARG_H=1)
ENDIF()

SET(ZLIB_INCLUDE_DIR "${CMAKE_CURRENT_SOURCE_DIR}" CACHE INTERNAL "" FORCE)
SET(ZLIB_LIBRARY "zlib" CACHE INTERNAL "" FORCE)

ADD_LIBRARY(zlib STATIC EXCLUDE_FROM_ALL
	adler32.c
	compress.c
	crc32.c
	crc32.h
	deflate.c
	deflate.h
	gzclose.c
	gzguts.h
	gzlib.c
	gzread.c
	gzwrite.c
	infback.c
	inffast.c
	inffast.h
	inffixed.h
	inflate.c
	inflate.h
	inftrees.c
	inftrees.h
	trees.c
	trees.h
	uncompr.c
	zconf.h
	zlib.h
	zutil.c
	zutil.h
)

SET_TARGET_PROPERTIES(zlib PROPERTIES OUTPUT_NAME "z")
