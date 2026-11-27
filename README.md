# Prime3AP

*Phazopelago*

**Metroid Prime 3: Corruption for [Archipelago](https://archipelago.gg).**

> **Beta available:** [**Prime3AP 0.4.0 (beta)**](https://github.com/junkx420/Prime3AP/releases/tag/v0.4.0) is the
> current beta. Expect rough edges; see
> [known limitations](docs/INSTALL.md#8-known-limitations-040) and report problems in the
> [issues](https://github.com/junkx420/Prime3AP/issues).

## What you get

Download from the [v0.4.0 release](https://github.com/junkx420/Prime3AP/releases/tag/v0.4.0):

| File | What it is |
|---|---|
| `metroidprime3.apworld` | The Archipelago world: generation, the patch file `.apmp3`, the launcher entry and the **Metroid Prime 3 Client** (connects Dolphin/PrimeHack to the Archipelago server). |
| `metroidprime3-example.yaml` | Example player YAML with the default options (also in [`examples/`](examples/)). |
| `metroidprime3-tools-win.zip` | Patch tools (MP3Randomizer, nodtool, wit, HDiffPatch and patch data). **You do not need to download it**: the patch tool fetches it automatically the first time. Only for offline installs. |
| `wiimms-iso-tools-r8638-src.tar.gz`, `cygwin-3.1.7-1-src.tar.xz` | Source code of the GPL/LGPL programs in the tools ZIP (wit, Cygwin). Not needed to play. |
| `SHA256SUMS.txt` | SHA-256 checksums of the files above. |

## Quick start

Requirements: Windows, [Archipelago](https://github.com/ArchipelagoMW/Archipelago/releases) 0.6.8 or newer,
Dolphin or PrimeHack, and **your own** clean Wii PAL (**RM3P01**) or NTSC-U (**RM3E01**) Rev 0 disc image of Metroid Prime 3: Corruption.

1. Install `metroidprime3.apworld` (double-click it or Launcher → **Install APWorld**), restart the launcher.
2. Put the example YAML (with your `name`) into `Players`, generate, host.
3. Open your `.apmp3` (double-click or Launcher → **Open Patch**). The first time, choose your original ISO; the patch
   tools are downloaded once. A patched ISO appears next to the `.apmp3` and the client starts.
4. Boot the patched ISO in Dolphin/PrimeHack, connect the client, start a new game.

Full guide with troubleshooting: **[docs/INSTALL.md](docs/INSTALL.md)**.

## Supported versions

Wii PAL (**RM3P01**) and NTSC-U (**RM3E01**) Rev 0 on **Dolphin** or **PrimeHack**. PAL applies Deflicker by default.
NTSC-U applies MP3Update and Deflicker by default.

Universal Tracker v0.3.8 can track a slot from seed data with the v0.4.0 APWorld installed.
[Tracker setup](docs/INSTALL.md#universal-tracker)

## No game files

This repository does not contain and will never distribute an ISO or any other game files. You need your own legally
obtained copy of the game.

## Development

Development happens in the fork [junkx420/corruptovania](https://github.com/junkx420/corruptovania) on the branch
[`archipelago`](https://github.com/junkx420/corruptovania/tree/archipelago) (logic data, APWorld, client, patch tool).
The release assets are built there with `apworld/tools/release/build_release.py`.

## Credits

- [Corruptovania](https://github.com/Schwork-Corruption/corruptovania) and [Randovania](https://github.com/randovania/randovania)
  for the game logic data and the patcher this project builds on
- gollop's MP3Randomizer, [nod](https://github.com/AxioDL/nod), [lzokay](https://github.com/AxioDL/lzokay) and
  [Wiimms ISO Tools](https://wit.wiimm.de/) (licences in the tools ZIP)
- [Archipelago](https://github.com/ArchipelagoMW/Archipelago) for the multiworld framework

## License

[GNU General Public License v3.0](LICENSE). The third-party programs in the tools ZIP keep their own licences
(`THIRD-PARTY-NOTICES.txt` inside the ZIP).
