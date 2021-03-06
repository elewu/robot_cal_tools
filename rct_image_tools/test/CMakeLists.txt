find_package(GTest REQUIRED)

# ChArUco detection unit test
add_executable(${PROJECT_NAME}_charuco_test charuco_test.cpp)
target_link_libraries(${PROJECT_NAME}_charuco_test
    PRIVATE
    ${PROJECT_NAME}
    GTest::GTest
    GTest::Main
)
rct_gtest_discover_tests(${PROJECT_NAME}_charuco_test)
add_dependencies(${PROJECT_NAME}_charuco_test ${PROJECT_NAME})
add_dependencies(run_tests ${PROJECT_NAME}_charuco_test)
target_compile_definitions(${PROJECT_NAME}_charuco_test PUBLIC TEST_SUPPORT_DIR="${CMAKE_CURRENT_SOURCE_DIR}/images/")

# Install the test executables so they can be run independently later if needed
install(
  TARGETS
    ${PROJECT_NAME}_charuco_test
  RUNTIME DESTINATION bin/tests
  LIBRARY DESTINATION lib/tests
  ARCHIVE DESTINATION lib/tests
)
