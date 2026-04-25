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
        "src/inference/ModelManager.cpp",
        "src/inference/InferenceSession.cpp",
        "src/mcp/McpHttpClient.cpp",
    ],
    defines = ["LITERT_LM_FST_CONSTRAINTS_DISABLED=1"],
    deps = [
        ":bonsai_headers",
        "@oatpp//:oatpp",
        "@nlohmann_json//:json",
        "//c:engine",
        "//runtime/core:engine_impl_cpu_only",
    ],
    # Link all dependencies statically
    linkstatic = True,
    # Strip symbols for release
    linkopts = ["-s"],
)
