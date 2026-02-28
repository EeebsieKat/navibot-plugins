  # CLAUDE.md

  This repo hosts community Lua plugins for [NaviBot](https://github.com/Sewdohe/NaviBot),
  a Discord bot with a Rust core and hot-reloadable Lua plugin system.

  ## Your job when asked to create a plugin

  1. Create `plugins/<id>.lua` — the filename stem is the plugin ID
  2. Add an entry to `manifest.json`
  3. That's it — no Rust changes needed

  ## Manifest entry format

  ```json
  {
    "id": "myplugin",
    "name": "Human Readable Name",
    "description": "One or two sentences.",
    "author": "your-handle",
    "version": "1.0.0",
    "tags": ["utility"],
    "url": "https://raw.githubusercontent.com/Sewdohe/navibot-plugins/main/plugins/myplugin.lua"
  }
  ```

  The `id` must exactly match the `.lua` filename stem. The `url` must use `raw.githubusercontent.com`.

  ## Writing plugins

  See `lua_api_refrence.md` for the complete API. Key rules:

  - **All plugin state is global** — use unique variable names to avoid collisions
  - **DB keys**: `navi.db.get("key")` auto-prefixes with the plugin filename. If a key contains `:` it is used as-is
  - **Config values** are stored at `config:<plugin>:<key>` — read them with `navi.db.get("config:myplugin:mykey")`
  - **`msg.channel_id` and `msg.author_id`** are u64 integers — use `tostring()` before using as table keys or in `navi.send_message()`
  - **`ctx.channel_id`** from slash commands is already a string
  - **`navi.say(channel_id, text)`** takes a u64 channel_id
  - **`navi.send_message(channel_id, data)`** takes a string channel_id
  - Do not make HTTP calls from inside `navi.set_interval` callbacks — only from slash command handlers or message listeners

  ## Available tags

  `economy` · `fun` · `moderation` · `utility` · `leveling` · `logging` · `roles` · `games` · `music` · `admin`