
find_package(CapnProto REQUIRED)
include_directories(${CAPNP_INCLUDE_DIRS})
add_definitions(${CAPNP_DEFINITIONS})

set(CAPNPC_OUTPUT_DIR ${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CAPNPC_OUTPUT_DIR})

capnp_generate_cpp(CAPNP_ADDR_SRCS CAPNP_ADDR_HDRS addressbook.capnp)
capnp_generate_cpp(CAPNP_CALC_SRCS CAPNP_CALC_HDRS calculator.capnp)

add_executable(capnp-sample-addressbook addressbook.c++ ${CAPNP_ADDR_SRCS} ${CAPNP_ADDR_HDRS})
target_link_libraries(capnp-sample-addressbook ${CAPNP_LIBRARIES})

add_executable(capnp-sample-calculator-server calculator-server.c++ ${CAPNP_CALC_SRCS} ${CAPNP_CALC_HDRS})
target_link_libraries(capnp-sample-calculator-server ${CAPNP_LIBRARIES})

add_executable(capnp-sample-calculator-client calculator-client.c++ ${CAPNP_CALC_SRCS} ${CAPNP_CALC_HDRS})
target_link_libraries(capnp-sample-calculator-client ${CAPNP_LIBRARIES})
