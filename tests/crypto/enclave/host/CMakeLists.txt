# Copyright (c) Open Enclave SDK contributors.
# Licensed under the MIT License.

set(EDL_FILE ../crypto.edl)

add_custom_command(
  OUTPUT crypto_u.h crypto_u.c
  DEPENDS ${EDL_FILE} edger8r
  COMMAND edger8r --untrusted ${EDL_FILE} --search-path
          ${CMAKE_CURRENT_SOURCE_DIR})

add_executable(cryptohost host.c crypto_u.c)
add_dependencies(cryptohost crypto_test_data)
target_include_directories(cryptohost PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries(cryptohost oehost)
