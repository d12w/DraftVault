# DraftVault

> [!WARNING]
> **BETA ONLY — DraftVault is currently in beta.** It is experimental software and may contain bugs or behavior changes. Use it with that in mind and keep important drafts backed up elsewhere.

DraftVault is a local Discord draft-history plugin for **Vencord and Equicord**. It automatically saves earlier text versions of your unsent messages and lets you search, browse, and restore them to Discord's composer without sending anything.

## Preview

A short preview recorded by the author shows the DraftVault interface and how saved drafts are browsed and restored.

[▶ Watch the DraftVault preview video](docs/preview.mp4)

## Features

- Automatically saves text draft versions as you type, with a short debounce.
- Keeps separate history for channels, DMs, group DMs, and threads.
- Search saved drafts by conversation or text.
- Restore a saved version directly to Discord's composer. **Restoring never sends the message.**
- Delete individual versions or clear a conversation's history.
- Local storage only: no external API, telemetry, or third-party server.

## Installation

DraftVault is a **source-build userplugin**. It is intended for Vencord and Equicord builds that support src/userplugins.

### Already built Vencord or Equicord from source?

1. Download and extract the [DraftVault 0.1.0 beta package](DraftVault-0.1.0-beta.zip).
2. Move the entire **DraftVault** folder from the extracted ZIP into your client source directory:

       src/userplugins/DraftVault/

   Do not copy the files individually.
3. From the Vencord or Equicord source root, run:

       pnpm build
       pnpm inject

4. Restart Discord if needed, then enable **DraftVault** in **Settings → Plugins**.

### Build Vencord from source

If you have not built Vencord from source yet, install Git, Node.js LTS, and pnpm, then run:

    git clone https://github.com/Vendicated/Vencord.git
    cd Vencord
    pnpm install --frozen-lockfile
    pnpm build
    pnpm inject

Then follow the steps above to move DraftVault into src/userplugins/DraftVault/, rebuild, and enable it.

For a visual walkthrough of building Vencord from source, see:

[YouTube — Build Vencord from source](https://www.youtube.com/watch?v=XmVNRKrphlw)

### Build Equicord from source

For Equicord, use the Equicord repository and its own source tree:

    git clone https://github.com/Equicord/Equicord.git
    cd Equicord
    pnpm install --frozen-lockfile
    pnpm build
    pnpm inject

Then follow the same plugin-folder steps above, moving the entire DraftVault folder into src/userplugins/DraftVault/, rebuilding, and enabling it in **Settings → Plugins**.

## How to use

1. Open DraftVault using the vault icon in the chat toolbar, or choose **Open DraftVault** from the client toolbox.
2. Select a conversation and browse its saved versions.
3. Choose **Restore this draft** to return to that conversation and put the selected text back into the composer.
4. Use the delete control beside a version to remove it, or **Clear history** to clear that conversation's saved drafts.

## Privacy and limitations

- DraftVault stores **text only**. It does not save or restore attachments, uploads, stickers, or other composer state.
- Drafts are stored locally through the client's DataStore and separated by Discord user ID. They are not sent to an external server.
- Drafts are sensitive and are **not independently encrypted** by DraftVault. Protect your local Discord/Vencord/Equicord data directory.
- Autosaves follow Discord's native DraftStore updates and use a 550 ms debounce. Very recent typing may not be captured until Discord emits an update.
- Keeps up to **25 versions per conversation** for **30 days**, across up to **60 conversations**.
- This release is experimental. Full source-client builds and live restore testing have not been completed for every Vencord/Equicord version.

## License

GPL-3.0-or-later.
