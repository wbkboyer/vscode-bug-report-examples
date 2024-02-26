# vscode-bug-report-examples
A repo with a simple Hello World C program to demonstrate issues with the VSCode C/C++ Extension v1.19.4 on Windows.

## Summary of issues encountered
* For Clang on MacOS, spaces added to enclose `-g` parameter causes the build to fail
    * To be resolved by [vscode-cpptools #12001](https://github.com/microsoft/vscode-cpptools/issues/12001)
* For MinGW GCC, spaces added to enclose `args`, which causes the build to fail
    * To be resolved by [vscode-cpptools #12001](https://github.com/microsoft/vscode-cpptools/issues/12001)
* For MSVC compiler toolchain
    * Debugger breakpoints not working with external console ([others](https://stackoverflow.com/questions/53108690/visual-studio-code-c-debugger-doesnt-start) seem to have encountered this issue _years_ ago)
    * On some projects, `externalConsole` is deprecated and we are instructed to use `console`, but for other projects, `externalConsole` is accepted and there's an error that `console` is not an accepted key.
    * With `externalConsole` set to `false` (or `console` set to `integratedTerminal`)
        * Can't find `.pdb` symbols file for _some_ projects (for example, [edge-addition-planarity-suite](https://github.com/graph-algorithms/edge-addition-planarity-suite)), even after setting `symbolSearchPath` or `symbolOptions`; see:
            * [`launch.json` reference - symbolSearchPath](https://code.visualstudio.com/docs/cpp/launch-json-reference#_symbolsearchpath) docs
            * [`launch.json` reference - symbolOptions](https://code.visualstudio.com/docs/cpp/launch-json-reference#_symbol-options) docs
            * [Debug C++ in Visual Studio Code - Additional symbols](https://code.visualstudio.com/docs/cpp/cpp-debug#_additional-symbols) docs
        * If you manage to attach the debugger, then the process terminates normally or via the "Stop Debugging" button, then try to start a new debug session, for small projects the debugger process ends without the program being executed; for larger projects, VSCode hangs.
            * Process for executable is not killed after VSCode is terminated
        * Setting `cwd` to `${workspaceFolder}` not being set correctly in internal console so relative paths are broken; user must start debugging with focus given to entrypoint C file open
- Bottom of screen run configuration (blue bar icon) doesn't match actual run configuration being used when `isDefault` set to `true` for configuration in `tasks.json`, but rather matches the first configuration in `tasks.json`/`launch.json`,
- when `isDefault: true`, any changes to `launch.json`/`tasks.json` aren't respected (e.g. changing external vs. internal console) unless you turn isDefault back to false and choose the desired task
