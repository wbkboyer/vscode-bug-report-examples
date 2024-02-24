# vscode-bug-report-examples
A repo with a simple Hello World C program to demonstrate issues with the VSCode C/C++ Extension v1.19.4 on Windows.

## Summary of issues encountered
* For MinGW GCC, spaces added to enclose `args`, which causes the build to fail
* For MSVC compiler toolchain
    * Debugger breakpoints not working with external console
    * Setting `cwd` to `${workspaceFolder}` not being set correctly in internal console so relative paths are broken; user must start debugging with focus given to entrypoint C file open
    * Can't find `.pdb` symbols file for some projects, even after setting `symbolSearchPath` or `symbolOptions`
    * If you manage to attach the debugger, then the process terminates normally or via the "Stop Debugging" button, then try to start a new debug session, VSCode hangs
- Bottom of screen run configuration (blue bar icon) doesn't match actual run configuration being used when `isDefault` set to `true` for configuration in `tasks.json`, but rather matches the first configuration in `tasks.json`/`launch.json`,
- when `isDefault: true`, any changes to `launch.json`/`tasks.json` aren't respected (e.g. changing external vs. internal console) unless you turn isDefault back to false and choose the desired task
