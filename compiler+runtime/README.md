# jank compiler and runtime

boehm now support wasm64?
https://github.com/bdwgc/bdwgc/commit/3f4e077edb2496bfd14e625f3a440f38caac458a

## emscripten build attempts

need [emscripten](https://emscripten.org/index.html)

cpptrace commit from upstream needed

- https://github.com/jeremy-rifkin/cpptrace/pull/329/changes
- https://github.com/jeremy-rifkin/cpptrace/commit/eb58832363b517f298f35715c6756ad83a3a553a
- https://github.com/jeremy-rifkin/cpptrace/commit/a354f410bf98d9b57714672fdd5d4995921f0beb


./bin/emconfigure and ./bin/emcompile are the same as ./bin/configure and ./bin/compile but cmake is appended with `emcmake.bat` and `emmake.bat`. also tested "working" on steam os with `emcmake` and `emmake`. The artifact is unusable though because during linking with jank's generated cpp, bdwgc linking will fail.

```sh
./bin/emconfigure -GNinja -DCMAKE_BUILD_TYPE=Release -DCPPTRACE_UNWIND_WITH_NOTHING=1 -Djank_only_static_runtime=1 -Denable_threads=false

./bin/emcompile --target jank_common_lib --target jank_static_lib
```

emscripten used
- for windows: https://packages.msys2.org/packages/mingw-w64-clang-x86_64-emscripten
- for steam os: nix-shell -p emscripten
