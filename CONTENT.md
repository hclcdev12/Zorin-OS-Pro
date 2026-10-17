# Minimal vs. Extra content

`zorin.sh` has two install modes. Without any flag it installs the **minimal** set; with `-X` it installs the **extra** set. The `-U` flag only removes the confirmation prompts and does not change what gets installed.

The lists below are taken from the package lists inside `zorin.sh`. The script is idempotent: running it again with `-X` on a system that already received the minimal set only adds what is missing.

## Summary

| | Minimal (no flag) | Extra (`-X`) |
|---|---|---|
| Pro layouts for Zorin Appearance | yes | yes |
| Pro wallpapers for your release | yes | yes |
| Pro wallpapers from older releases | no | yes |
| Core wallpapers from older releases | no | yes |
| `zorin-os-pro-creative-suite` (GIMP, Shotwell) | no | yes |
| `zorin-os-pro-productivity-apps` (GNOME Maps, LibreCAD) | no | yes |
| General Zorin packages (already on a stock Core install) | no | yes |
| 22 Flatpak applications from Flathub | no | yes |
| apt `--no-install-recommends` | yes | no |

The minimal mode installs with `--no-install-recommends`, which is why the two Pro suites are listed by apt as "Recommended packages" and skipped. The extra mode installs them, plus everything they recommend.

## Minimal set

Installed on every supported release:

- `zorin-appearance`
- `zorin-appearance-layouts-shell-core`
- `zorin-appearance-layouts-shell-premium` (the 8 extra layouts: macOS, Windows modern, ChromeOS, Ubuntu, Windows classic, elementary, Cinnamon, Compact)
- `zorin-appearance-layouts-support`
- `zorin-auto-theme`
- `zorin-icon-themes`
- `zorin-os-artwork`
- `zorin-os-keyring`
- `zorin-os-premium-keyring`
- `zorin-os-pro` (the marker package that makes Settings > About show "Pro")
- `zorin-os-pro-wallpapers`
- `zorin-os-wallpapers`

Plus the wallpaper packs for your release:

| Release | Pro wallpapers | Core wallpapers |
|---|---|---|
| 16 | `zorin-os-pro-wallpapers-16` | `zorin-os-wallpapers-16` |
| 17 | `zorin-os-pro-wallpapers-17` | `zorin-os-wallpapers-17` |
| 18 | (included in `zorin-os-pro-wallpapers`, which pulls `zorin-os-pro-wallpapers-18`) | `zorin-os-wallpapers-18` |

## Extra set: what `-X` adds

Everything in the minimal set, plus the following.

### Pro application suites (APT)

These are metapackages from the premium repository. Their content is what they *recommend*, which is installed because the extra mode does not use `--no-install-recommends`.

| Package | Pulls in |
|---|---|
| `zorin-os-pro-creative-suite` | `gimp`, `gimp-plugin-registry`, `shotwell` |
| `zorin-os-pro-productivity-apps` | `gnome-maps`, `librecad` |

### Wallpapers from older releases (APT)

| Release | Extra Pro wallpapers | Extra Core wallpapers |
|---|---|---|
| 16 | none | `zorin-os-wallpapers-12`, `-15` |
| 17 | `zorin-os-pro-wallpapers-16` | `zorin-os-wallpapers-12`, `-15`, `-16` |
| 18 | `zorin-os-pro-wallpapers-16`, `-17` | `zorin-os-wallpapers-12`, `-15`, `-16`, `-17` |

### General Zorin packages (APT)

These are part of every stock Zorin OS Core install, so on an unmodified system they are already present and this part of the list changes nothing. They are included so that a system where some of them were removed gets them back. Verified on Zorin OS 18.1 Core: all 19 were already installed.

- `zorin-additional-drivers-checker`
- `zorin-connect`
- `zorin-desktop-session`
- `zorin-desktop-themes`
- `zorin-exec-guard`
- `zorin-exec-guard-app-db`
- `zorin-gnome-tour-autostart`
- `zorin-os-default-settings`
- `zorin-os-docs`
- `zorin-os-file-templates`
- `zorin-os-minimal`
- `zorin-os-overlay`
- `zorin-os-printer-test-page`
- `zorin-os-restricted-addons`
- `zorin-os-standard`
- `zorin-os-tour-video`
- `zorin-os-upgrader`
- `zorin-sound-theme`
- `zorin-windows-app-support-installation-shortcut`

### Flatpak applications (Flathub)

Installed one at a time, so without `-U` you are asked for each one and can skip any of them. A refused or failed application does not stop the others. Expect several gigabytes in total.

| Application | Flatpak ID | What it is |
|---|---|---|
| Blender | `org.blender.Blender` | 3D modelling and animation (about 1.1 GB installed) |
| Krita | `org.kde.krita` | Digital painting (about 640 MB installed) |
| Inkscape | `org.inkscape.Inkscape` | Vector graphics |
| darktable | `org.darktable.Darktable` | RAW photo editing |
| Scribus | `net.scribus.Scribus` | Desktop publishing |
| OpenToonz | `io.github.OpenToonz` | 2D animation |
| GColor3 | `nl.hjdskes.gcolor3` | Colour picker |
| OBS Studio | `com.obsproject.Studio` | Screen recording and streaming (about 530 MB installed) |
| Kooha | `io.github.seadve.Kooha` | Simple screen recorder |
| Kdenlive | `org.kde.kdenlive` | Video editor (releases 17 and 18) |
| Pitivi | `org.pitivi.Pitivi` | Video editor (release 16 only, instead of Kdenlive) |
| HandBrake | `fr.handbrake.ghb` | Video transcoder |
| VLC | `org.videolan.VLC` | Media player |
| Audacity | `org.audacityteam.Audacity` | Audio editor |
| Ardour | `org.ardour.Ardour` | Digital audio workstation |
| Mixxx | `org.mixxx.Mixxx` | DJ software |
| Blanket | `com.rafaelmardojai.Blanket` | Ambient sounds |
| Bottles | `com.usebottles.bottles` | Run Windows software through Wine |
| Xournal++ | `com.github.xournalpp.xournalpp` | Handwritten notes and PDF annotation |
| Foliate | `com.github.johnfactotum.Foliate` | E-book reader |
| Feeds | `org.gabmus.gfeeds` | RSS reader |
| Denaro | `org.nickvision.money` | Personal finance |
| Break Timer | `org.gnome.BreakTimer` | Break reminders |

## Going from minimal to extra

Run the script again with `-X`. Already-installed packages are skipped and only the missing ones are added:

```sh
bash ./zorin.sh -X
```

Add the version flag (`-6`, `-7` or `-8`) if you want to skip the automatic detection, and `-U` if you do not want to confirm each step.
