# codal-pico2
CODAL target for the Raspberry Pi RP2350 (Cortex-M33, ARM secure mode), e.g. the Raspberry Pi Pico 2 board.

Uses [codal-rp2040](https://github.com/lancaster-university/codal-rp2040), which supports both RP2040 and RP2350 on pico-sdk 2.x. Until that support is merged upstream, `target.json` points to the `rp2350` branch of the [rc-kid fork](https://github.com/rc-kid/codal-rp2040). The chip is selected via `cmake_definitions` (`PICO_PLATFORM=rp2350-arm-s`, `PICO_BOARD=none`, i.e. the 48 GPIO RP2350B superset). The pico-sdk bundled with codal-rp2040 is used unless `PICO_SDK_PATH` is set.

The build produces `.hex` and `.bin`. A UF2 for drag & drop can be made with picotool: `cp build/PICO2 PICO2.elf && picotool uf2 convert PICO2.elf PICO2.uf2 --family rp2350-arm-s` (picotool needs the `.elf` extension).
