load("//Vendor/rules_pods/BazelExtensions:extensions.bzl", "pch_with_name_hint")
load("//Vendor/rules_pods/BazelExtensions:extensions.bzl", "acknowledged_target")
load("//Vendor/rules_pods/BazelExtensions:extensions.bzl", "gen_module_map")

# Add a config setting release for compilation mode
# Assume that people are using `opt` for release mode
# see the bazel user manual for more information
# https://bazel.build/versions/master/docs/bazel-user-manual.html
native.config_setting(
    name = "release",
    values = {
        "compilation_mode": "opt",
    },
)

config_setting(
    name = "iosCase",
    values = {
        "cpu": "powerpc1",
    },
)

config_setting(
    name = "osxCase",
    values = {
        "cpu": "powerpc2",
    },
)

filegroup(
    name = "PINCache_hdrs",
    srcs = glob(
        [
            "pod_support/Headers/Public/**/*",
        ],
        exclude_directories = 1,
    ),
    visibility = [
        "//visibility:public",
    ],
)

gen_module_map(
    "PINCache",
    "PINCache_module_map",
    "PINCache",
    [
        "PINCache_hdrs",
    ],
)

objc_library(
    name = "PINCache",
    hdrs = [
        "PINCache_module_map_module_map_file",
    ] + [
        "PINCache_hdrs",
    ],
    copts = [
        "-Wnon-modular-include-in-framework-module",
        "-g",
        "-stdlib=libc++",
        "-DCOCOAPODS=1",
        "-DOBJC_OLD_DISPATCH_PROTOTYPES=0",
        "-fdiagnostics-show-note-include-stack",
        "-fno-common",
        "-fembed-bitcode-marker",
        "-fmessage-length=0",
        "-fpascal-strings",
        "-fstrict-aliasing",
        "-Wno-error=nonportable-include-path",
    ] + select(
        {
            "//conditions:default": [
                "-DPOD_CONFIGURATION_RELEASE=0",
            ],
            ":release": [
                "-DPOD_CONFIGURATION_RELEASE=1",
                "-DNS_BLOCK_ASSERTIONS=1",
            ],
        },
    ) + [
        "-IVendor/PINCache/pod_support/Headers/Public/PINCache/",
    ] + [
        "-fmodule-name=PINCache_pod_module",
    ],
    enable_modules = 1,
    includes = [
        "PINCache_module_map",
        "pod_support/Headers/Public/",
    ],
    pch = pch_with_name_hint(
        "PINCache",
        [
        ],
    ),
    sdk_frameworks = [
        "Foundation",
    ],
    visibility = [
        "//visibility:public",
    ],
    weak_sdk_frameworks = select(
        {
            ":osxCase": [
                "AppKit",
            ],
            "//conditions:default": [
                "UIKit",
            ],
        },
    ),
    deps = [
        ":Arc-exception-safe",
        ":Core",
    ],
)

acknowledged_target(
    name = "PINCache_acknowledgement",
    value = "//Vendor/PINCache/pod_support_buildable:acknowledgement_fragment",
    deps = [
    ],
)

filegroup(
    name = "Core_hdrs",
    srcs = glob(
        [
            "Source/*.h",
        ],
        exclude_directories = 1,
    ),
    visibility = [
        "//visibility:public",
    ],
)

