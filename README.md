# DraftVault

> [!WARNING]
> **BETA ONLY — DraftVault is currently in beta.** It is experimental software and may contain bugs or behavior changes. Do not rely on it as your only copy of important drafts.

DraftVault is a local Discord draft-history plugin for **Vencord and Equicord**. It automatically keeps previous text versions of your unsent messages so you can search, browse, and restore a draft to Discord's composer without sending it.

## Preview

This short recording, captured by the author, demonstrates the DraftVault interface and its draft-browsing and restore workflow.

[▶ Watch the DraftVault preview](docs/preview.mp4)

## Features

- Automatically saves text draft versions when Discord's native DraftStore updates, with a 550 ms debounce.
- Captures outgoing draft text just before sending, so a quick send is not missed by the debounce.
- Keeps separate history for channels, DMs, group DMs, and threads.
- Search by server, conversation, or saved text.
- Restore a saved version to Discord's composer. **Restoring never sends a message.**
- Delete individual versions or clear a conversation's history.
- Uses the client's local DataStore; DraftVault does not send drafts to an external service.

## Installation

DraftVault is a **source-build userplugin** for Vencord and Equicord. It is not installed through the regular plugin list in prebuilt clients.

### Already built Vencord or Equicord from source?

1. Download and extract the [Download DraftVault 0.1.0 beta](https://github.com/d12w/DraftVault/raw/refs/heads/main/DraftVault-0.1.0-beta.zip).
2. Move the entire **DraftVault** folder from the extracted ZIP into your client source directory:

       src/userplugins/DraftVault/

   Do not copy the files individually.
3. From the Vencord or Equicord source root, run:

       pnpm build
       pnpm inject

4. Restart Discord if needed, then enable **DraftVault** in **Settings → Plugins**.

### Build Vencord from source

If you have not built Vencord yet, install Git, Node.js LTS, and pnpm, then clone the source:

    git clone https://github.com/Vendicated/Vencord.git
    cd Vencord
    pnpm install --frozen-lockfile

Next, extract the DraftVault beta package and move its entire **DraftVault** folder into:

    src/userplugins/DraftVault/

Then, from the Vencord source root, run:

    pnpm build
    pnpm inject

Enable **DraftVault** in **Settings → Plugins** after restarting Discord.

For a visual walkthrough of building Vencord from source, see:

[YouTube — Build Vencord from source](https://www.youtube.com/watch?v=XmVNRKrphlw)

### Build Equicord from source

For Equicord, use its own repository and source directory:

    git clone https://github.com/Equicord/Equicord.git
    cd Equicord
    pnpm install --frozen-lockfile

Extract the DraftVault beta package and move its entire **DraftVault** folder into:

    src/userplugins/DraftVault/

Then, from the Equicord source root, run:

    pnpm build
    pnpm inject

Enable **DraftVault** in **Settings → Plugins** after restarting Discord.

## How to use

1. Open DraftVault using the vault icon in the chat toolbar, or choose **Open DraftVault** from the client toolbox.
2. Select a conversation and browse its saved versions.
3. Choose **Restore this draft** to return to that conversation and restore the text to the composer.
4. Use the delete control beside a version to remove it, or **Clear history** to clear that conversation's saved drafts.

## Privacy and limitations

- DraftVault stores **text only**. It does not save or restore attachments, uploads, stickers, or other composer state.
- Drafts are stored locally through the client's DataStore (IndexedDB), separated by Discord user ID. The plugin does not make network requests or send draft contents to an external service.
- Drafts are sensitive and are **not independently encrypted** by DraftVault. Protect your local Discord/Vencord/Equicord data directory.
- Very recent typing may not be captured until Discord emits a native draft-store update.
- Keeps up to **25 versions per conversation**, for **30 days**, across up to **60 conversations**.
- This release is experimental. A full live-client build and restore test has not been completed for every Vencord/Equicord version.

## License

GPL-3.0-or-later.
