SET(EXAMPLES-SOURCES nfc-list nfc-mfclassic nfc-mfultralight nfcip-initiator nfcip-target nfc-anticol nfc-emulate nfc-relay)

# XXX: Examples should not use private API!
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/../libnfc)

INCLUDE_DIRECTORIES(${LIBUSB_INCLUDE_DIRS} ${PCSC_INCLUDE_DIRS})
LINK_DIRECTORIES(${LIBUSB_LIBRARY_DIRS} ${PCSC_LIBRARY_DIRS})

# Examples
FOREACH(source ${EXAMPLES-SOURCES})
  ADD_EXECUTABLE(${source} ${source}.c)
  TARGET_LINK_LIBRARIES(${source} nfc)
  INSTALL(TARGETS ${source} RUNTIME DESTINATION bin COMPONENT examples)
ENDFOREACH(source)

IF(NOT MSVC)
  # Manuals for the examples
  FILE(GLOB manuals "${CMAKE_CURRENT_SOURCE_DIR}/*.1")
  INSTALL(FILES ${manuals} DESTINATION ${SHARE_INSTALL_PREFIX}/man/man1 COMPONENT manuals)
ENDIF(NOT MSVC)