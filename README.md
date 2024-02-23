# build2 Package for snitch

This project is a [build2](https://build2.org) package repository that provides access to [`snitch`](https://github.com/snitch-org/snitch), a lightweight C++20 testing framework.

[![Official](https://img.shields.io/website/https/github.com/snitch-org/snitch.svg?down_message=offline&label=Official&style=for-the-badge&up_color=blue&up_message=online)](https://github.com/snitch-org/snitch)
[![build2](https://img.shields.io/website/https/github.com/build2-packaging/libsnitch.svg?down_message=offline&label=build2&style=for-the-badge&up_color=blue&up_message=online)](https://github.com/build2-packaging/libsnitch)
[![cppget.org](https://img.shields.io/website/https/cppget.org/libsnitch.svg?down_message=offline&label=cppget.org&style=for-the-badge&up_color=blue&up_message=online)](https://cppget.org/libsnitch)
[![queue.cppget.org](https://img.shields.io/website/https/queue.cppget.org/libsnitch.svg?down_message=empty&down_color=blue&label=queue.cppget.org&style=for-the-badge&up_color=orange&up_message=running)](https://queue.cppget.org/libsnitch)

## Usage
Make sure to add the stable section of the [`cppget.org`](https://cppget.org/?about) repository to your project's `repositories.manifest` to be able to fetch this package.

    :
    role: prerequisite
    location: https://pkg.cppget.org/1/stable
    # trust: ...

If the stable section of `cppget.org` is not an option then add this Git repository itself instead as a prerequisite.

    :
    role: prerequisite
    location: https://github.com/build2-packaging/snitch.git

Add the respective dependency in your project's `manifest` file to make the package available for import.

    depends: libsnitch ^1.2.4

To import the library target that already implements the `main` function, include the following declaration in a `buildfile`.

    import snitch = libsnitch%lib{snitch-main}

If you want to customize the testing process by providing your own `main`, use the following library target instead.

    import snitch = libsnitch%lib{snitch}

## Configuration
`snitch` itself already comes with various configuration options that provide sane defaults.
Nearly all of these can be accessed by the package configuration.
As a testing framework, `snitch` will most likely be linked to generate a final executable.
In this case, feel free to change these defaults and adjust them to your needs if you know what to do.

    config [uint64] config.libsnitch.max_test_cases           ?= 5000
    config [uint64] config.libsnitch.max_nested_sections      ?=    8
    config [uint64] config.libsnitch.max_expr_length          ?= 1024
    config [uint64] config.libsnitch.max_message_length       ?= 1024
    config [uint64] config.libsnitch.max_test_name_length     ?= 1024
    config [uint64] config.libsnitch.max_tag_length           ?=  256
    config [uint64] config.libsnitch.max_captures             ?=    8
    config [uint64] config.libsnitch.max_capture_length       ?=  256
    config [uint64] config.libsnitch.max_unique_tags          ?= 1024
    config [uint64] config.libsnitch.max_command_line_args    ?= 1024
    config [uint64] config.libsnitch.max_registered_reporters ?=    8
    config [uint64] config.libsnitch.max_path_length          ?= 1024

    config [bool] config.libsnitch.with_exceptions                 ?=  true
    config [bool] config.libsnitch.with_timings                    ?=  true
    config [bool] config.libsnitch.with_shorthand_macros           ?=  true
    config [bool] config.libsnitch.default_with_color              ?=  true
    config [bool] config.libsnitch.constexpr_float_use_bitcast     ?=  true
    config [bool] config.libsnitch.decompose_successful_assertions ?= false
    config [bool] config.libsnitch.with_all_reporters              ?=  true
    config [bool] config.libsnitch.with_teamcity_reporter          ?= false
    config [bool] config.libsnitch.with_catch2_reporter            ?= false

## Issues and Notes
Currently, there are no issues to be reported.

## Contributing
Thanks in advance for your help and contribution to keep this package up-to-date.
For now, please, file an issue on [GitHub](https://github.com/build2-packaging/snitch/issues) for everything that is not described below.

### Recommend Updating Version
Please, file an issue on [GitHub](https://github.com/build2-packaging/snitch/issues) with the new recommended version.

### Update Version by Pull Request
1. Fork the repository on [GitHub](https://github.com/build2-packaging/snitch) and clone it to your local machine.
2. Run `git submodule init` and `git submodule update` to get the current upstream directory.
3. Inside the `upstream` directory, checkout the new library version `X.Y.Z` by calling `git checkout vX.Y.Z` that you want to be packaged.
4. If needed, change source files, `buildfile`s, and symbolic links accordingly to create a working build2 package. Make sure not to directly depend on the upstream directory inside the build system but use symbolic links instead.
5. Update library version in `manifest` file if it has changed or add package update by using `+n` for the `n`-th update.
6. Make an appropriate commit message by using imperative mood and a capital letter at the start and push the new commit to the `master` branch.
7. Run `bdep ci` and test for errors.
8. If everything works fine, make a pull request on GitHub and write down the `bdep ci` link to your CI tests.
9. After a successful pull request, we will run the appropriate commands to publish a new package version.

### Update Version Directly if You Have Permissions
1. Inside the `upstream` directory, checkout the new library version `X.Y.Z` by calling `git checkout vX.Y.Z` that you want to be packaged.
2. If needed, change source files, `buildfile`s, and symbolic links accordingly to create a working build2 package. Make sure not to directly depend on the upstream directory inside the build system but use symbolic links instead.
3. Update library version in `manifest` file if it has changed or add package update by using `+n` for the `n`-th update.
4. Make an appropriate commit message by using imperative mood and a capital letter at the start and push the new commit to the `master` branch.
5. Run `bdep ci` and test for errors and warnings.
6. When successful, run `bdep release --tag --push` to push new tag version to repository.
7. Run `bdep publish` to publish the package to [cppget.org](https://cppget.org).
