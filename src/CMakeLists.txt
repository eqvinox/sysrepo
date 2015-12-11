include_directories("${PROJECT_SOURCE_DIR}/inc")
set(SYSREPO-SOURCES
     sr_access.c
     )

set(SYSREPO-ENGINE-SOURCES
     data_manager.c
     connection_manager.c
     session_manager.c
     xpath_processor.c
     sr_common.c
     sr_logger.c
)

set(HEADERS "${PROJECT_SOURCE_DIR}/inc/sysrepo.h" "${PROJECT_SOURCE_DIR}/inc/sr_engine.h")

#shared and static library
add_library(sysrepo ${SYSREPO-SOURCES})
add_library(sysrepo_so SHARED ${SYSREPO-SOURCES})
SET_TARGET_PROPERTIES(sysrepo_so PROPERTIES
              OUTPUT_NAME sysrepo CLEAN_DIRECT_OUTPUT 1)

add_library(sysrepo-engine ${SYSREPO-ENGINE-SOURCES})
add_library(sysrepo-engine_so SHARED ${SYSREPO-ENGINE-SOURCES})
SET_TARGET_PROPERTIES(sysrepo-engine_so PROPERTIES
              OUTPUT_NAME sysrepo-engine CLEAN_DIRECT_OUTPUT 1)

target_link_libraries(sysrepo avl)
target_link_libraries(sysrepo_so avl)
target_link_libraries(sysrepo-engine avl)
target_link_libraries(sysrepo-engine_so avl)

install(TARGETS sysrepo_so DESTINATION ${LIB_INSTALL_DIR})
install(TARGETS sysrepo-engine_so DESTINATION ${LIB_INSTALL_DIR})
install(FILES ${HEADERS} DESTINATION ${INCLUDE_INSTALL_DIR})