# Zopfli in Rust [![crates.io badge](https://img.shields.io/crates/v/zopfli)](https://crates.io/crates/zopfli)

This is a reimplementation of the [Zopfli](https://github.com/google/zopfli) compression tool in Rust.

Carol Nichols started the Rust implementation as an experiment in incrementally rewriting a C library in Rust, keeping the project compiling at every step. For more information about that experiment, see [the slides for a talk she gave about it](https://github.com/carols10cents/rust-out-your-c-talk) and [the repo as it was for the experiment](https://github.com/carols10cents/zopfli).

## How to build

To build the code, run:

```
$ cargo build --release
```

and the executable will be in `target/release/zopfli`.

This should work on stable or beta Rust.

You can also run `make zopfli`, which will run `cargo build` and then symlink `target/release/zopfli` to just `zopfli` in the project root; this is what the C library does and it was useful for scripting purposes during the rewrite process to keep the command and resulting artifacts the same.

## Running the tests

There are some unit tests, mostly around the boundary package merge algorithm implementation in katajainen.rs, that can be run with:

```
$ cargo test
```

Golden master tests, to check that compressed files are exactly the same as the C implementation would generate, can be run using:

```
$ ./test/run.sh
```

and then checking that git reports no changes to the files in `test/results`.

Or you can run `make test`, which will run `cargo test`, then `./test/run.sh`, and then will fail if there are any changed files according to git. Note that if you have uncommitted changes and you run this, your changes will cause this command to fail, but the tests actually passed.

