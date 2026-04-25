# Plugin Reference

This page documents the current MCP plugin interface as a v1 author-facing contract.

## Plugin location

Custom MCP plugins go into the active server plugin folder under:
- `plugins\\MCPPlugins\\<plugin-name>`

For the main `1.21.8` reference setup, that is usually:
- `server\\plugins\\MCPPlugins\\<plugin-name>`

## Required plugin shape

Each plugin should live in its own folder.

A minimal plugin folder contains:
- `plugin.mcp`
- the Lua file referenced by `main`, usually `plugin.lua`

## plugin.mcp DSL

The current documented DSL lines are:
- `plugin "name"`
- `version "x.y.z"`
- `main "plugin.lua"`
- `command "name" -> "luaFunction"`
- `event "event.name" -> "luaFunction"`

### Example

```text
plugin "my-first-plugin"
version "1.0.0"
main "plugin.lua"

command "starter" -> "onStarter"
event "server.start" -> "onServerStart"
event "player.join" -> "onPlayerJoin"
```

## Current event support

The currently documented event names are:
- `server.start`
- `player.join`

### Current event data

#### `server.start`
Current examples may include values such as:
- `pluginCount`

#### `player.join`
Current examples may include:
- `player`
- `uuid`

## Current command support

Commands are declared in `plugin.mcp` and mapped to Lua functions.

Example:

```text
command "starter" -> "onStarter"
```

That means a slash command like `/starter` can trigger the Lua function `onStarter(api, event)`.

### Current command event data

Command handlers currently receive event data such as:
- `sender`
- `message`

## Lua function form

The current function form is:

```lua
function myFunction(api, event)
end
```

## Current helper methods on `api`

The currently documented helper methods are:
- `log(message)`
- `reply(message)`
- `colorize(message)`

### Intent of each helper

- `log(message)`: write a plugin message to the server log
- `reply(message)`: send a visible response from the plugin host
- `colorize(message)`: apply the server color formatting rules used by the host

## Current `event` access pattern

Use `event:get("key")` to read event data.

Example:

```lua
local playerName = event:get("player")
```

## Architecture summary

The MCP plugin system currently works like this:
- Paper loads `MCPServerCore`
- `MCPServerCore` scans `MCPPlugins`
- `plugin.mcp` tells the host what to bind
- `plugin.lua` contains the behavior that gets called

## Example minimal plugin

```text
plugin "my-first-plugin"
version "1.0.0"
main "plugin.lua"

command "starter" -> "onStarter"
```

```lua
function onStarter(api, event)
    local sender = event:get("sender")
    api:reply("&bStarter command worked for " .. sender .. "!")
end
```

## Current scope note

This reference documents the currently working v1 plugin flow.

It does not promise future features beyond the currently described bindings, helpers, and folder-based plugin model.
