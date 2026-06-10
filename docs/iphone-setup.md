# Whispr on iPhone — one-tap voice capture

Goal: tap once on your iPhone, speak, and the transcript lands as text in your chosen Obsidian folder.

## 1. Get your vault on the iPhone

Obsidian mobile can only open vaults stored in **Obsidian's iCloud folder** or **local device storage** (or synced via Obsidian Sync). Pick one:

- **iCloud (free):** On iPhone, open Obsidian → Create/open a vault stored in iCloud. On the Mac, the same vault appears at `~/Library/Mobile Documents/iCloud~md~obsidian/Documents/<VaultName>`. Move or sync your vault there.
- **Obsidian Sync (paid):** syncs any vault, including `.obsidian` settings, end-to-end encrypted.

## 2. Install Whispr on mobile

The plugin files (`main.js`, `manifest.json`, `styles.css`) live in `.obsidian/plugins/whispr/` inside the vault. If your sync method includes the `.obsidian` folder (iCloud does; Obsidian Sync needs "Installed community plugins" enabled in Sync settings), the plugin arrives automatically.

On iPhone: Settings → Community plugins → turn off Restricted mode → enable **Whispr**.

## 3. Add your API key on the iPhone

API keys are stored in Obsidian's SecretStorage, which is **per-device by design** (keys never sync through your vault files — this is a security feature). Enter your Whisper API key once in Whispr's settings on the phone.

## 4. Configure where transcripts go

In Whispr settings:

- **Create note file**: on
- **Note save path**: the vault folder you want memos filed into (e.g. `Inbox/Voice`)
- **Note filename template**: `{{datetime}}` (or enable post-processing + auto-title)

## 5. One-tap capture with the Shortcuts app

Whispr registers an Obsidian URI, so any URL-opener can drive it:

```
obsidian://whispr?command=start   start recording
obsidian://whispr?command=stop    stop and transcribe
```

Create two shortcuts in the **Shortcuts** app:

1. **"Record idea"** — single action: *Open URLs* → `obsidian://whispr?command=start`
2. **"Save idea"** — single action: *Open URLs* → `obsidian://whispr?command=stop`

Then surface them however you like:

- **Home Screen icon** (Shortcuts → ⋯ → Add to Home Screen)
- **Action Button** (Settings → Action Button → Shortcut → Record idea)
- **Back Tap** (Settings → Accessibility → Touch → Back Tap)
- **Siri**: "Hey Siri, record idea"

Tap *Record idea* → Obsidian opens and recording starts immediately → speak → tap *Save idea* (or the stop button in Obsidian) → transcript is created in your chosen folder.

## Troubleshooting

- **Mic permission**: iOS will prompt the first time; Obsidian needs microphone access (Settings → Obsidian → Microphone).
- **Nothing happens on the URI**: the plugin must be enabled in that vault, and the vault must be the last-opened one (URIs open the most recent vault unless you add `&vault=YourVault`).
- **"Add your API key"**: keys don't sync between devices — set it on the phone (step 3).
