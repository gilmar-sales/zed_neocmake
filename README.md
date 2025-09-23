# NeoCMake

This is [CMake](https://cmake.org/) extension for [Zed editor](https://zed.dev/). It combines [uyha/tree-sitter-cmake](https://github.com/uyha/tree-sitter-cmake) and [Decodetalkers/neocmakelsp](https://github.com/Decodetalkers/neocmakelsp) (hence why it's "neo").
The tree-sitter grammar is taken from [helix repo](https://github.com/helix-editor/helix/tree/master/runtime/queries/cmake).

## C++ LSP support (`compile_commands.json`)

For making clangd and cmake work together do the following:

1. Add `set(CMAKE_EXPORT_COMPILE_COMMANDS ON)` at the top of the `CMakeLists.txt` (somewhere below `project`);
2. Reconfigure cmake project. If everything is correct there should be `compile_commands.json` file under build directory. I also advise using `CXX=clang` for better compatibility with clangd;
3. Go to Zed's `settings.json`: Ctrl+Shift+P `open local settings`/`open default settings`;
5. Find `lsp` section. Inside it paste the following (replace `build` with your build directory name):

```json
"clangd": {
    "arguments": ["-background-index", "-compile-commands-dir=build"]
}
```

## CMake tasks

The extension now provides 5 tasks to start with:
- `CMake configure Debug`
- `CMake configure Release`
- `CMake build Debug/Release` - builds what is configured beforehand
- `CMake configure and build Debug`
- `CMake configure and build Release`

**All tasks use `build` directory for building**
