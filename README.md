 # NaviBot Community Plugins

  A community-maintained collection of Lua
  plugins for [NaviBot](https://github.com/Sew
  dohe/NaviBot) — a hot-reloadable Discord bot
   with a Rust core and Lua plugin system.

  Plugins in this repo are browseable and
  installable directly from the NaviBot TUI:
  press **`p`** to open the Plugin Browser.

  ---

  ## Installing a Plugin

  No manual file copying needed. From the
  NaviBot TUI:

  1. Press **`p`** to open the Plugin Browser
  2. Use **`Up`/`Down`** to browse available
  plugins
  3. Press **`Enter`** to install the selected
   plugin
  4. Press **`r`** to hot-reload — the plugin
  is now active
  5. Run **`!sync`** in Discord if the plugin
  registers slash commands

  To remove a plugin, select it in the browser
   and press **`d`**, then **`r`** to reload.

  ---

  ## Contributing a Plugin

  ### 1. Write your plugin

  Plugins are standard `.lua` files using the
  `navi.*` API. A minimal example:

  ```lua
  -- plugins/myplugin.lua

  navi.register_config("myplugin", {
      { key = "greeting", name = "Greeting
  Text", type = "string", default = "Hello!" }
  })

  navi.create_slash("greet", "Send a
  greeting", {}, function(ctx)
      local msg = navi.db.get("greeting")
      ctx.reply(msg, true)
  end)
  ```

  See the [NaviBot API
  reference](https://github.com/Sewdohe/NaviBo
  t/blob/main/navi_api.lua) for the full
  `navi.*` surface.

  ### 2. Add your file

  Place your plugin at:
  ```
  plugins/yourplugin.lua
  ```

  The filename (without `.lua`) becomes the
  plugin's `id` in the manifest and the
  namespace for all `navi.db` keys.

  ### 3. Register it in `manifest.json`

  Add an entry to the `plugins` array in
  `manifest.json`:

  ```json
  {
    "id": "yourplugin",
    "name": "Your Plugin Name",
    "description": "One or two sentences
  describing what it does.",
    "author": "your-github-username",
    "version": "1.0.0",
    "tags": ["utility"],
    "url":
  "https://raw.githubusercontent.com/Sewdohe/n
  avibot-plugins/main/plugins/yourplugin.lua"
  }
  ```

  **Field reference:**

  | Field | Required | Notes |
  |---|---|---|
  | `id` | ✅ | Must match the `.lua` filename
   (no extension). Lowercase, no spaces. |
  | `name` | ✅ | Human-readable display name
  shown in the TUI |
  | `description` | ✅ | Short summary shown
  in the details pane |
  | `author` | ✅ | Your GitHub username or
  handle |
  | `version` | ✅ | Semver string, e.g.
  `"1.0.0"` |
  | `tags` | ✅ | Array of category strings —
  use existing tags where possible |
  | `url` | ✅ | Raw GitHub URL to the `.lua`
  file |

  ### 4. Open a Pull Request

  Submit a PR with both your `.lua` file and
  the updated `manifest.json`. A maintainer
  will review and merge it.

  ---

  ## Plugin Guidelines

  - **No network calls from Lua** — use the
  `navi.*` API only; raw HTTP from Lua is not
  supported
  - **Namespace your DB keys** —
  `navi.db.get/set` auto-prefix with your
  plugin filename, so no collisions
  - **One feature per plugin** — keep plugins
  focused; users can install multiple
  - **No destructive defaults** — don't delete
   data on load; be safe to hot-reload
  - **Test before submitting** — run the bot
  locally with your plugin loaded

  ---

  ## Available Tags

  Use these tags to help users find your
  plugin:

  `economy` · `fun` · `moderation` · `utility`
   · `leveling` · `logging` · `roles` ·
  `games` · `music` · `admin`

  Feel free to propose new tags in your PR if
  none fit.

  ---

  ## Repo Layout

  ```
  manifest.json        ← index of all plugins
  (edit this when adding a plugin)
  plugins/
    economy.lua
    leveling.lua
    ...
  ```
