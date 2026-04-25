# Plugin Development

This guide is for people making custom MCP plugins for `MCPServerV2`.

## Start with 1.21.8

If you are making your first MCP plugin, test it on `1.21.8` first.

That version is the main reference flow for the current plugin host.

## How MCP plugins work

At runtime, the stack looks like this:
- Paper runs the Minecraft server
- Paper loads the `MCPServerCore` plugin
- `MCPServerCore` scans the `MCPPlugins` folder
- each plugin folder is read through `plugin.mcp`
- matching Lua functions from `plugin.lua` are called for events or commands

So MCP plugins are not normal Paper jar plugins.
They are folder-based plugins hosted by `MCPServerCore`.

## Plugin folder layout

A minimal plugin usually looks like this:

```text
plugins\\MCPPlugins\\my-first-plugin\\
plugins\\MCPPlugins\\my-first-plugin\\plugin.mcp
plugins\\MCPPlugins\\my-first-plugin\\plugin.lua
```

For the current `1.21.8` reference setup, that usually means:

```text
server\\plugins\\MCPPlugins\\my-first-plugin\\
server\\plugins\\MCPPlugins\\my-first-plugin\\plugin.mcp
server\\plugins\\MCPPlugins\\my-first-plugin\\plugin.lua
```

## Your first plugin

### Step 1: create `plugin.mcp`

```text
plugin "my-first-plugin"
version "1.0.0"
main "plugin.lua"

command "starter" -> "onStarter"
event "server.start" -> "onServerStart"
event "player.join" -> "onPlayerJoin"
```

### Step 2: create `plugin.lua`

```lua
function onServerStart(api, event)
    api:log("my-first-plugin loaded successfully")
end

function onPlayerJoin(api, event)
    local playerName = event:get("player")
    api:reply("&aWelcome " .. playerName .. " from my-first-plugin!")
end

function onStarter(api, event)
    local sender = event:get("sender")
    api:reply("&bStarter command worked for " .. sender .. "!")
end
```

## What happens when it runs

- `plugin.mcp` tells MCPServer which Lua functions should handle which commands or events
- when the server starts, `server.start` can trigger `onServerStart`
- when a player joins, `player.join` can trigger `onPlayerJoin`
- when a player runs `/starter`, MCPServer can call `onStarter(api, event)`

## Testing flow

1. Put the plugin folder into the active `MCPPlugins` directory
2. Restart the server
3. Watch the server output for plugin load messages
4. Join the server
5. Run the test command such as `/starter`

## What to look for in logs

A good load usually includes messages that show:
- `MCPServerCore` was enabled
- the MCP plugin was loaded
- the plugin folder was scanned successfully

If the plugin is not behaving correctly, check for:
- bad `plugin.mcp` syntax
- a function name in `plugin.mcp` that does not exist in `plugin.lua`
- event names or command names that do not match your test

## Good beginner habits

- keep plugin names simple and lowercase to start
- change one thing at a time while testing
- start with one command and one event before building bigger logic
- test on `1.21.8` before trying older versions

## Next page

For the exact currently documented plugin interface, see [Plugin Reference](plugin-reference.md).