objc_library(
    name = "Core",
    srcs = glob(
        [
            "Source/*.m",
        ],
        exclude = [
            "Source/PINDiskCache.m",
        ],
        exclude_directories = 1,
    ) + glob(
        [
            "Source/*.h",
        ],
        exclude_directories = 1,
    ) + [
    ],
    hdrs = [
        "PINCache_module_map_module_map_file",
    ] + [
        "PINCache_hdrs",
    ],
    copts = [
        "-Wnon-modular-include-in-framework-module",
        "-g",
        "-stdlib=libc++",
        "-DCOCOAPODS=1",
        "-DOBJC_OLD_DISPATCH_PROTOTYPES=0",
        "-fdiagnostics-show-note-include-stack",
        "-fno-common",
        "-fembed-bitcode-marker",
        "-fmessage-length=0",
        "-fpascal-strings",
        "-fstrict-aliasing",
        "-Wno-error=nonportable-include-path",
    ] + select(
        {
            "//conditions:default": [
                "-DPOD_CONFIGURATION_RELEASE=0",
            ],
            ":release": [
                "-DPOD_CONFIGURATION_RELEASE=1",
                "-DNS_BLOCK_ASSERTIONS=1",
            ],
        },
    ) + [
        "-IVendor/PINCache/pod_support/Headers/Public/PINCache/",
    ] + [
        "-fmodule-name=PINCache_pod_module",
    ],
    enable_modules = 1,
    includes = [
        "PINCache_module_map",
        "pod_support/Headers/Public/",
    ],
    pch = pch_with_name_hint(
        "PINCache",
        [
            "Source/**/*.pch",
        ],
    ),
    sdk_frameworks = [
        "Foundation",
    ],
    visibility = [
        "//visibility:public",
    ],
    weak_sdk_frameworks = select(
        {
            ":osxCase": [
                "AppKit",
            ],
            "//conditions:default": [
                "UIKit",
            ],
        },
    ),
    deps = [
        "//Vendor/PINOperation",
    ],
)

acknowledged_target(
    name = "Core_acknowledgement",
    value = "//Vendor/PINCache/pod_support_buildable:acknowledgement_fragment",
    deps = [
        "//Vendor/PINOperation:PINOperation_acknowledgement",
    ],
)

filegroup(
    name = "Arc-exception-safe_hdrs",
    srcs = [
    ],
    visibility = [
        "//visibility:public",
    ],
)

objc_library(
    name = "Arc-exception-safe",
    srcs = glob(
        [
            "Source/PINDiskCache.m",
        ],
        exclude_directories = 1,
    ) + [
    ] + [
        ":Core_hdrs",
    ],
    hdrs = [
        "PINCache_module_map_module_map_file",
    ] + [
        "PINCache_hdrs",
    ],
    copts = [
        "-fobjc-arc-exceptions",
        "-Wnon-modular-include-in-framework-module",
        "-g",
        "-stdlib=libc++",
        "-DCOCOAPODS=1",
        "-DOBJC_OLD_DISPATCH_PROTOTYPES=0",
        "-fdiagnostics-show-note-include-stack",
        "-fno-common",
        "-fembed-bitcode-marker",
        "-fmessage-length=0",
        "-fpascal-strings",
        "-fstrict-aliasing",
        "-Wno-error=nonportable-include-path",
    ] + select(
        {
            "//conditions:default": [
                "-DPOD_CONFIGURATION_RELEASE=0",
            ],
            ":release": [
                "-DPOD_CONFIGURATION_RELEASE=1",
                "-DNS_BLOCK_ASSERTIONS=1",
            ],
        },
    ) + [
        "-IVendor/PINCache/pod_support/Headers/Public/PINCache/",
    ] + [
        "-fmodule-name=PINCache_pod_module",
    ],
    enable_modules = 1,
    includes = [
        "PINCache_module_map",
        "pod_support/Headers/Public/",
    ],
    pch = pch_with_name_hint(
        "PINCache",
        [
            "Source/**/*.pch",
        ],
    ),
    sdk_frameworks = [
        "Foundation",
    ],
    visibility = [
        "//visibility:public",
    ],
    weak_sdk_frameworks = select(
        {
            ":osxCase": [
                "AppKit",
            ],
            "//conditions:default": [
                "UIKit",
            ],
        },
    ),
    deps = [
        ":Core",
    ],
)

acknowledged_target(
    name = "Arc-exception-safe_acknowledgement",
    value = "//Vendor/PINCache/pod_support_buildable:acknowledgement_fragment",
    deps = [
    ],
)
