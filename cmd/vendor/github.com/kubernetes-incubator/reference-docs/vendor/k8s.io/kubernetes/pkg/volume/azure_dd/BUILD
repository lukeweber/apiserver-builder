package(default_visibility = ["//visibility:public"])

load(
    "@io_bazel_rules_go//go:def.bzl",
    "go_library",
    "go_test",
)

go_library(
    name = "go_default_library",
    srcs = [
        "attacher.go",
        "azure_common.go",
        "azure_common_unsupported.go",
        "azure_dd.go",
        "azure_mounter.go",
        "azure_provision.go",
    ] + select({
        "@io_bazel_rules_go//go/platform:linux_amd64": [
            "azure_common_linux.go",
        ],
        "@io_bazel_rules_go//go/platform:windows_amd64": [
            "azure_common_windows.go",
        ],
        "//conditions:default": [],
    }),
    importpath = "k8s.io/kubernetes/pkg/volume/azure_dd",
    deps = [
        "//vendor/github.com/Azure/azure-sdk-for-go/arm/compute:go_default_library",
        "//vendor/github.com/Azure/azure-sdk-for-go/arm/storage:go_default_library",
        "//vendor/github.com/golang/glog:go_default_library",
        "//vendor/k8s.io/api/core/v1:go_default_library",
        "//vendor/k8s.io/apimachinery/pkg/api/resource:go_default_library",
        "//vendor/k8s.io/apimachinery/pkg/apis/meta/v1:go_default_library",
        "//vendor/k8s.io/apimachinery/pkg/types:go_default_library",
        "//vendor/k8s.io/apimachinery/pkg/util/sets:go_default_library",
        "//vendor/k8s.io/apimachinery/pkg/util/wait:go_default_library",
        "//vendor/k8s.io/kubernetes/pkg/api:go_default_library",
        "//vendor/k8s.io/kubernetes/pkg/cloudprovider:go_default_library",
        "//vendor/k8s.io/kubernetes/pkg/cloudprovider/providers/azure:go_default_library",
        "//vendor/k8s.io/kubernetes/pkg/util/keymutex:go_default_library",
        "//vendor/k8s.io/kubernetes/pkg/util/mount:go_default_library",
        "//vendor/k8s.io/kubernetes/pkg/util/strings:go_default_library",
        "//vendor/k8s.io/kubernetes/pkg/volume:go_default_library",
        "//vendor/k8s.io/kubernetes/pkg/volume/util:go_default_library",
        "//vendor/k8s.io/kubernetes/pkg/volume/util/volumehelper:go_default_library",
    ],
)

filegroup(
    name = "package-srcs",
    srcs = glob(["**"]),
    tags = ["automanaged"],
    visibility = ["//visibility:private"],
)

filegroup(
    name = "all-srcs",
    srcs = [":package-srcs"],
    tags = ["automanaged"],
)

go_test(
    name = "go_default_test",
    srcs = [
        "azure_common_test.go",
        "azure_dd_test.go",
    ],
    importpath = "k8s.io/kubernetes/pkg/volume/azure_dd",
    library = ":go_default_library",
    deps = [
        "//vendor/k8s.io/api/core/v1:go_default_library",
        "//vendor/k8s.io/client-go/util/testing:go_default_library",
        "//vendor/k8s.io/kubernetes/pkg/util/mount:go_default_library",
        "//vendor/k8s.io/kubernetes/pkg/volume:go_default_library",
        "//vendor/k8s.io/kubernetes/pkg/volume/testing:go_default_library",
    ],
)
