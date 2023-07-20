workspace(name = "platform")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

#-----------------------------------------------------------------------------
# Go Toolchain
#-----------------------------------------------------------------------------
http_archive(
    name = "io_bazel_rules_go",
    sha256 = "16e9fca53ed6bd4ff4ad76facc9b7b651a89db1689a2877d6fd7b82aa824e366",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.34.0/rules_go-v0.34.0.zip",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.34.0/rules_go-v0.34.0.zip",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains(version = "1.18.4")

#-----------------------------------------------------------------------------
# Gazelle Tools
#-----------------------------------------------------------------------------
http_archive(
    name = "bazel_gazelle",
    sha256 = "501deb3d5695ab658e82f6f6f549ba681ea3ca2a5fb7911154b5aa45596183fa",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.26.0/bazel-gazelle-v0.26.0.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.26.0/bazel-gazelle-v0.26.0.tar.gz",
    ],
)

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

gazelle_dependencies()

#-----------------------------------------------------------------------------
# Java Toolchain
#-----------------------------------------------------------------------------
http_archive(
    name = "rules_java",
    sha256 = "d974a2d6e1a534856d1b60ad6a15e57f3970d8596fbb0bb17b9ee26ca209332a",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_java/releases/download/5.1.0/rules_java-5.1.0.tar.gz",
        "https://github.com/bazelbuild/rules_java/releases/download/5.1.0/rules_java-5.1.0.tar.gz",
    ],
)

load("@rules_java//java:repositories.bzl", "rules_java_dependencies", "rules_java_toolchains")

rules_java_dependencies()

rules_java_toolchains()

#-----------------------------------------------------------------------------
# Jvm External to use maven packages
#-----------------------------------------------------------------------------
http_archive(
    name = "rules_jvm_external",
    sha256 = "6cc8444b20307113a62b676846c29ff018402fd4c7097fcd6d0a0fd5f2e86429",
    strip_prefix = "rules_jvm_external-5.3",
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/5.3.zip",
)

load("@rules_jvm_external//:defs.bzl", "maven_install")

#-----------------------------------------------------------------------------
# Proto Toolchain
#-----------------------------------------------------------------------------
http_archive(
    name = "rules_proto",
    sha256 = "e017528fd1c91c5a33f15493e3a398181a9e821a804eb7ff5acdd1d2d6c2b18d",
    strip_prefix = "rules_proto-4.0.0-3.20.0",
    urls = [
        "https://github.com/bazelbuild/rules_proto/archive/refs/tags/4.0.0-3.20.0.tar.gz",
    ],
)

load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")

rules_proto_dependencies()

rules_proto_toolchains()

#-----------------------------------------------------------------------------
# Grpc Toolchain
#-----------------------------------------------------------------------------
http_archive(
    name = "io_grpc_grpc_java",
    sha256 = "fd5f319252eac66920391ceb79b94611cac74de8f1ff7ef51391ee859a2243ea",
    strip_prefix = "grpc-java-1.49.0",
    urls = ["https://github.com/grpc/grpc-java/archive/v1.49.0.tar.gz"],
)

load("@io_grpc_grpc_java//:repositories.bzl", "IO_GRPC_GRPC_JAVA_ARTIFACTS", "IO_GRPC_GRPC_JAVA_OVERRIDE_TARGETS", "grpc_java_repositories")

grpc_java_repositories()

#-----------------------------------------------------------------------------
# Maven packages
#-----------------------------------------------------------------------------
load("//:repositories.bzl", "PLATFORM_JAVA_ARTIFACTS")

maven_install(
    artifacts = PLATFORM_JAVA_ARTIFACTS + IO_GRPC_GRPC_JAVA_ARTIFACTS,
    generate_compat_repositories = True,
    override_targets = IO_GRPC_GRPC_JAVA_OVERRIDE_TARGETS,
    repositories = [
        "https://repo.maven.apache.org/maven2/",
    ],
)

load("@maven//:compat.bzl", "compat_repositories")

compat_repositories()

#-----------------------------------------------------------------------------
# StackB Gazelle setup
#-----------------------------------------------------------------------------
http_archive(
    name = "build_stack_rules_proto",
    sha256 = "16c93fe75314f21f8ef786f27668e2d796400950df1fcd7d249be426420405ac",
    strip_prefix = "rules_proto-9bea22f9fe0bb81c9cbfa855e6bf979faa73f742",
    urls = ["https://github.com/stackb/rules_proto/archive/9bea22f9fe0bb81c9cbfa855e6bf979faa73f742.tar.gz"],
)

register_toolchains("@build_stack_rules_proto//toolchain:prebuilt")

load("@build_stack_rules_proto//:go_deps.bzl", "gazelle_protobuf_extension_go_deps")

gazelle_protobuf_extension_go_deps()

#-----------------------------------------------------------------------------
# JVM Contrib Rules
#-----------------------------------------------------------------------------
http_archive(
    name = "contrib_rules_jvm",
    sha256 = "c15e2208094a3c2de41180c7f7612328c6720758c7c3e8bd8ead448f4048689c",
    strip_prefix = "rules_jvm-9c590479bd2cf1afc2e51e5b5b7a1eb1212c2ab5",
    url = "https://github.com/bazel-contrib/rules_jvm/archive/9c590479bd2cf1afc2e51e5b5b7a1eb1212c2ab5.zip",
)

load("@contrib_rules_jvm//:repositories.bzl", "contrib_rules_jvm_deps", "contrib_rules_jvm_gazelle_deps")

contrib_rules_jvm_deps()

contrib_rules_jvm_gazelle_deps()

load("@contrib_rules_jvm//:setup.bzl", "contrib_rules_jvm_setup")

contrib_rules_jvm_setup()

load("@contrib_rules_jvm//:gazelle_setup.bzl", "contrib_rules_jvm_gazelle_setup")

contrib_rules_jvm_gazelle_setup()
