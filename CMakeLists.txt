# Copyright 2018 Glen Joseph Fernandes
# (glenjofe@gmail.com)
#
# Distributed under the Boost Software License, Version 1.0.
# (http://www.boost.org/LICENSE_1_0.txt)

if(NOT DEFINED IDF_TARGET)

cmake_minimum_required(VERSION 3.5...3.20)

project(boost_concept_check VERSION "${BOOST_SUPERPROJECT_VERSION}" LANGUAGES CXX)

add_library(boost_concept_check INTERFACE)

add_library(Boost::concept_check ALIAS boost_concept_check)

target_include_directories(boost_concept_check INTERFACE include)

target_link_libraries(boost_concept_check INTERFACE
    Boost::config
    Boost::preprocessor
    Boost::static_assert
    Boost::type_traits
)

else()

FILE(GLOB_RECURSE headers include/*.h include/*.hpp)

idf_component_register(
    SRCS
        ${headers}
    INCLUDE_DIRS
        include
    REQUIRES
        boost_config
        boost_preprocessor
        boost_static_assert
        boost_type_traits
)

endif()
