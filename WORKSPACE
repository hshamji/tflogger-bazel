workspace(name = "test_tflogger")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "f2dcd210c7095febe54b804bb1cd3a58fe8435a909db2ec04e31542631cf715c",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.31.0/rules_go-v0.31.0.zip",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.31.0/rules_go-v0.31.0.zip",
    ],
)

http_archive(
    name = "bazel_gazelle",
    sha256 = "5982e5463f171da99e3bdaeff8c0f48283a7a5f396ec5282910b9e8a49c0dd7e",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.25.0/bazel-gazelle-v0.25.0.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.25.0/bazel-gazelle-v0.25.0.tar.gz",
    ],
)

http_archive(
    name = "com_google_protobuf",
    sha256 = "b10bf4e2d1a7586f54e64a5d9e7837e5188fc75ae69e36f215eb01def4f9721b",
    strip_prefix = "protobuf-3.15.3",
    url = "https://github.com/protocolbuffers/protobuf/archive/v3.15.3.tar.gz",
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")
load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")
load("//:deps.bzl", "go_dependencies")

# gazelle:repository_macro deps.bzl%go_dependencies
go_dependencies()

go_rules_dependencies()

go_register_toolchains(version = "1.16.5")

gazelle_dependencies()

# Proto Dependencies - https://github.com/bazelbuild/rules_go/blob/0.19.0/go/workspace.rst#proto-dependencies
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

# git_repository(
#     name = "com_google_protobuf",
#     commit = "09745575a923640154bcf307fba8aedff47f240a",
#     remote = "https://github.com/protocolbuffers/protobuf",
#     shallow_since = "1558721209 -0700",
# )

load("@com_google_protobuf//:protobuf_deps.bzl", "protobuf_deps")

protobuf_deps()

# # gRPC Dependencies - https://github.com/bazelbuild/rules_go/blob/0.19.0/go/workspace.rst#grpc-dependencies
# load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies", "go_repository")

# # gazelle_dependencies()

# go_repository(
#     name = "org_golang_google_grpc",
#     build_file_proto_mode = "disable",
#     importpath = "google.golang.org/grpc",
#     sum = "h1:J0UbZOIrCAl+fpTOf8YLs4dJo8L/owV4LYVtAXQoPkw=",
#     version = "v1.22.0",
# )

# go_repository(
#     name = "org_golang_x_net",
#     importpath = "golang.org/x/net",
#     sum = "h1:oWX7TPOiFAMXLq8o0ikBYfCJVlRHBcsciT5bXOrH628=",
#     version = "v0.0.0-20190311183353-d8887717615a",
# )

# go_repository(
#     name = "org_golang_x_text",
#     importpath = "golang.org/x/text",
#     sum = "h1:g61tztE5qeGQ89tm6NTjjM9VPIm088od1l6aSorWRWg=",
#     version = "v0.3.0",
# )

all_content = """filegroup(name = "all", srcs = glob(["**"]), visibility = ["//visibility:public"])"""

http_archive(
    name = "rules_foreign_cc",
    strip_prefix = "rules_foreign_cc-main",
    url = "https://github.com/bazelbuild/rules_foreign_cc/archive/main.zip",
    sha256 = "5969e26dea8b4d715c61a8b359e819ef87f8490e0cc26f19248f916d95903e15",
)

load("@rules_foreign_cc//:workspace_definitions.bzl", "rules_foreign_cc_dependencies")

rules_foreign_cc_dependencies()

http_archive(
    name = "librdkafka",
    build_file_content = """load("@rules_foreign_cc//tools/build_defs:cmake.bzl", "cmake_external")

filegroup(
    name = "sources",
    srcs = glob(["**"]),
)

cmake_external(
    name = "librdkafka",
    cache_entries = {
        "RDKAFKA_BUILD_STATIC": "ON",
        "WITH_ZSTD": "OFF",
        "WITH_SSL": "OFF",
        "WITH_SASL": "OFF",
        "ENABLE_LZ4_EXT": "OFF",
        "WITH_LIBDL": "OFF",
    },
    lib_source = ":sources",
    static_libraries = [
        "librdkafka++.a",
        "librdkafka.a",
    ],
    visibility = ["//visibility:public"],
)
""",
    sha256 = "ae27ea3f3d0d32d29004e7f709efbba2666c5383a107cc45b3a1949486b2eb84",
    strip_prefix = "librdkafka-1.4.0",
    urls = ["https://github.com/edenhill/librdkafka/archive/v1.4.0.tar.gz"],
)