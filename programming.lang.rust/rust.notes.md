{
    Which files from the target directory are required?
None. By default, the compiler makes statically-linked binaries.

The other files are merely build artifacts maintained by Cargo in order to make rebuilding your code more efficient. They include things like your dependencies.

A non-exhaustive sampling of some of the files you might find:

    *.d — Makefile-compatible dependency lists
    *.rlib — Rust library files. Contain the compiled code of a dependency
    build — Directories for build scripts to use as scratch space
    deps — Your compiled dependencies
    examples — Binaries from the examples directory
    incremental — A directory for the incremental compilation cache
    *-{hash} — Binaries from cargo test
    executables — Your target binaries

Some of this is documented in the Cargo source code.
}