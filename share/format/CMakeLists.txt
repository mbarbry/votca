find_program(CLANG_FORMAT_EXECUTABLE clang-format)
find_package_handle_standard_args(CLANG_FORMAT REQUIRED_VARS CLANG_FORMAT_EXECUTABLE)
if(CLANG_FORMAT_FOUND)
  set(FORMAT_SOURCES)
  foreach(DIR ${ENABLED_VOTCA_PACKAGES})
    set(ABS_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../../${DIR})
    file(GLOB_RECURSE ${DIR}_SOURCES ${ABS_DIR}/*.cc ${ABS_DIR}/*.h)
    list(APPEND FORMAT_SOURCES ${${DIR}_SOURCES})
  endforeach()
  add_custom_target(format
    COMMAND ${CLANG_FORMAT_EXECUTABLE} -i -style=file ${FORMAT_SOURCES}
    DEPENDS ${FORMAT_SOURCES})
endif()
