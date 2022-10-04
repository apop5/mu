# Requirements for contributing Source Code

## Basics

1. Make sure it follows the package, repo, and codebase rules
2. Make sure it builds
3. Write sa unit test for it.  Test positive cases as well as negative cases.
4. Make sure it has docs.  Even a minimal readme.md will get collected and added to the docs.
5. Make sure it has only valid characters encoded (often copy paste from Microsoft Word docs or the internet will lead
   to invalid characters)
6. Any changes made to code that originates from outside Project Mu (e.g. upstream project TianoCore, OpenSSL, etc.)
   should be surrounded with comments/tags indicating that it is a "MU_CHANGE".
    - Most of the contents of `mu_basecore`, `mu_tiano_plus`, `mu_silicon_arm_tiano`, and `mu_silicon_intel_tiano`
      fall under this requirement.
    - Example:

    ```c
    EFI_STATUS
    EFIAPI
    SomeFunction (
            VOID
            )
        {
            EFI_STATUS      Status;
            // MU_CHANGE [BEGIN] - Add new counters for Feature X
            UINTN           CounterA;
            UINTN           CounterB;
            // MU_CHANGE [END]

            Status = EFI_ABORTED;
            ...
        }
    ```

## Repositories

[Repo Philosophy](docs/overview.md#repo-philosophy)

- Repositories should have a clear owner
- Repositories should have a clear target
    -Cross platform/single platform
    -Cross architecture/single architecture
    -Cross organization/single organization
- Repositories should have a consistence license (open source or proprietary)
- Repositories should have a well defined
    -CI process
    -Build/Test process
    -Release process
- Repositories should provide documentation for working with the repository

## Uefi Packages

- Packages are the sharing granular in Project Mu
- Packages should be for a feature/feature set
- Packages should enable all CI features
- Packages should contain a hosted-based unit test Dsc
- Packages should contain a compile test Dsc that includes all INF files
- Packages should have minimized dependencies
- Package documentation should reside in the same package (Docs folder)
  - Documentation should describe dependencies
  - Documentation should describe integration steps
  - Documentation should describe abstraction points and package usage

## Uefi Components

1. All new modules must be listed in their containing package Dsc in the components section
2. All modules must follow the dependency rules of their containing package
3. All modules within common layers should avoid silicon or architecture dependencies.
    - Use existing libraries and functionality when possible
    - Build out minimal required abstraction to allow other silicon or architectures to leverage common capabilities
4. All modules should consider testability as part of their design.
    - Writing a unit test e

## Public Header files

1. Don't include other header files
2. Don't mix public and private information in the same header file
    - Implementation details should be contained to the instance
3. Use "doxygen" style function header comments to clearly specify parameters and return results.
4. Use a guidgen tool to define any guids
5. For libraries:
    - Library class should be listed in Package DEC file
    - A NULL instance must be created that allows compiling and linking with minimal dependencies.

## Library Instance

1. The supported module types in the INFs must be accurate.

    ``` inf
    LIBRARY_CLASS: <Library Class Name>|<Module types supported by this instance>
    ```

2. Use STATIC on each non-public function and non-public global to avoid conflicts with other modules.
3. Use EFIAPI on all public library class functions.

## Source files

Source files should follow the Edk2 coding standards available on [TianoCore.org](https://www.tianocore.org/) website.  

Please include the appropriate copyright messages in the file headers, and Spdx License
Identifiers are appreciated (<https://spdx.org/licenses/>).

## More info

For general Edk2 and UEFI development additional information can be found at the
[TianoCore.org](https://www.tianocore.org/) website.
