# CustomRunelite

This repository preserves the official RuneLite history and keeps our plugin
source separate from the client. It is independent of BScriptz/runelite.

## Upstream updates and builds

The `Sync and build CustomRunelite` GitHub Actions workflow checks official
`runelite/runelite` master every 30 minutes. GitHub schedules may be delayed.
It merges new upstream commits, runs the official build and tests, and uploads
the shaded client JAR as a workflow artifact. Only a successful build is pushed
to master. Failed builds or merge conflicts leave the published branch alone
and are visible in GitHub Actions. The workflow can also be run manually.

This tracks upstream development commits, not just tagged stable releases.
A successful build is not proof of compatibility with third-party plugins.
It does not automatically replace a running or installed Windows client.

Do not add plugin implementations to the client repository. Keep each plugin
we maintain in its own repository and compile it against the intended client
API. The standard Plugin Hub remains available for hub plugins.

## Shared Windows data

The local checkout is G:\CustomRunelite. RuneLite derives its data directory
from the Java user.home property, so running it as Bradl normally uses:

    C:\Users\Bradl\.runelite

That includes profiles, settings, logs, plugin-data, and sideloaded-plugins.
No data copy or new symlink is needed merely because the source moved.
Do not override user.home or run under another Windows account when sharing
this existing data. Existing plugin-specific symlinks must be preserved.

A directly launched shaded client supports sideloading in developer mode:

    java -ea -jar path-to-client-shaded.jar --developer-mode

Own plugin JARs belong in C:\Users\Bradl\.runelite\sideloaded-plugins.
Do not put a complete client or a plugin with a bundled client in that folder.

## Pending integration

- Move geToolKit into a clearly named independent repository, preserving source.
- Verify Omega's separate sideload distribution and supported RuneLite version.
  The Omega 0.27.1 Windows package is a bundled development client whose README
  explicitly says its omega-plugin-all.jar must not be put in sideloaded-plugins.
- Configure and verify the Jagex Launcher entry point before switching clients.
- Add a local installer/updater that promotes a verified artifact while retaining
  the previous working client. Cloud builds alone do not update the local client.

The existing G:\Runelite installation and VitaLite are not managed by this repo.
