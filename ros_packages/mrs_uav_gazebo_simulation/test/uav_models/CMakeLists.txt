get_filename_component(TEST_NAME "${CMAKE_CURRENT_SOURCE_DIR}" NAME)

set(MODELS
  x500
  f330
  f450
  f550
  t650
  m690
  naki
  robofly
  )

catkin_add_executable_with_gtest(test_${TEST_NAME}
  test.cpp
  )

target_link_libraries(test_${TEST_NAME}
  ${catkin_LIBRARIES}
  )

add_dependencies(test_${TEST_NAME}
  ${${PROJECT_NAME}_EXPORTED_TARGETS}
  ${catkin_EXPORTED_TARGETS}
  )

foreach(MODEL ${MODELS})

  add_rostest(${TEST_NAME}.test
      ARGS
      UAV_TYPE:=${MODEL}
    )

endforeach()
