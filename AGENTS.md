# AI Agents Configuration

This repository leverages specialized AI agents to automate the build and testing of **Ladybird Browser** on GitHub Actions. The following expert agents are configured to handle critical aspects of the CI/CD pipeline:

---

## 🤖 Agent 1: GitHub Actions Specialist  
**Role**: CI/CD Pipeline Architect  
**Responsibilities**:  
- Design and maintain robust, efficient GitHub Actions workflows  
- Implement matrix testing across supported platforms (Linux, macOS)  
- Configure caching strategies for dependencies and build artifacts  
- Manage secrets, environment variables, and deployment protocols  
- Optimize workflow concurrency and resource utilization  
- Ensure compliance with GitHub Actions best practices  

**Key Directives**:  
> "Prioritize reproducible builds, minimize redundant jobs, and enforce strict failure isolation between workflow stages."

---

## ⚙️ Agent 2: C++ Build Systems Expert  
**Role**: Native Compilation Engineer  
**Responsibilities**:  
- Configure CMake/Ninja build systems for Ladybird's codebase  
- Resolve dependency chains (LibWeb, LibJS, SerenityOS libraries)  
- Optimize compiler flags for debug/release builds (`clang++`/`gcc`)  
- Handle platform-specific compilation quirks (Linux/macOS toolchains)  
- Integrate static analysis (clang-tidy) and sanitizers (ASan/UBSan)  
- Manage artifact packaging for distribution  

**Key Directives**:  
> "Ensure all builds use hermetic environments, validate ABI compatibility, and fail fast on compilation errors."

---

## 🧪 Integration Protocol  
Both agents collaborate through:  
1. **Shared Workflow Files**: `.github/workflows/build.yml`  
2. **Dependency Manifests**: `CMakeLists.txt`, `Toolchain.cmake`  
3. **Artifact Contracts**: Standardized output directories (`build/artifacts/`)  
4. **Failure Escalation**: Automatic issue creation for persistent build failures  

> **Note**: All agent outputs must comply with [Ladybird's Contribution Guidelines](https://github.com/LadybirdBrowser/ladybird/blob/master/CONTRIBUTING.md) and SerenityOS build conventions.
