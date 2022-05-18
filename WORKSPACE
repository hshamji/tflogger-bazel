workspace(name = "test_tflogger")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "8e968b5fcea1d2d64071872b12737bbb5514524ee5f0a4f54f5920266c261acb",
    url = "https://github.com/bazelbuild/rules_go/releases/download/v0.28.0/rules_go-v0.28.0.zip",
)

http_archive(
    name = "bazel_gazelle",
    sha256 = "62ca106be173579c0a167deb23358fdfe71ffa1e4cfdddf5582af26520f1c66f",
    url = "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.23.0/bazel-gazelle-v0.23.0.tar.gz",
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
