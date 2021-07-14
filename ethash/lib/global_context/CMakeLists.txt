# ethash: C/C++ implementation of Ethash, the Ethereum Proof of Work algorithm.
# Copyright 2021 Pawel Bylica.
# Licensed under the Apache License, Version 2.0.

add_library(global-context STATIC)
add_library(ethash::global-context ALIAS global-context)
target_link_libraries(global-context PUBLIC ethash::ethash)
target_include_directories(global-context PUBLIC ${PROJECT_SOURCE_DIR}/include)
set_target_properties(global-context PROPERTIES OUTPUT_NAME ethash-global-context)
target_sources(global-context PRIVATE
    ${PROJECT_SOURCE_DIR}/include/ethash/global_context.h
    ${PROJECT_SOURCE_DIR}/include/ethash/global_context.hpp
    global_context.cpp
)

if(CABLE_COMPILER_GNULIKE AND NOT SANITIZE MATCHES undefined)
    target_compile_options(global-context PRIVATE $<$<COMPILE_LANGUAGE:CXX>:-fno-rtti>)
endif()
