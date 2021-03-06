set(BASE "${CMAKE_CURRENT_SOURCE_DIR}")

set(
    SOURCES
    "${BASE}/build.cpp"
    "${BASE}/convert.cpp"
    "${BASE}/entwine.cpp"
    "${BASE}/merge.cpp"
    "${BASE}/scan.cpp"
    "${BASE}/update.cpp"
)

set(CMAKE_THREAD_PREFER_PTHREAD TRUE)
find_package(Threads REQUIRED)

add_executable(app ${SOURCES})
add_dependencies(app entwine)

target_link_libraries(app
    entwine
    ${Backtrace_LIBRARIES}
    ${CMAKE_DL_LIBS}
    ${CMAKE_THREAD_LIBS_INIT}
)
set_target_properties(app PROPERTIES OUTPUT_NAME entwine)

install(TARGETS app DESTINATION bin)

