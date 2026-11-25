# Installing and playing Prime3AP

Metroid Prime 3: Corruption for [Archipelago](https://archipelago.gg), version 0.3.0 (beta).

## 1. Requirements

| What | Notes |
|---|---|
| Windows 10 or 11 | The patch tool runs on Windows only. |
| [Archipelago](https://github.com/ArchipelagoMW/Archipelago/releases) **0.6.8 or newer** | The installed version is fine. |
| [Dolphin](https://dolphin-emu.org/) or [PrimeHack](https://github.com/shiiion/dolphin/releases) | Tested: Dolphin 2609b, PrimeHack 1.0.9. In PrimeHack, leave "Emulated CPU Clock Override" off. |
| Your own **Wii PAL** disc image of Metroid Prime 3: Corruption, game ID **RM3P01**, unmodified | Not provided here, and never will be. Dump your own disc. NTSC (RM3E01, RM3J01) and Metroid Prime Trilogy do **not** work. |
| Microsoft Visual C++ 2015-2022 Redistributable ([x64](https://aka.ms/vs/17/release/vc_redist.x64.exe), [x86](https://aka.ms/vs/17/release/vc_redist.x86.exe)) | Most PCs already have it (Dolphin needs it too). |
| About 10 GB free disk space | Temporary files while patching (about 2 × the ISO) plus the patched ISO. |
| Internet on the first patch | The patch tools (31 MB) are downloaded once. For offline use see [Troubleshooting](#7-troubleshooting). |

How to check the game ID of your ISO: in Dolphin, right-click the game → Properties → Info: "Game ID" must be `RM3P01`.

## 2. Install the APWorld

1. Download `metroidprime3.apworld` from the [latest release](https://github.com/junkx420/Prime3AP/releases).
2. Double-click it, or open the Archipelago Launcher and choose **Install APWorld**. It ends up in
   `custom_worlds` inside your Archipelago folder.
3. Restart the Archipelago Launcher. "Metroid Prime 3 Client" now appears in the launcher.

To update, install the new `.apworld` the same way (it replaces the old one).

## 3. Create your player YAML

Use [`examples/Metroid Prime 3 Corruption.yaml`](../examples/Metroid%20Prime%203%20Corruption.yaml) (also attached to
each release as `metroidprime3-example.yaml`). Change `name` to your slot name. The world has no game-specific options yet; everything else can stay at
the default:

```yaml
name: YourName
game: 'Metroid Prime 3: Corruption'
requires:
  version: 0.6.8
'Metroid Prime 3: Corruption':
  progression_balancing: normal
  accessibility: full
```

What the world does:

- 99 locations (every pickup in the game) are shuffled into the multiworld. Pickups that belong to other players show
  up in the game as "Archipelago Item".
- You start at G.F.S. Valhalla, Docking Bay 5, with the same starting items as Randovania's starter preset.
- Goal: defeat Dark Samus and Aurora Unit 313 on Phaaze.

## 4. Generate or join a multiworld

- **Hosting yourself:** put all YAMLs into `Players` in your Archipelago folder and run **Generate** in the launcher.
  The output ZIP in `output` contains one `AP_<seed>_P<slot>_<name>.apmp3` per Metroid Prime 3 player. Host it with
  **Host** (local) or upload the output ZIP to [archipelago.gg](https://archipelago.gg/uploads).
- **Joining:** the `.apmp3` of your slot is the file you need. Get it from the person who generated the seed (it is in
  the output ZIP). If the room page on archipelago.gg offers a download for your slot, that one also contains the
  server address.

Whoever generates needs the `.apworld` installed (step 2). archipelago.gg cannot generate seeds with this world, so
generate locally.

## 5. Patch the game: open the `.apmp3`

Double-click the `.apmp3` (choose `ArchipelagoLauncher.exe` under "Open with" the first time), or open the
launcher, choose **Open Patch** and select the `.apmp3`.

1. **First time only:** a file dialog asks for your original Metroid Prime 3 ISO (RM3P01). The path is saved in
   `host.yaml` (`metroidprime3_options` → `iso_file`).
2. **First time only:** the patch tools (MP3Randomizer, nodtool, wit) are downloaded from this repository's release,
   checked against a fixed SHA-256 and stored in `metroidprime3_tools` inside your Archipelago folder. The patch window
   shows the progress.
3. The patch window shows six steps (about 40 seconds). The patched ISO is written next to the `.apmp3`, with the same
   name and the extension `.iso`. Your original ISO is not changed.
4. The **Metroid Prime 3 Client** starts. If the `.apmp3` came from archipelago.gg, it already knows the server.

Opening the same `.apmp3` again skips patching (the ISO already has the right seed ID) and only starts the client.

Optional `host.yaml` settings:

```yaml
metroidprime3_options:
  iso_file: "D:\\Games\\Metroid Prime 3 (PAL).iso"   # original ISO
  tools_folder: ""      # folder with the patch tools; empty = download/cache automatically
  output_folder: ""     # where patched ISOs go; empty = next to the .apmp3
```

## 6. Play

1. Start Dolphin or PrimeHack and boot the **patched** ISO (`AP_..._<name>.iso`), not the original.
2. In the Metroid Prime 3 Client, connect to the server if it is not connected yet: type
   `/connect <address:port>` (for example `/connect archipelago.gg:38281`), then your slot name.
3. Start a new game. The client sends every pickup you collect and gives you every item you receive.

The order of emulator and client does not matter; the client reconnects to the emulator every few seconds. The client
only works when the running ISO belongs to the connected slot (seed ID check): if it says **WRONG ISO** or **NOT AN AP
ISO**, you booted the ISO of another seed or slot, or the original.

Useful client commands: `/seed` (result of the seed ID check), `/inventory` (what the client manages),
`/seedwarn on|off` (Leviathan seed warning),
`/missing`, `/received`, `!hint <item>`.

## 7. Troubleshooting

| Problem | What to do |
|---|---|
| "Could not download the patch tools" (no internet, firewall) | Download `metroidprime3-tools-win.zip` from the [release page](https://github.com/junkx420/Prime3AP/releases/tag/v0.3.0) on any PC. Put the ZIP **as it is** (not extracted) into `metroidprime3_tools` in your Archipelago folder (create the folder) and open the `.apmp3` again. Or extract it anywhere and set `tools_folder` in `host.yaml` to that folder. |
| "... has SHA-256 ..., expected ..." | The ZIP is damaged or not the one of this version. Delete it and download it again from the release page. |
| "nodtool.exe failed ... a DLL is missing" | Install the Microsoft Visual C++ 2015-2022 Redistributable (links in section 1). |
| "game ID ... is not Metroid Prime 3: Corruption" or "... untested" | Wrong disc image. Only the Wii PAL version RM3P01 works; Metroid Prime Trilogy does not. Set `iso_file` in `host.yaml` to the right file. |
| Wrong ISO chosen in the file dialog | Edit `iso_file` under `metroidprime3_options` in `host.yaml` (Archipelago folder). |
| Patching fails with a disk error | Free about 10 GB on the drive of your temp folder and of the `.apmp3`. |
| Client says "WRONG ISO" or "NOT AN AP ISO", nothing is sent | Boot the ISO that was built from **your** `.apmp3`. Each seed and slot has its own ISO. |
| Client does not find the game | Start the game in Dolphin/PrimeHack first. Only one emulator may run. |
| A received Energy Tank is empty | Known limitation: save at your ship or collect energy to refill it. |
| A collected pickup was not sent | Rare (see limitations). Leave the room and come back; if it is still missing, ask the host to use `/send_location <your name> <location>`. |
| Something else | Logs are in `logs` in your Archipelago folder: `MetroidPrime3Patch_*.txt` (patching) and `MetroidPrime3Client_*.txt` (client). Open an [issue](https://github.com/junkx420/Prime3AP/issues) with them. |

## 8. Known limitations (0.3.0)

- **Wii PAL (RM3P01) only.** NTSC-U, NTSC-J and Metroid Prime Trilogy are not supported.
- **Leviathan cores:** only enter a Leviathan seed's core when you have the item you need to get out again, or you are
  stuck and must reload your save:
  Bryyo seed → Hyper Ball; SkyTown Elysia seed → Hyper Missile (and at least 4 Missiles);
  Pirate Homeworld seed → Hyper Grapple and Grapple Voltage.
  The client warns you when you enter a seed without it (`/seedwarn off` turns the warning off).
- **SkyTown Elysia bomb sequence:** do not start it without Seeker Missiles. Collecting only the first part of the
  seed bomb and then going back to SkyTown Elysia Main crashed the game in testing. If it happens, reload your save.
- **Several copies of a world's location flags:** the game keeps more than one copy of the flag block per world. The
  client checks all of them; in testing no pickup was lost, but a missed pickup cannot be ruled out yet.
- Received Energy Tanks are not refilled (see Troubleshooting).
- Pickups of other players all look the same ("Archipelago Item", Energy Cell model); there is no per-item text yet.
- No game-specific options yet (no starting location, trick level or DeathLink).

## 9. Licences and sources

The `.apworld` is GPL-3.0 (logic data derived from [Corruptovania](https://github.com/Schwork-Corruption/corruptovania)
/ [Randovania](https://github.com/randovania/randovania)). Development happens in
[junkx420/corruptovania](https://github.com/junkx420/corruptovania/tree/archipelago). The patch tools ZIP contains
third-party programs under MIT, GPL-2.0 and LGPL-3.0 and other licences; see `THIRD-PARTY-NOTICES.txt` and the
`licenses` folder inside the ZIP.
