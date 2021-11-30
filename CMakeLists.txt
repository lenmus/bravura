cmake_minimum_required(VERSION 3.1)

# project name
project(fonts-lenmus-bravura)

# install folder
set(INSTALL_DIR "/usr/share/fonts/truetype/")

#install Bravura font
install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/src/Bravura.otf
        DESTINATION ${INSTALL_DIR}
)

#CPack configuration. Common to all generators
set(CPACK_PACKAGE_NAME "fonts-lenmus-bravura")
set(CPACK_MONOLITHIC_INSTALL 1)
set(CPACK_PACKAGE_VENDOR "LenMus")
set(CPACK_PACKAGE_CONTACT "s.cecilio@gmail.com")
set(CPACK_PACKAGE_MAINTAINER "Cecilio Salmeron <s.cecilio@gmail.com>")
set(CPACK_PACKAGE_HOMEPAGE "https://github.com/lenmus/bravura")
set(CPACK_STRIP_FILES ON)		#remove debug information, if any, from binaries
set(CPACK_PACKAGE_LICENSE "SIL Open Font License")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Bravura music font to render music scores")
set(CPACK_PACKAGE_DESCRIPTION
"Bravura music font to render music scores
 Bravura is a Unicode typeface designed by Steinberg. It is compliant with
 the Standard Music Font Layout (SMuFL), a community-driven standard for how
 music symbols should be laid out in the Unicode Private Use Area (PUA) in
 the Basic Multilingual Plane (BMP) for compatibility between different
 scoring applications.
 .
 The Bravura font family is made available under the SIL Open Font License.
 .
 The Steinberg's repo for this font is at:
 https://github.com/steinbergmedia/bravura
 .
 The latest version of the SMuFL specification can be found at:
 https://w3c.github.io/smufl/gitbook/
")

#Determine Linux Distro
find_program(LSB_RELEASE_EXEC lsb_release)
execute_process(COMMAND ${LSB_RELEASE_EXEC} -is
    OUTPUT_VARIABLE   DISTRIBUTOR_ID
    OUTPUT_STRIP_TRAILING_WHITESPACE
)

#determine if RPM or DEB package
# RPM:
#   CentOS, Fedora, Mageia, Mandriva, OpenMandriva, openSUSE, 
#   Red Hat Linux, SUSE
# DEB:
#   Debian, Knoppix, Guadalinex, Linux Mint, Ubuntu
#
set(CPACK_GENERATOR "DEB")  #assume DEB

if (("${DISTRIBUTOR_ID}" STREQUAL "CentOS") OR
    ("${DISTRIBUTOR_ID}" STREQUAL "Fedora") OR
    ("${DISTRIBUTOR_ID}" STREQUAL "openSUSE")
   )
    set(CPACK_GENERATOR "RPM")

#TODO: Confirm Distributor ID for other distros
# from Internet:
#   "CentOS"
#   "Debian"
#   "RedHatEntrerpriseServer"
#   "openSUSE project"
#   "Ubuntu"
# confirmed:
#   "LinuxMint"

endif()
message(STATUS "DISTRIBUTOR_ID: ${DISTRIBUTOR_ID}")
message(STATUS "CPack generator: ${CPACK_GENERATOR}")


# configure CPack for Debian (.deb) packages
set(CPACK_DEB_COMPONENT_INSTALL 0)
set(CPACK_DEBIAN_PACKAGE_VERSION "1.392-0")
set(CPACK_DEBIAN_PACKAGE_ARCHITECTURE "all")
set(CPACK_DEBIAN_PACKAGE_SECTION "fonts") 
set(CPACK_PACKAGE_FILE_NAME "${CPACK_PACKAGE_NAME}_${CPACK_DEBIAN_PACKAGE_VERSION}_${CPACK_DEBIAN_PACKAGE_ARCHITECTURE}")
set(CPACK_DEBIAN_PACKAGE_DEPENDS "")
set(CPACK_DEBIAN_PACKAGE_DESCRIPTION ${CPACK_PACKAGE_DESCRIPTION})


#configure for Red Hat (.rpm) packages
set(CPACK_RPM_COMPONENT_INSTALL 0)
set(CPACK_RPM_PACKAGE_VERSION "1.392-0")
set(CPACK_RPM_PACKAGE_RELEASE 1)
set(CPACK_RPM_PACKAGE_ARCHITECTURE "noarch")
set(CPACK_RPM_PACKAGE_DESCRIPTION ${CPACK_PACKAGE_DESCRIPTION})
set(CPACK_RPM_FILE_NAME "${CPACK_PACKAGE_NAME}_${CPACK_RPM_PACKAGE_VERSION}_${CPACK_RPM_PACKAGE_ARCHITECTURE}.rpm")


# Must be after the last CPACK macro
include(CPack)

message(" ")
message("CMakeLists.txt processed. Generation starts:")
