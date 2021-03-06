licenses(["notice"])  # Apache 2

# Trace driver for LightStep (https://lightstep.com/)

load(
    "//bazel:envoy_build_system.bzl",
    "envoy_cc_extension",
    "envoy_cc_library",
    "envoy_package",
)

envoy_package()

envoy_cc_library(
    name = "lightstep_tracer_lib",
    srcs = [
        "lightstep_tracer_impl.cc",
    ],
    hdrs = [
        "lightstep_tracer_impl.h",
    ],
    external_deps = ["lightstep"],
    deps = [
        "//source/common/config:utility_lib",
        "//source/common/grpc:context_lib",
        "//source/common/stats:symbol_table_lib",
        "//source/common/tracing:http_tracer_lib",
        "//source/extensions/tracers:well_known_names",
        "//source/extensions/tracers/common/ot:opentracing_driver_lib",
    ],
)

envoy_cc_extension(
    name = "config",
    srcs = ["config.cc"],
    hdrs = ["config.h"],
    security_posture = "robust_to_untrusted_downstream",
    deps = [
        ":lightstep_tracer_lib",
        "//source/extensions/tracers:well_known_names",
        "//source/extensions/tracers/common:factory_base_lib",
        "@envoy_api//envoy/config/trace/v2:pkg_cc_proto",
    ],
)
