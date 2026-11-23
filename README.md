# DraftVault

> [!WARNING]
> **BETA ONLY — DraftVault is experimental software and may contain bugs or behavior changes. Do not rely on it as the only copy of important drafts.**

DraftVault is a local Discord draft-history plugin for **Vencord and Equicord**. It saves previous versions of unsent text drafts so you can search, browse, compare, and restore them without sending a message.

## Update — 0.3.1 Beta

- Added a scrollable draft timeline that automatically loads 50 older versions as you reach the bottom. You no longer need to delete newer drafts to reach older ones.
- Added protected conversations, side-by-side version comparison, JSON backup export/import, and a storage monitor with an optional storage limit.
- Reworked retention and storage: removed the fixed revision and conversation-count caps, added compact delta storage, and introduced configurable inactivity-based cleanup.

## Download

[Download DraftVault 0.3.1 Beta](https://github.com/d12w/DraftVault/raw/refs/heads/main/DraftVault-0.3.1-beta.zip)

## Preview

Watch the author-recorded preview:

[Google Drive — DraftVault Preview](https://drive.google.com/file/d/13kVLufr7euWAeP52E6kGI1i1UrHSaaGj/view?usp=sharing)

## Features

- Automatically saves draft versions when Discord's native DraftStore updates, with a 550 ms debounce.
- Captures draft text just before sending to reduce missed quick sends.
- Keeps separate history for channels, DMs, group DMs, and threads.
- Search by server, conversation, or saved text.
- Restore a saved version to Discord's composer. Restoring never sends it.
- Browse an independently scrollable history; older batches load automatically near the bottom.
- Protect important conversations from automatic cleanup and storage-cap trimming.
- Compare two versions and highlight added and removed text.
- Export and import history as JSON backups. Imports merge with existing history and skip duplicate version IDs rather than overwriting existing data.
- Monitor estimated local storage usage and optionally set a maximum storage size.

## Retention and storage

DraftVault has no fixed per-conversation revision cap or fixed conversation-count cap. The practical limit is the local storage quota available to Discord/IndexedDB on your device.

The **Retention period** setting controls how long a conversation can remain without a newly saved draft before its history is automatically deleted. The default is `1mo`. Supported units:

| Value | Meaning |
| --- | --- |
| `1s` | 1 second |
| `1m` | 1 minute |
| `1h` | 1 hour |
| `1mo` | 1 month (30 days) |
| `1y` | 1 year (365 days) |

Saving a new version resets that conversation's inactivity period. Simply opening or browsing its history does not reset the timer. Protected conversations are excluded from inactivity cleanup.

To reduce storage use, DraftVault stores compact differences between versions when they are smaller than the full text and creates periodic full checkpoints. The optional **Maximum storage (MB)** setting trims older unprotected versions first, while keeping the newest version in each conversation. Protected histories are not trimmed; the configured cap may therefore be exceeded when protected or newest versions alone require more space.

The JSON backup contains readable draft text and conversation identifiers. Keep backup files private. DraftVault does not independently encrypt draft contents.

## Installation

DraftVault is a **source-build userplugin**. It is not installed through the regular plugin list in prebuilt clients.

### Already built Vencord or Equicord from source?

1. Download and extract the [DraftVault 0.3.1 Beta ZIP](https://github.com/d12w/DraftVault/raw/refs/heads/main/DraftVault-0.3.1-beta.zip).
2. Move the entire **DraftVault** folder from the extracted ZIP into:
   
       src/userplugins/DraftVault/

   Do not copy the files individually.
3. From the client source root, run:

       pnpm build
       pnpm inject

4. Restart Discord if needed, then enable **DraftVault** in **Settings → Plugins**.

### Build Vencord from source

Install Git, Node.js LTS, and pnpm, then run:

    git clone https://github.com/Vendicated/Vencord.git
    cd Vencord
    pnpm install --frozen-lockfile

Move the entire **DraftVault** folder into `src/userplugins/DraftVault/`, then run:

    pnpm build
    pnpm inject

For a visual walkthrough, see [YouTube — Build Vencord from source](https://www.youtube.com/watch?v=XmVNRKrphlw).

### Build Equicord from source

Use the Equicord repository:

    git clone https://github.com/Equicord/Equicord.git
    cd Equicord
    pnpm install --frozen-lockfile

Move the entire **DraftVault** folder into `src/userplugins/DraftVault/`, then run:

    pnpm build
    pnpm inject

After restarting Discord, enable **DraftVault** in **Settings → Plugins**.

## Limitations and privacy

- DraftVault stores **text only**. It does not save or restore attachments, uploads, stickers, or other composer state.
- Each draft is limited to 10,000 characters.
- Drafts are stored locally through the client's DataStore/IndexedDB, separated by Discord user ID. DraftVault does not send draft contents to an external service.
- Draft contents are not independently encrypted by DraftVault. Protect your local Discord/Vencord/Equicord data directory and exported backups.
- Very recent typing may not be captured until Discord emits a native draft-store update.
- A full live-client build and restore test has not been completed for every Vencord/Equicord version. This release remains experimental.

## License

GPL-3.0-or-later.
