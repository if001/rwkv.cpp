function(rwkv_add_test source)
    get_filename_component(TEST_TARGET ${source} NAME_WE)
    add_executable(${TEST_TARGET} ${source})
    target_link_libraries(${TEST_TARGET} PRIVATE ggml rwkv)
    add_test(NAME ${TEST_TARGET} COMMAND $<TARGET_FILE:${TEST_TARGET}> ${ARGN})
endfunction()

file(COPY tiny-rwkv-660K-FP32.bin DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
file(COPY tiny-rwkv-660K-FP16.bin DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
file(COPY expected_logits.bin DESTINATION ${CMAKE_CURRENT_BINARY_DIR})

rwkv_add_test(test_ggml_basics.c)
rwkv_add_test(test_Q4_1_O.c)
rwkv_add_test(test_Q4_1_O_large_matmul.c)
rwkv_add_test(test_tiny_rwkv.c)
