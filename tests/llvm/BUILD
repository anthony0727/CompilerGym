# Copyright (c) Facebook, Inc. and its affiliates.
#
# This source code is licensed under the MIT license found in the
# LICENSE file in the root directory of this source tree.
load("@rules_python//python:defs.bzl", "py_test")

py_test(
    name = "action_space_test",
    srcs = ["action_space_test.py"],
    deps = [
        "//compiler_gym/envs",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "all_actions_single_step_test",
    timeout = "long",
    srcs = ["all_actions_single_step_test.py"],
    shard_count = 8,
    deps = [
        "//compiler_gym/envs",
        "//compiler_gym/errors",
        "//compiler_gym/third_party/autophase",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "autophase_test",
    timeout = "short",
    srcs = ["autophase_test.py"],
    deps = [
        "//compiler_gym/envs",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "compute_observation_test",
    srcs = ["compute_observation_test.py"],
    deps = [
        "//compiler_gym/envs/llvm",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "custom_benchmarks_test",
    srcs = ["custom_benchmarks_test.py"],
    data = [
        "invalid_ir.ll",
        "//compiler_gym/third_party/cbench:crc32",
    ],
    deps = [
        "//compiler_gym/envs",
        "//compiler_gym/errors",
        "//compiler_gym/service/proto",
        "//compiler_gym/util",
        "//tests:test_main",
        "//tests/pytest_plugins:common",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "datasets_pickle_test",
    timeout = "long",
    srcs = ["datasets_pickle_test.py"],
    deps = [
        "//compiler_gym/datasets",
        "//compiler_gym/envs/llvm",
        "//tests:test_main",
        "//tests/pytest_plugins:common",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "download_llvm_test",
    srcs = ["download_llvm_test.py"],
    deps = [
        "//compiler_gym/third_party/llvm",
        "//compiler_gym/util",
        "//tests:test_main",
        "//tests/pytest_plugins:common",
    ],
)

py_test(
    name = "episode_reward_test",
    timeout = "long",
    srcs = ["episode_reward_test.py"],
    deps = [
        "//compiler_gym/envs",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "fork_env_test",
    timeout = "long",
    srcs = ["fork_env_test.py"],
    data = [
        "//compiler_gym/third_party/cbench:crc32",
    ],
    deps = [
        "//compiler_gym/envs",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "fork_regression_test",
    timeout = "long",
    srcs = ["fork_regression_test.py"],
    deps = [
        "//compiler_gym/envs",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "fresh_environment_observation_reward_test",
    timeout = "long",
    srcs = ["fresh_environment_observation_reward_test.py"],
    shard_count = 12,
    deps = [
        "//compiler_gym/envs",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "fuzzing_regression_test",
    srcs = ["fuzzing_regression_test.py"],
    deps = [
        "//tests:test_main",
        "//tests/pytest_plugins:common",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "gym_interface_compatability_test",
    timeout = "short",
    srcs = ["gym_interface_compatability_test.py"],
    deps = [
        "//compiler_gym/envs/llvm",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "invalid_ir_test",
    srcs = ["invalid_ir_test.py"],
    data = ["invalid_ir.ll"],
    deps = [
        "//compiler_gym/errors",
        "//compiler_gym/util",
        "//tests:test_main",
        "//tests/pytest_plugins:common",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "llvm_benchmark_test",
    srcs = ["llvm_benchmark_test.py"],
    deps = [
        "//compiler_gym/envs",
        "//compiler_gym/service/proto",
        "//tests:test_main",
        "//tests/pytest_plugins:common",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "llvm_env_test",
    srcs = ["llvm_env_test.py"],
    shard_count = 4,
    deps = [
        "//compiler_gym",
        "//tests:test_main",
        "//tests/pytest_plugins:common",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "llvm_session_parameters_test",
    srcs = ["llvm_session_parameters_test.py"],
    deps = [
        "//compiler_gym/envs",
        "//compiler_gym/errors",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "module_id_test",
    timeout = "short",
    srcs = ["module_id_test.py"],
    deps = [
        "//compiler_gym",
        "//tests:test_main",
        "//tests/pytest_plugins:common",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "multiprocessing_test",
    srcs = ["multiprocessing_test.py"],
    flaky = 1,
    deps = [
        "//compiler_gym",
        "//tests:test_main",
        "//tests/pytest_plugins:common",
    ],
)

py_test(
    name = "observation_spaces_test",
    srcs = ["observation_spaces_test.py"],
    deps = [
        "//compiler_gym/envs",
        "//tests:test_main",
        "//tests/pytest_plugins:common",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "reward_spaces_test",
    srcs = ["reward_spaces_test.py"],
    deps = [
        "//compiler_gym/envs",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "runtime_test",
    timeout = "long",
    srcs = ["runtime_test.py"],
    deps = [
        "//compiler_gym/envs/llvm",
        "//compiler_gym/service:connection",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "service_connection_test",
    srcs = ["service_connection_test.py"],
    deps = [
        "//compiler_gym",
        "//compiler_gym/envs",
        "//compiler_gym/errors",
        "//compiler_gym/third_party/autophase",
        "//compiler_gym/util",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "threading_test",
    timeout = "short",
    srcs = ["threading_test.py"],
    flaky = 1,
    deps = [
        "//compiler_gym",
        "//tests:test_main",
    ],
)

py_test(
    name = "validate_test",
    timeout = "moderate",
    srcs = ["validate_test.py"],
    deps = [
        "//compiler_gym",
        "//compiler_gym/datasets",
        "//compiler_gym/envs",
        "//tests:test_main",
        "//tests/pytest_plugins:llvm",
    ],
)

py_test(
    name = "validation_regression_test",
    timeout = "long",
    srcs = ["validation_regression_test.py"],
    shard_count = 4,
    deps = [
        "//compiler_gym",
        "//tests:test_main",
        "//tests/pytest_plugins:common",
        "//tests/pytest_plugins:llvm",
    ],
)
