crate : smallest amount of code Rust compiler considers at a time

the compiler considers the single source file as a crate

crates contain: 
- modules

modules allow privacy control/visibility management
modules allow hierarchically splitting code into logical units
modules are collections of items: functions, structs, traits, `impl` blocks, even other modules

modules are private by default

2 types of crates:
    
- binary crate, has `main` 
- library crate, for sharing

Rustaceans "crates" are "libraries"

package: set of crates
- package = {c1,c2,..,cn} where cn is crate n