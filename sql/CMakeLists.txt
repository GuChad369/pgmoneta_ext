# retrieve the shared directory of the PostgreSQL installation
execute_process(COMMAND pg_config --sharedir
                OUTPUT_STRIP_TRAILING_WHITESPACE
                OUTPUT_VARIABLE SHARE_DIR)

# handle the result
if (SHARE_DIR)
  set(SHARE_DIR "${SHARE_DIR}/extension")
  message(STATUS "Extension directory: ${SHARE_DIR}")
else (SHARE_DIR)
  message(FATAL_ERROR "pg_config --sharedir failed")
endif (SHARE_DIR)

# Installing SQL Files
install(DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/"
        DESTINATION "${SHARE_DIR}" 
        FILES_MATCHING PATTERN "*.sql")

# Installing Control Files
install(DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/"
        DESTINATION "${SHARE_DIR}" 
        FILES_MATCHING PATTERN "*.control")