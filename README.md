# Ladybird Builder GitHub Actions

This repository contains GitHub Actions workflows to automatically build and release Ladybird Browser for major Linux distributions.

## Overview

This is a **builder repository** that automatically:
- Clones the official Ladybird Browser source code from [LadybirdBrowser/ladybird](https://github.com/LadybirdBrowser/ladybird)
- Builds Ladybird Browser on Ubuntu and Fedora
- Creates releases with auto-incrementing version tags
- Packages binaries as portable tarballs

## Repository Structure

```
ladybird-builder/
├── .github/
│   ├── actions/
│   │   └── ladybird-build/
│   │       └── action.yml          # Reusable action
│   └── workflows/
│       ├── build-and-release.yml   # Main workflow file
│       └── workflow-config.json    # Configuration documentation
├── scripts/                        # Helper scripts
├── README.md                       # Main documentation
├── CODEOWNERS                      # Review requirements
└── LICENSE                         # License file
```

## Workflow Features

### Triggers

| Event | Branch/Schedule | Description |
|-------|-----------------|-------------|
| Push | main, master | Automatic build on main branch changes |
| Schedule | `0 0,12 * * *` | Twice daily at 00:00 and 12:00 UTC |
| Workflow Dispatch | - | Manual build with version input |

### Concurrency

- Same-branch pushes cancel in-progress builds
- Prevents resource waste from rapid commits

### Timeout Limits

| Job | Timeout |
|-----|---------|
| Build (Ubuntu/Fedora) | 6 hours |
| Release Creation | 30 minutes |

## Artifact Structure

Both Ubuntu and Fedora builds produce portable tarballs:

```
ladybird-{platform}.tar.gz
└── dist
    ├── bin
    │   ├── BenchmarkJPEGLoader
    │   ├── BindingsGenerator
    │   ├── dns
    │   ├── GenerateAriaRoles
    │   ├── GenerateCSSDescriptors
    │   ├── GenerateCSSEnums
    │   ├── GenerateCSSEnvironmentVariable
    │   ├── GenerateCSSKeyword
    │   ├── GenerateCSSMathFunctions
    │   ├── GenerateCSSMediaFeatureID
    │   ├── GenerateCSSNumericFactoryMethods
    │   ├── GenerateCSSPropertyID
    │   ├── GenerateCSSPseudoClass
    │   ├── GenerateCSSPseudoElement
    │   ├── GenerateCSSStyleProperties
    │   ├── GenerateCSSTransformFunctions
    │   ├── GenerateCSSUnits
    │   ├── GenerateNamedCharacterReferences
    │   ├── GenerateWindowOrWorkerInterfaces
    │   ├── image
    │   ├── IPCCompiler
    │   ├── IPCMagicLinter
    │   ├── js
    │   ├── Ladybird
    │   ├── test262-runner
    │   ├── test-js
    │   ├── test-js-bytecode
    │   ├── test-value-js
    │   ├── test-wasm
    │   ├── test-web
    │   ├── wasm
    │   ├── WebDriver
    │   └── xml
    ├── lib/
    │   └── lib*.so*
    ├── libexec
    │   ├── ImageDecoder
    │   ├── RequestServer
    │   ├── WebContent
    │   └── WebWorker
    └── share
        └── ladybird
            └── res
                ├── fonts
                ├── icons
                ├── ladybird
                └── themes

```

### RPATH Configuration

All binaries are configured with `$ORIGIN/../lib` RPATH, making them portable without system library installation.

## Related Projects

- [Ladybird Browser](https://github.com/LadybirdBrowser/ladybird) - Official repository
- [Ladybird Documentation](https://github.com/LadybirdBrowser/ladybird/blob/master/Documentation/BuildInstructionsLadybird.md) - Official build instructions
- [SerenityOS](https://github.com/SerenityOS/serenity) - Parent project
