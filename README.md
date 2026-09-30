# BBCrossBuild projects

The project files of [BBCrossBuild](https://github.com/badbat75/bbcrossbuild), checked out as its
`projects/` submodule. A project is `<name>.prj`, ordinary Bash that `bbxb build <name> <platform>`
sources with every function of the framework in scope; `<name>.conf` next to it (gitignored) holds
the settings of the user and is sourced by `bbxb` before it.

| File | Content |
| --- | --- |
| `lfs.prj` | The reference project: toolchain, kernel, ~100 packages, disk image, QEMU scripts |
| `lfs.conf.template` | The settings `lfs.prj` reads: `cp lfs.conf.template lfs.conf` |
| `librespot.prj`, `rpi-kernel.prj`, `wsl-kernel.prj` | Minimal examples: one application, one kernel |
| `gcc-toolkits.prj` | The toolchain only (`setup_full_toolchain`); `utilities/gcc_tkit_path` puts one in `PATH` |
| `tests/board_check` | Checks a running system `lfs.prj` built, on the board or under QEMU |

```bash
./bbxb build lfs rpi3-aarch64                              # from the checkout of the framework
scp projects/tests/board_check <host>:/tmp/ && ssh <host> sudo /tmp/board_check
```

Another directory of projects works the same way: `PRJ_PATH=<directory> ./bbxb build <name> <platform>`
(absolute, or relative to the checkout of the framework).
