add_executable(timeServerSSL timeServerSSL.c)

find_package(OpenSSL REQUIRED)
if (NOT OPENSSL_FOUND)
    message(FATAL_ERROR "OpenSSL not found")
endif()

target_include_directories(timeServerSSL PRIVATE ${OPENSSL_INCLUDE_DIR})
message(STATUS "OpenSSL include directory: ${OPENSSL_INCLUDE_DIR}")

if (WIN32)
    target_link_libraries(timeServerSSL PRIVATE ${OPENSSL_LIBRARIES} ws2_32)
    message(STATUS "OpenSSL libraries: ${OPENSSL_LIBRARIES}")
else()
    target_link_libraries(timeServerSSL PRIVATE ${OPENSSL_LIBRARIES})
    message(STATUS "OpenSSL libraries: ${OPENSSL_LIBRARIES}")
endif()
