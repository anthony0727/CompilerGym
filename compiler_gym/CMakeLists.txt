# Copyright (c) Facebook, Inc. and its affiliates.
#
# This source code is licensed under the MIT license found in the
# LICENSE file in the root directory of this source tree.

cg_add_all_subdirs()

if(COMPILER_GYM_ENABLE_LLVM_ENV)
    list(APPEND MAKE_CONFIG_OPTS " --enable-llvm-env")
endif()
if(COMPILER_GYM_ENABLE_MLIR_ENV)
    list(APPEND MAKE_CONFIG_OPTS " --enable-mlir-env")
endif()
execute_process(
    COMMAND
        bash -c
        "\"${CMAKE_CURRENT_SOURCE_DIR}/make_config.py\" --out-file-path \"${CMAKE_CURRENT_BINARY_DIR}/config.py\" ${MAKE_CONFIG_OPTS}"
    OUTPUT_VARIABLE _PY_PGK_FILE_NAME
    COMMAND_ERROR_IS_FATAL ANY
)
set_property(DIRECTORY APPEND PROPERTY CMAKE_CONFIGURE_DEPENDS make_config.py)

cg_py_library(
  NAME
    compiler_gym
  SRCS
    "__init__.py"
  DEPS
    ::random_replay
    ::random_search
    ::validate
    compiler_gym::bin::bin
    compiler_gym::datasets::datasets
    compiler_gym::envs::envs
    compiler_gym::errors::errors
    compiler_gym::leaderboard::leaderboard
    compiler_gym::service::service
    compiler_gym::spaces::spaces
    compiler_gym::util::util
    compiler_gym::util::flags::flags
    compiler_gym::wrappers::wrappers
  PUBLIC
)

cg_py_library(
  NAME
    compiler_env_state
  SRCS
    "compiler_env_state.py"
  DEPS
    compiler_gym::datasets::uri
    compiler_gym::util::util
  PUBLIC
)

cg_py_library(
  NAME
    random_replay
  SRCS
    "random_replay.py"
  DEPS
    ::random_search
    compiler_gym::envs::envs
    compiler_gym::util::util
  PUBLIC
)

cg_py_library(
  NAME
    random_search
  SRCS
    "random_search.py"
  DEPS
    compiler_gym::envs::envs
    compiler_gym::errors::errors
    compiler_gym::util::util
  PUBLIC
)

cg_py_library(
  NAME
    validate
  SRCS
    "validate.py"
  DEPS
    ::validation_error
    ::validation_result
    compiler_gym::service::client_service_compiler_env
    compiler_gym::spaces::spaces
    compiler_gym::util::util
  PUBLIC
)

cg_py_library(
  NAME
    validation_error
  SRCS
    "validation_error.py"
  DEPS
    compiler_gym::errors::errors
  PUBLIC
)

cg_py_library(
  NAME
    validation_result
  SRCS
    "validation_result.py"
  DEPS
    ::compiler_env_state
    compiler_gym::errors::errors
    ::validation_error
    compiler_gym::util::util
  PUBLIC
)

set(_PY_PKG_IN_DIR "${CMAKE_CURRENT_BINARY_DIR}/..")
cmake_path(RELATIVE_PATH _PY_PKG_IN_DIR BASE_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/..")
set(_PY_PKG_OUT_DIR "${CMAKE_CURRENT_BINARY_DIR}/../py_pkg")
string(
    CONCAT
    _CMD
    "cd \"${CMAKE_CURRENT_SOURCE_DIR}/..\""
    " && \"${Python3_EXECUTABLE}\" setup.py"
    " --build-dir \"${_PY_PKG_OUT_DIR}/build\""
    " bdist_wheel"
    " --package-dir \"${_PY_PKG_IN_DIR}\""
    " --dist-dir \"${_PY_PKG_OUT_DIR}/dist\""
    " --bdist-dir \"${_PY_PKG_OUT_DIR}/bdist\""
)
string(CONCAT _CMD_GET_WHEEL_FILENAME "${_CMD}" " --get-wheel-filename")
execute_process(
    COMMAND bash -c "${_CMD_GET_WHEEL_FILENAME}"
    OUTPUT_VARIABLE _PY_PGK_FILE_NAME
    COMMAND_ERROR_IS_FATAL ANY
)
set_property(DIRECTORY APPEND PROPERTY CMAKE_CONFIGURE_DEPENDS ../setup.py)

string(CONCAT _BUILD_CMD "rm -rf \"${_PY_PKG_OUT_DIR}/build\"" " && ${_CMD}")
set(PY_PKG_DEPS
    compiler_gym::compiler_gym
    compiler_gym::bin::bin
    compiler_gym::datasets::datasets
    compiler_gym::envs::envs
    compiler_gym::service::service
    compiler_gym::service::runtime::runtime
    compiler_gym::spaces::spaces
    compiler_gym::util::util
    compiler_gym::util::flags::flags
    compiler_gym::views::views
)
if(COMPILER_GYM_ENABLE_LLVM_ENV)
    list(
        APPEND
        PY_PKG_DEPS
        compiler_gym::third_party::cbench::benchmarks_list
        compiler_gym::third_party::cbench::crc32
    )
endif()
cg_genrule(
  NAME python_package
  COMMAND "${_BUILD_CMD}"
  SRCS "${CMAKE_CURRENT_SOURCE_DIR}/../setup.py"
  OUTS "${_PY_PKG_OUT_DIR}/dist/${_PY_PGK_FILE_NAME}"
  DEPENDS ${PY_PKG_DEPS}
)

string(
    CONCAT
    _CMD
    "\"${Python3_EXECUTABLE}\" -m pip install --upgrade --no-deps --force-reinstall"
    " \"${_PY_PKG_OUT_DIR}/dist/${_PY_PGK_FILE_NAME}\""
)
cg_genrule(
  NAME install_python_package
  COMMAND "${_CMD}"
  DEPENDS ::python_package
  EXCLUDE_FROM_ALL
)
