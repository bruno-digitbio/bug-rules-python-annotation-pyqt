workspace(name = "bug-example")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "rules_python",
    sha256 = "e85ae30de33625a63eca7fc40a94fea845e641888e52f32b6beea91e8b1b2793",
    strip_prefix = "rules_python-0.27.1",
    url = "https://github.com/bazelbuild/rules_python/releases/download/0.27.1/rules_python-0.27.1.tar.gz",
)

load("@rules_python//python:repositories.bzl", "py_repositories")

py_repositories()

load("@rules_python//python:repositories.bzl", "python_register_toolchains")

python_register_toolchains(
    name = "python_3_11",
    # Available versions are listed in @rules_python//python:versions.bzl.
    # We recommend using the same version your team is already standardized on.
    python_version = "3.11",
)

load("@python_3_11//:defs.bzl", "interpreter")

load("@rules_python//python:pip.bzl", "package_annotation", "pip_parse")

PIP_ANNOTATIONS = {
    "PyQt6": package_annotation(
        additive_build_content = """# A comment.""",
        copy_files = {
            "@pip_pyqt6_sip//:site-packages/PyQt6/sip.cpython-311-x86_64-linux-gnu.so": "site-packages/PyQt6/sip.cpython-311-x86_64-linux-gnu.so",
        },
    ),
    "wheel": package_annotation(
        additive_build_content = """# A comment.""",
    ),
}

pip_parse(
    name = "pip",
    annotations = PIP_ANNOTATIONS,
    python_interpreter_target = interpreter,
    requirements_darwin = "//:requirements_darwin.txt",
    requirements_windows = "//:requirements_windows.txt",
    requirements_linux = "//:requirements_linux.txt",
)

load("@pip//:requirements.bzl", "install_deps")

install_deps()
