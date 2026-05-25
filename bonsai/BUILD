# BonsAI Monolithic Build

cc_library(
    name = "bonsai_headers",
    hdrs = glob(["include/**/*.hpp"]),
    includes = ["include"],
    visibility = ["//visibility:private"],
)

cc_binary(
    name = "bonsai",
    srcs = [
        "src/main.cpp",
        "src/ServerRunner.cpp",
        "src/inference/ModelManager.cpp",
        "src/inference/InferenceSession.cpp",
        "src/mcp/McpHttpClient.cpp",
    ],
    defines = [
        "LITERT_LM_FST_CONSTRAINTS_DISABLED=1",
        "LITERT_DISABLE_OPENCL_SUPPORT=1",
    ],
    deps = [
        ":bonsai_headers",
        "//runtime/components/constrained_decoding:gemma_model_constraint_provider_stub",
        "@oatpp//:oatpp",
        "@nlohmann_json//:json",
        "//c:engine",
    ],
    # Link all dependencies statically
    linkstatic = True,
    linkopts = select({
        "@platforms//os:android": [
            "-latomic",
            "-ldl",
        ],
        "//conditions:default": [
            "-lrt",
            "-latomic",
            "-lpthread",
            "-ldl",
            "-Wl,--export-dynamic-symbol=LiteRt*",
        ],
    }),
)

cc_binary(
    name = "libbonsai_jni.so",
    srcs = [
        "src/jni/bonsai_jni.cpp",
        "src/ServerRunner.cpp",
        "src/inference/ModelManager.cpp",
        "src/inference/InferenceSession.cpp",
        "src/mcp/McpHttpClient.cpp",
    ],
    defines = [
        "LITERT_LM_FST_CONSTRAINTS_DISABLED=1",
        "LITERT_DISABLE_OPENCL_SUPPORT=1",
    ],
    deps = [
        ":bonsai_headers",
        "//runtime/components/constrained_decoding:gemma_model_constraint_provider_stub",
        "@oatpp//:oatpp",
        "@nlohmann_json//:json",
        "//c:engine",
    ],
    linkshared = True,
    linkopts = select({
        "@platforms//os:android": [
            "-llog",
            "-landroid",
        ],
        "//conditions:default": [],
    }),
)
