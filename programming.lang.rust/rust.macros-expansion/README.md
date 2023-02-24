# Rust macro expansion
Want to see what the rust macros are actually doing?

Macro expansion features only work with nightly

Rust should already be installed with `rustup` and `cargo` available

1. Install rust nightly
    - `rustup install nightly`
2. Get cargo expand
    - `cargo install cargo-expand`
    - cargo expand prints the result of macro expansion and passes it to `rustfmt` to make the code more readable
3. Temporarily use the nightly toolchains by using "plus syntax"
    - `cargo +nightly expand`
    - `cargo +nightly rustc --profile=check -- -Zunpretty=expanded`