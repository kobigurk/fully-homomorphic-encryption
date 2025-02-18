load("//transpiler:fhe.bzl", "fhe_cc_library")
load("@bazel_skylib//:bzl_library.bzl", "bzl_library")

licenses(["notice"])

_PRIMITIVE_TYPES = [
    "array",
    "char",
    "int",
    "long",
]

[
    fhe_cc_library(
        name = "%s_tfhe" % i,
        src = "%s.cc" % i,
        hdrs = [],
        num_opt_passes = 2,
    )
    for i in _PRIMITIVE_TYPES
]

cc_library(
    name = "test_util",
    testonly = True,
    srcs = ["test_util.cc"],
    hdrs = ["test_util.h"],
    visibility = [
        "//:__subpackages__",
    ],
    deps = [
        "//transpiler/data:fhe_data",
        "@com_google_absl//absl/memory",
        "@com_google_googletest//:gtest",
        "@com_google_xls//xls/common/status:matchers",
    ],
)

cc_test(
    name = "types_test",
    srcs = ["types_test.cc"],
    shard_count = 4,
    deps = [":%s_tfhe" % i for i in _PRIMITIVE_TYPES] + [
        ":test_util",
        "@com_google_googletest//:gtest_main",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/container:fixed_array",
        "@com_google_absl//absl/strings",
        "@com_google_xls//xls/common/status:matchers",
        "//transpiler/data:fhe_data",
        "@tfhe//:libtfhe",
    ],
)

_CONTROL_STRUCTURE = [
    "if",
    "for",
    "function",
    "nested_for",
    "switch",
]

[
    fhe_cc_library(
        name = "%s_tfhe" % i,
        src = "%s.cc" % i,
        hdrs = [],
        num_opt_passes = 2,
    )
    for i in _CONTROL_STRUCTURE
]

cc_test(
    name = "control_structure_test",
    size = "medium",
    srcs = ["control_structure_test.cc"],
    shard_count = 8,
    deps = [":%s_tfhe" % i for i in _CONTROL_STRUCTURE] + [
        ":test_util",
        "@com_google_googletest//:gtest_main",
        "@com_google_absl//absl/base",
        "@com_google_absl//absl/container:fixed_array",
        "@com_google_absl//absl/strings",
        "@com_google_xls//xls/common/status:matchers",
        "//transpiler/data:fhe_data",
        "@tfhe//:libtfhe",
    ],
)

fhe_cc_library(
    name = "function_bool",
    src = "function.cc",
    hdrs = [],
    num_opt_passes = 1,
    transpiler_type = "bool",
)

fhe_cc_library(
    name = "out_params_bool",
    src = "out_params.cc",
    hdrs = [],
    transpiler_type = "bool",
)

fhe_cc_library(
    name = "out_params_with_return_bool",
    src = "out_params_with_return.cc",
    hdrs = [],
    transpiler_type = "bool",
)

fhe_cc_library(
    name = "single_out_param_bool",
    src = "single_out_param.cc",
    hdrs = [],
    transpiler_type = "bool",
)

fhe_cc_library(
    name = "single_out_param_with_return_bool",
    src = "single_out_param_with_return.cc",
    hdrs = [],
    transpiler_type = "bool",
)

cc_test(
    name = "out_params_test",
    srcs = ["out_params_test.cc"],
    deps = [
        ":out_params_bool",
        ":out_params_with_return_bool",
        ":single_out_param_bool",
        ":single_out_param_with_return_bool",
        "//transpiler/data:boolean_data",
        "@com_google_absl//absl/base",
        "@com_google_googletest//:gtest_main",
        "@com_google_xls//xls/common/status:matchers",
    ],
)
