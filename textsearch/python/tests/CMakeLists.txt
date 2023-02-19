function(textsearch_add_py_test source)
  get_filename_component(name ${source} NAME_WE)
  set(name "${name}_py")
  message(STATUS "name: ${name}")

  add_test(NAME ${name}
    COMMAND
      "${PYTHON_EXECUTABLE}"
      "${CMAKE_CURRENT_SOURCE_DIR}/${source}"
  )

  get_filename_component(textsearch_path ${CMAKE_CURRENT_LIST_DIR} DIRECTORY)

  set_property(TEST ${name}
    PROPERTY ENVIRONMENT "PYTHONPATH=${textsearch_path}:$<TARGET_FILE_DIR:_fasttextsearch>:$ENV{PYTHONPATH}"
  )
endfunction()

if(LILCOM_ENABLE_TESTS)
  set(test_srcs
    test_suffix_array.py
  )

  foreach(source IN LISTS test_srcs)
    textsearch_add_py_test(${source})
  endforeach()
endif()