load("@bazel_gazelle//:def.bzl", "gazelle")

# gazelle:prefix test_tflogger
gazelle(name = "gazelle")

gazelle(
    name = "gazelle-update-repos",
    args = [
        "-from_file=go.mod",
        "-to_macro=deps.bzl%go_dependencies",
        "-prune",
        # "-build_file_proto_mode=disable_global",
    ],
    command = "update-repos",
)
