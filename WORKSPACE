workspace (
    name = "dylan",
    managed_directories = {"@npm": ["node_modules"]},
)

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "f9e7b9f42ae202cc2d2ce6d698ccb49a9f7f7ea572a78fd451696d03ef2ee116",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/1.6.0/rules_nodejs-1.6.0.tar.gz"],
)

load("@build_bazel_rules_nodejs//:index.bzl", "node_repositories")

load("@build_bazel_rules_nodejs//:index.bzl", "yarn_install")

node_repositories(
    package_json = ["//:package.json"],
    node_version = "12.16.3",
    node_repositories = {
        "12.16.3-darwin_amd64": ("node-v12.16.3-darwin-x64.tar.gz", "node-v12.16.3-darwin-x64", "0718812b3ab8e77e8d1354f4d10428ae99d78f721bdcceee527c4b592ea7fed0"),
        "12.16.3-linux_amd64": ("node-v12.16.3-linux-x64.tar.xz", "node-v12.16.3-linux-x64", "1956e196e3c3c8ef5f0c45db76d7c1245af4ccdda2b7ab30a57ce91d6e165caa"),
        "12.16.3-windows_amd64": ("node-v12.16.3-win-x64.zip", "node-v12.16.3-win-x64", "d0bb0e0b1f1a948529ddd543e2cfe0bfe209eb843defc70217b3d2f84cbf3b78"),
    }
)

yarn_install(
    name = "npm",
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)

# Install all bazel dependencies of the @npm npm packages
load("@npm//:install_bazel_dependencies.bzl", "install_bazel_dependencies")
install_bazel_dependencies()

# Set up TypeScript toolchain
load("@npm_bazel_typescript//:index.bzl", "ts_setup_workspace")
ts_setup_workspace()
