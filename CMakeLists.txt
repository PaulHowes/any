cmake_minimum_required(VERSION 2.8.12)
project(any)

# Configures the compiler, regardless of the build type.
if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
  add_definitions(-std=c++11                # Use the modern language.
                  -Weverything              # Display every warning possible.
                  -Wno-c++98-compat         # Compiling for C++11; don't care about 98
                  -Wno-missing-prototypes   # Stupid warning.
                  -Wno-padded               # Don't care about padding.
                  -Wno-float-equal          # Just to keep the tests happy.
                  )
  if("${CMAKE_SYSTEM_NAME}" STREQUAL "Darwin")
    add_definitions(-stdlib=libc++)         # Use the modern library on Darwin
  endif()
elseif("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  add_definitions(-std=c++11                # Use the modern language
                  -Wall                     #
                  -Wextra                   #
                  -Wpedantic                # Display every warning possible.
                  )
endif()

#
# Use `make doc` to generate API documentation.
#
find_package(Doxygen)
if(DOXYGEN_FOUND)
  configure_file(${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in
    ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile @ONLY)
  add_custom_target(doc
    ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    COMMENT "Generating API documentation with Doxygen" VERBATIM)
  install(DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/doc/html
          DESTINATION doc)
endif(DOXYGEN_FOUND)


# Adds the include directory to the compiler's search path.
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

# Header files installed with the library.
set(
  LIBRARY_HEADERS
  ${CMAKE_CURRENT_SOURCE_DIR}/include/any.hpp
)

# Builds the test drivers.
enable_testing()

#add_executable(TEST ${CMAKE_CURRENT_SOURCE_DIR}/test/TEST.cpp)
#add_test(TEST TEST)

add_executable(test_any_assign_from_any ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_assign_from_any.cpp)
add_test(test_any_assign_from_any test_any_assign_from_any)

add_executable(test_any_assign_from_const ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_assign_from_const.cpp)
add_test(test_any_assign_from_const test_any_assign_from_const)

add_executable(test_any_assign_from_const_array ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_assign_from_const_array.cpp)
add_test(test_any_assign_from_const_array test_any_assign_from_const_array)

add_executable(test_any_assign_from_object ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_assign_from_object.cpp)
add_test(test_any_assign_from_object test_any_assign_from_object)

add_executable(test_any_assign_from_object_pointer ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_assign_from_object_pointer.cpp)
add_test(test_any_assign_from_object_pointer test_any_assign_from_object_pointer)

add_executable(test_any_construct_any_const ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_construct_any_const.cpp)
add_test(test_any_construct_any_const test_any_construct_any_const)

add_executable(test_any_construct_any_const_array ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_construct_any_const_array.cpp)
add_test(test_any_construct_any_const_array test_any_construct_any_const_array)

add_executable(test_any_construct_any_object ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_construct_any_object.cpp)
add_test(test_any_construct_any_object test_any_construct_any_object)

add_executable(test_any_construct_any_object_pointer ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_construct_any_object_pointer.cpp)
add_test(test_any_construct_any_object_pointer test_any_construct_any_object_pointer)

add_executable(test_any_construct_const ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_construct_const.cpp)
add_test(test_any_construct_const test_any_construct_const)

add_executable(test_any_construct_const_array ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_construct_const_array.cpp)
add_test(test_any_construct_const_array test_any_construct_const_array)

add_executable(test_any_construct_object ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_construct_object.cpp)
add_test(test_any_construct_object test_any_construct_object)

add_executable(test_any_construct_object_pointer ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_construct_object_pointer.cpp)
add_test(test_any_construct_object_pointer test_any_construct_object_pointer)

add_executable(test_any_type ${CMAKE_CURRENT_SOURCE_DIR}/test/test_any_type.cpp)
add_test(test_any_type test_any_type)

