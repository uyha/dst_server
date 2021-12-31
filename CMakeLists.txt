cmake_minimum_required(VERSION 3.21)
project(DST LANGUAGES NONE)

set(CPACK_GENERATOR DEB)
set(CPACK_PACKAGE_NAME dst-server)
set(CPACK_PACKAGE_CONTACT "Uy Ha<hchanuy@gmail.com>")
set(CPACK_DEBIAN_PACKAGE_DEPENDS "curl,lib32gcc1,lib32stdc++6,libcurl4-gnutls-dev:i386")
string(CONCAT CPACK_DEBIAN_PACKAGE_CONTROL_EXTRA
  "${CMAKE_SOURCE_DIR}/data/deb-scripts/postinst;"
  "${CMAKE_SOURCE_DIR}/data/deb-scripts/prerm"
  )

install(
  PROGRAMS
    setup
    start
  DESTINATION libexec/dst)
install(
  FILES
    services/dst-master.service
    services/dst-caves.service
  DESTINATION /etc/systemd/system
  )

include(CPack)
