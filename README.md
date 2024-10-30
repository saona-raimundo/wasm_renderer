Based on [wasmlink demo](https://github.com/bytecodealliance/wit-bindgen/tree/main/crates/wasmlink/demo) of the [wit-bindgen project](https://github.com/bytecodealliance/wit-bindgen).

# Goal

A Rust plugin-based app that renders text, where the plugins are wasm modules.

# Design

- The renderer API is defined by `renderer.wit`. 
- The app will search for plugins in the `plugins` directory.
- 

# Building

Let us build the plugin that renders markdown into html.

## Prerequisites

We use [cargo-wasi](https://github.com/bytecodealliance/cargo-wasi) to compile the plugin. Install it using `cargo`:

```text
$ cargo install cargo-wasi
```

### Building the `markdown` plugin

The `renderer.wit` defines the structure of a plugin: a `render` function that takes a string (the [Markdown](https://en.wikipedia.org/wiki/Markdown)) as an argument and returns a string (the rendered HTML).

To build the `markdown` plugin:

- Go to the `markdown` directory.
- Build using `cargo wasi build`

### Adding the plugin to the app

Take the resulting `markdown.wasm` file (in `markdown\target\wasm32-wasi\debug\markdown.wasm`) and put it into `app\plugins`, so that the app can find it.
You may run something like `cp markdown\target\wasm32-wasi\debug\markdown.wasm app\plugins`.

# Running

Let us run our app. (For now it will run only the markdown plugin)

- Go to the `app` directory.
- Use `cargo run`.

## Notes

- Check that `markdown.wasm` is under the `plugins` folder.
- Note that the `renderer.wit` is also needed for the app to interpret this wasm file.
