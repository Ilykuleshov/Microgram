# Microgram

**Microgram** is a lightweight fork of [Telegram for Android](https://github.com/DrKLO/Telegram), focused on private messaging without the noise of broadcast channels and global discovery features.

Based on Telegram **12.9.0** (build 6966).

## What is different from Telegram

| Feature | Telegram | Microgram |
|---------|----------|-----------|
| Broadcast channels | Full support | Disabled — cannot create, join, or browse channels |
| Existing channel chats | Shown in chat list | Hidden from the chat list |
| Supergroups (megagroups) | Supported | Supported |
| Global / server search | Full support | Disabled — search is limited to your local chats |
| Apps / Mini Apps search tab | Available | Removed |
| Channels search tab | Available | Removed |
| App name & icon | Telegram | Microgram (custom branding) |
| Package ID | `org.telegram.messenger` | `app.microgram.messenger` |

Microgram keeps direct messages, groups, supergroups, secret chats, calls, and the rest of the core messaging experience.

## Philosophy

Microgram strips away one-to-many broadcast and global discovery layers so the app stays closer to personal and small-group communication — a "micro" messenger built on Telegram's protocol and codebase.

## Building

Microgram follows the same build process as upstream Telegram, with a few fork-specific notes.

### Requirements

- Android Studio (recent version recommended)
- Android NDK
- Your own Telegram API credentials from [my.telegram.org](https://my.telegram.org)

### Setup

1. Clone this repository:
   ```bash
   git clone https://github.com/Ilykuleshov/Microgram.git
   cd Microgram
   ```

2. Copy `local.properties.example` to `local.properties` and fill in your values (API credentials, keystore path, and signing passwords). Place your `release.keystore` at `TMessagesProj/config/release.keystore` unless you set `RELEASE_KEYSTORE_PATH`.

3. Add `google-services.json` for Firebase (application ID: `app.microgram.messenger` for release, `app.microgram.messenger.beta` for debug).

4. Open the project in Android Studio (open, do not import).

5. Build and run.

### Fork configuration

Microgram-specific flags live in `SharedConfig.java`:

```java
public static final boolean CHANNELS_ENABLED = false;
public static final boolean GLOBAL_SEARCH_ENABLED = false;
```

## Syncing with upstream

An `upstream` remote pointing to `https://github.com/DrKLO/Telegram` is recommended:

```bash
git remote add upstream https://github.com/DrKLO/Telegram.git
git fetch upstream
git merge upstream/master
```

After merging, re-check `SharedConfig.java` and the Microgram-specific changes in `ChatObject.java`, `MessagesController.java`, `SearchViewPager.java`, and `SearchAdapterHelper.java`.

## License

Microgram is based on Telegram for Android, licensed under **GNU GPL v. 2 or later**. See [LICENSE](LICENSE).

Per Telegram's guidelines for third-party clients:

- Do not distribute this as "Telegram".
- Use your own API credentials.
- Publish your source code to comply with the GPL.

## Links

- Upstream source: https://github.com/DrKLO/Telegram
- Telegram API: https://core.telegram.org/api
- MTProto protocol: https://core.telegram.org/mtproto
