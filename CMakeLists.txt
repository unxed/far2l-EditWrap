
project(far2l-EditWrap)

set(SOURCES
EditWrap.cpp 
)

add_library (far2l-EditWrap MODULE ${SOURCES})

if (${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    set(CMAKE_SHARED_MODULE_CREATE_CXX_FLAGS "${CMAKE_SHARED_MODULE_CREATE_CXX_FLAGS} -flat_namespace -undefined suppress")
endif()

target_link_libraries(far2l-EditWrap utils far2l)

target_compile_definitions(far2l-EditWrap PRIVATE -DWINPORT_DIRECT -DUNICODE -DFAR_DONT_USE_INTERNALS)

target_include_directories(far2l-EditWrap PRIVATE .)
target_include_directories(far2l-EditWrap PRIVATE ../far2l)
target_include_directories(far2l-EditWrap PRIVATE ../far2l/Include)
target_include_directories(far2l-EditWrap PRIVATE ../WinPort)

set_target_properties(far2l-EditWrap
  PROPERTIES
    LIBRARY_OUTPUT_DIRECTORY "${INSTALL_DIR}/Plugins/far2l-EditWrap/plug"
    PREFIX ""
    SUFFIX ".far-plug-wide")


#add_custom_command(TARGET far2l-EditWrap POST_BUILD
#   DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/configs
#   COMMAND ${CMAKE_COMMAND} -E copy_directory ${CMAKE_CURRENT_SOURCE_DIR}/configs "${INSTALL_DIR}/Plugins/far2l-EditWrap"
#)
