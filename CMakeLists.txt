cmake_minimum_required(VERSION 3.1)

# project name
project(fonts-lenmus-bravura)

# install folder
set(INSTALL_DIR "/usr/share/fonts/truetype/")

#install Bravura font
install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/src/Bravura.otf
        DESTINATION ${INSTALL_DIR}
)

# configure CPack for Debian packages
set(CPACK_MONOLITHIC_INSTALL 1)
set(CPACK_DEB_COMPONENT_INSTALL 0)

set(CPACK_PACKAGE_VENDOR "LenMus")
set(CPACK_PACKAGE_CONTACT "s.cecilio@gmail.com")
set(CPACK_GENERATOR "DEB")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Cecilio Salmeron <s.cecilio@gmail.com>")
set(CPACK_DEBIAN_PACKAGE_HOMEPAGE "https://github.com/lenmus/bravura")
set(CPACK_STRIP_FILES ON)		#remove debug information, if any, from binaries
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Bravura music font to render music scores")
set(CPACK_PACKAGE_DESCRIPTION
"Bravura music font to render music scores
 Bravura is a Unicode typeface designed by Steinberg. It is compliant with
 the Standard Music Font Layout (SMuFL), a community-driven standard for how
 music symbols should be laid out in the Unicode Private Use Area (PUA) in
 the Basic Multilingual Plane (BMP) for compatibility between different
 scoring applications.
 .
 More information about Steinberg's scoring application can be found at:
 http://www.steinberg.net/
 .
 The latest version of the SMuFL specification can be found at:
 https://w3c.github.io/smufl/gitbook/
")
set(CPACK_DEBIAN_PACKAGE_NAME "fonts-lenmus-bravura")
set(CPACK_DEBIAN_PACKAGE_VERSION "1.18-0")
set(CPACK_DEBIAN_PACKAGE_SECTION "fonts") 
set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "all")
string(CONCAT CPACK_PACKAGE_FILE_NAME "${CPACK_DEBIAN_PACKAGE_NAME}"
        "_${CPACK_DEBIAN_PACKAGE_VERSION}_${CPACK_DEBIAN_PACKAGE_ARCHITECTURE}")
set(CPACK_DEBIAN_PACKAGE_DEPENDS "")
set(CPACK_DEBIAN_PACKAGE_DESCRIPTION ${CPACK_PACKAGE_DESCRIPTION})

# Must be after the last CPACK macro
include(CPack)

message(" ")
message("CMakeLists.txt processed. Generation starts:")
