CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
PROJECT(makepnd)
SET(MAKEPND_NAME "makepnd")
SET(MAKEPND_DESCRIPTION "Scripts for creating PND packages from recipe")
SET(MAKEPND_MAJOR 1)
SET(MAKEPND_MINOR 0)
SET(MAKEPND_BUGFIX 0)
SET(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${makepnd_SOURCE_DIR}/CMake/modules)

SET(SYSCONFDIR "/etc" CACHE STRING "System configuration directory")
SET(SYSDATADIR "/share" CACHE STRING "System data directory")
SET(SYSLOCALEDIR "${SYSDATADIR}/locale" CACHE STRING "System locale directory")

SET(CARCH "armv7" CACHE STRING "Compiler architecture")
SET(CHOST "armv7-openpandora-linux-gnu" CACHE STRING "Compiler host")

SET(BUILDSCRIPT "PNDBUILD" CACHE STRING "Filename of the recipe file")
SET(DEBUGSUFFIX "debug" CACHE STRING "Suffix for debug packages")
SET(STRIP_BINARIES "--strip-all" CACHE STRING "Strip options for binaries")
SET(STRIP_SHARED "--strip-unneeded" CACHE STRING "Strip options for shared libraries")
SET(STRIP_STATIC "--strip-debug" CACHE STRING "Strip options for static libraries")
SET(PKGEXT ".pnd" CACHE STRING "Default package extension")
SET(SRCEXT ".src.tar.gz" CACHE STRING "Default source package extension")

CONFIGURE_FILE(src/makepnd.in makepnd @ONLY)
CONFIGURE_FILE(etc/makepnd.conf.in makepnd.conf.default @ONLY)
INSTALL(PROGRAMS ${makepnd_BINARY_DIR}/makepnd DESTINATION bin)
INSTALL(FILES ${makepnd_BINARY_DIR}/makepnd.conf.default DESTINATION ${SYSCONFDIR})
INSTALL(FILES share/PXML_schema.xsd DESTINATION ${CMAKE_INSTALL_PREFIX}${SYSDATADIR}/makepnd)
INSTALL(FILES share/pndcorelibs DESTINATION ${CMAKE_INSTALL_PREFIX}${SYSDATADIR}/makepnd)
INSTALL(FILES share/pndlibs DESTINATION ${CMAKE_INSTALL_PREFIX}${SYSDATADIR}/makepnd)
