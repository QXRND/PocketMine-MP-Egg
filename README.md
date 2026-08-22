# QXRND - PocketMine-MP Pterodactyl Egg

![Pterodactyl](https://img.shields.io/badge/Pterodactyl-PTDL_v2-1055CC)
![Platform](https://img.shields.io/badge/platform-Minecraft%20Bedrock-55C2E6)
![Maintainer](https://img.shields.io/badge/maintainer-DevPapo-2F81F7)

This repository contains a Pterodactyl Egg for deploying the QXRND - PocketMine-MP Bedrock server distributions. The Egg provides a single installation definition with a version selector for PM4, PM5, and PM6. The selected branch determines the server PHAR, PHP runtime, release source, and installation behavior.

The Egg is an infrastructure distribution mechanism. It does not alter PocketMine-MP gameplay semantics, plugin APIs, permissions, or server commands. Those behaviors are defined by the selected QXRND distribution.

## Supported distributions

| Selector | API line | Bedrock target | Protocol | PHP runtime | Release source |
|---|---:|---:|---:|---:|---|
| `PM4` | 4.26.0 | 1.26.44 | 2168 | PHP 8.1 | [QXRND/PocketMine-MP-PM4](https://github.com/QXRND/PocketMine-MP-PM4/releases/latest) |
| `PM5` | 5.44.5 | 1.26.44 | 2168 | PHP 8.2 | [QXRND/PocketMine-MP-PM5](https://github.com/QXRND/PocketMine-MP-PM5/releases/latest) |
| `PM6` | 6.0.0 | 1.26.44 | 2168 | PHP 8.3 | [QXRND/PocketMine-MP-PM6](https://github.com/QXRND/PocketMine-MP-PM6/releases/tag/qxrnd-26.44) |

All published server assets use the exact filename `PocketMine-MP.phar`. PM4 and PM5 resolve the latest release asset from their respective repositories. PM6 is intentionally pinned to the stable `qxrnd-26.44` release so that production installations do not change implicitly.

## Installation workflow

Import [`egg-pmmp.json`](./egg-pmmp.json) into the target Pterodactyl installation through **Nests → Import Egg**. Create a server from the imported Egg and set the `Version to install` variable to one of `PM4`, `PM5`, or `PM6`.

The installer performs the following operations:

1. Installs the required Debian packages used by the installation process.
2. Selects the corresponding PHP binary distribution.
3. Creates the expected `bin/php7/bin/php` runtime path.
4. Downloads the selected QXRND PHAR as `PocketMine-MP.phar`.
5. Creates the standard PocketMine-MP data directories and server files.
6. Leaves the server ready for the configured startup command.

The generated startup command is:

```text
./bin/php7/bin/php ./PocketMine-MP.phar --no-wizard --disable-ansi
```

When changing the selected version or replacing an existing PHAR, use **Reinstall Server**. Changing the variable and pressing **Start** does not execute the installation script again and therefore does not replace an already-installed PHAR.

## Runtime and platform requirements

The Egg currently targets x86_64 Linux containers using the Debian-based Pterodactyl images. The selected PHP runtime must match the API branch: PHP 8.1 for PM4, PHP 8.2 for PM5, and PHP 8.3 for PM6.

The server requires writable storage for worlds, plugins, resource packs, configuration files, logs, and the PHAR extraction cache. The node must permit outbound HTTPS access for runtime and PHAR downloads, and the server allocation must expose the required Bedrock UDP port.

The PHP binaries are downloaded from the QXRND PHP-Binaries distribution. They are not interchangeable across the PM4, PM5, and PM6 branches.

## Configuration behavior

The Egg configures `server.properties` with the Pterodactyl allocation and enables query support. It does not overwrite gameplay configuration after installation. Server-specific settings remain in the generated PocketMine-MP configuration files.

The selected QXRND distributions provide their own branch-level settings, including the configurable `/say` prefix where implemented. This Egg only installs and launches the distribution; it does not implement those server features.

## Release and update policy

The release policy is intentionally conservative. Small source and configuration changes are consolidated into the existing stable release asset instead of creating a new release for every change.

PM4 and PM5 use the latest GitHub release endpoint and select the asset named `PocketMine-MP.phar`. PM6 uses an explicit release URL:

```text
https://github.com/QXRND/PocketMine-MP-PM6/releases/download/qxrnd-26.44/PocketMine-MP.phar
```

When changing the PM6 release, update the pinned URL in `egg-pmmp.json`, commit the Egg change, re-import the Egg, and run **Reinstall Server**. A normal server restart will not download a new asset.

## Release matrix

| Distribution | Stable release | PHAR download |
|---|---|---|
| PM4 | [`v4.26.0-qxrnd.3`](https://github.com/QXRND/PocketMine-MP-PM4/releases/tag/v4.26.0-qxrnd.3) | [`PocketMine-MP.phar`](https://github.com/QXRND/PocketMine-MP-PM4/releases/download/v4.26.0-qxrnd.3/PocketMine-MP.phar) |
| PM5 | [`v5.44.5-qxrnd.8`](https://github.com/QXRND/PocketMine-MP-PM5/releases/tag/v5.44.5-qxrnd.8) | [`PocketMine-MP.phar`](https://github.com/QXRND/PocketMine-MP-PM5/releases/download/v5.44.5-qxrnd.8/PocketMine-MP.phar) |
| PM6 | [`qxrnd-26.44`](https://github.com/QXRND/PocketMine-MP-PM6/releases/tag/qxrnd-26.44) | [`PocketMine-MP.phar`](https://github.com/QXRND/PocketMine-MP-PM6/releases/download/qxrnd-26.44/PocketMine-MP.phar) |

## Repository layout

| File or directory | Purpose |
|---|---|
| [`egg-pmmp.json`](./egg-pmmp.json) | Importable Pterodactyl Egg definition. |
| [`README.md`](./README.md) | Deployment, runtime, release, and maintenance documentation. |
| `LICENSE` | Licensing terms for this Egg repository. |

## Operational troubleshooting

If installation fails while downloading PHP, inspect the selected version, architecture, and the corresponding QXRND PHP-Binaries release. If the server starts with an old implementation after changing a version variable, perform **Reinstall Server** and confirm that `/mnt/server/PocketMine-MP.phar` has a current modification timestamp.

If the PHAR fails during startup with a disk-space error, increase the server allocation or use the minimal PHAR supplied by the relevant QXRND release. The error is generated during PHAR extraction and is not an out-of-memory condition.

If a player cannot connect, inspect the server crash dump and confirm that the installed PHAR, API branch, PHP runtime, and Bedrock protocol target are consistent. Do not mix PHAR files or PHP runtimes between PM4, PM5, and PM6.

## Related repositories

| Resource | Link |
|---|---|
| PM4 source and distribution | [QXRND/PocketMine-MP-PM4](https://github.com/QXRND/PocketMine-MP-PM4) |
| PM5 source and distribution | [QXRND/PocketMine-MP-PM5](https://github.com/QXRND/PocketMine-MP-PM5) |
| PM6 source and distribution | [QXRND/PocketMine-MP-PM6](https://github.com/QXRND/PocketMine-MP-PM6) |
| Upstream lineage | [pmmp/PocketMine-MP](https://github.com/pmmp/PocketMine-MP) |
| PHP binary distribution | [QXRND/PHP-Binaries](https://github.com/QXRND/PHP-Binaries) |
| Technical support and invitation | [QXRND Discord](https://discord.gg/qhUXn72rGB) |

## Credits and legal notice

This Egg and its release integration are maintained and published by **DevPapo**. The deployed server distributions are downstream projects based on the PocketMine-MP ecosystem. PocketMine-MP, Minecraft, Minecraft Bedrock, Mojang, and Microsoft are the property of their respective owners. This repository is not affiliated with or endorsed by Mojang, Microsoft, or the PocketMine-MP maintainers.
