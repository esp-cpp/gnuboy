# gnuboy (Game Boy / Game Boy Color) for ESP32 emulators

The Game Boy / Game Boy Color core of esp-box-emu: gnuboy ([rofl0r/gnuboy](https://github.com/rofl0r/gnuboy), by way of [hex007/esp32-gnuboy](https://github.com/hex007/esp32-gnuboy) and retro-go), with esp-box-emu's changes.

## Layout

- `gnuboy/`: the emulator core, as esp-box-emu has carried it (see below for its origin and changes).
- `port/`: the glue to the host firmware: `port/include/gameboy.hpp` is the API the
  firmware calls (init / run a frame / save / load / deinit, the video buffer for
  screenshots), `port/` implements it.

The port talks to the board through the `BoxEmu` singleton of
[esp-box-emu](https://github.com/esp-cpp/esp-box-emu) (`box-emu.hpp`: frame
buffers, `push_frame()`, `palette()`, `play_audio()`, `gamepad_state()`, ...).
[tab5-emu](https://github.com/esp-cpp/tab5-emu) provides the same API
(`using BoxEmu = Tab5Emu`), so the same sources build for both.

## Use

Add this repository as a submodule inside an ESP-IDF component and register its
sources from that component's `CMakeLists.txt` (each firmware keeps its own
component wrapper: the requirements, compile flags and linker fragment for
its target). See esp-box-emu's `components/gbc/CMakeLists.txt`.

The history up to the split is esp-box-emu's history of `components/gbc`.

## License

gnuboy is under the GNU General Public License, version 2. The port is under the same license.
