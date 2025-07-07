# Upstream Contributions

This page lists the upstream contributions, for some distro who want to use these features but use a stable version of the software, you can cherry-pick these commits to your own stable branch.

## Bug fixes

### GLIBC

- ✅(Since 2.41)[Fix IFUNC resolver cannot access gp pointer](https://patchwork.sourceware.org/project/glibc/patch/tencent_C1F3ED085268473862E1B2C75884F035D20A@qq.com/)

    This is important for non-PIE binaries when IFUNC based function multi-version dispatching is used, such as in GCC with `target_clones` or `target_version`. Without this fix, FMV dispatching will crash when the function is called.

## New features

### GCC

- ❓[Add -ftarget-clones-table option support](https://patchwork.sourceware.org/project/gcc/list/?series=49088&state=*)
  
    This patch adds support for the `-ftarget-clones-table` option in GCC, allowing specifying a table of target clones in a **JSON** file for every target. Thus we don't need to use `target_clones` attribute in the source code, which makes the source code cleaner and easier to maintain.

- ❓[Redirect to specific target based on TARGET_VERSION_COMPATIBLE](https://patchwork.sourceware.org/project/gcc/list/?series=46245&state=*)

    To prevent the overhead from indirect function call which loads the pointer from GOT, this patch allows GCC to generate a direct call to the target version function if the target version is compatible with the current multi-versioning function. This is useful for performance-critical code that uses function multi-versioning and works well with LTO optimizations.

- ✅(Since 15.0)[RISC-V: Add Function Multi-Versioning support](https://patchwork.sourceware.org/project/gcc/list/?series=40263&state=*)

    This allows GCC to use `target_clones` and `target_version` to generate function multi-version dispatching code.

### LLVM

- ✅(Since 20.1)[[RISCV][FMV] Support target_version (#99040)](https://github.com/llvm/llvm-project/commit/7ab488e92c39c813a50cb4fd6587e7afc161c7d5)

    This allows LLVM to use `target_version` to generate function multi-version dispatching code.