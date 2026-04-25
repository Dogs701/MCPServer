# MCPServerV2

`MCPServerV2` is the packaged release name for the `MCPServer` project: a beginner-friendly Minecraft server launcher for Windows with a built-in custom MCP plugin system.

It is designed to help two groups at once:
- Server owners who want to launch a Paper server without manually doing the full setup by hand
- Plugin makers who want to create custom MCP plugins using a readable `plugin.mcp` file and a `plugin.lua` script

## What MCPServerV2 does

MCPServerV2 automates the usual early setup work for a Paper-based Minecraft server:
- Detects Java and checks whether the selected Minecraft version can run on it
- Downloads and prepares a Paper server on first launch
- Accepts the Minecraft EULA automatically for the local setup flow
- Lets you choose Minecraft version and RAM from a simple prompt
- Sets up a tunnel helper so you can share the server without a manual port-forwarding workflow
- Restarts the server automatically if it crashes
- Hosts custom MCP plugins through `MCPServerCore`

## What makes it different

A normal Paper setup usually expects the user to handle Java, server jars, folders, startup commands, and networking details manually.

MCPServerV2 wraps that into a simpler Windows-friendly launcher flow and also adds a custom plugin system on top of Paper:
- Normal Paper plugins are jar files
- MCP plugins are folder-based plugins that use `plugin.mcp` and `plugin.lua`

That means plugin authors can start with a small readable DSL file plus Lua logic instead of immediately building a full Java Paper plugin jar.

## Who this is for

### Server owners
Use MCPServerV2 if you want to:
- start a Minecraft server quickly
- avoid a more manual Paper setup flow
- share a server with friends more easily
- keep the startup process beginner friendly

### MCP plugin developers
Use MCPServerV2 if you want to:
- create custom plugins with Lua
- bind commands and events through a simple DSL
- prototype plugin behavior on `1.21.8`
- learn the MCP plugin host before building more advanced features

## How it works

At a high level, MCPServerV2 works like this:
1. `start.bat` launches the setup flow
2. MCPServer prepares or downloads the correct Paper server for the selected version
3. Paper loads the `MCPServerCore` plugin host
4. `MCPServerCore` scans the MCP plugin folder
5. Each MCP plugin folder is read through `plugin.mcp`
6. Matching Lua functions from `plugin.lua` are called for registered commands and events

In other words:
- Paper is still the actual Minecraft server base
- `MCPServerCore` is the bridge that makes custom MCP plugins possible
- MCP plugins are layered on top of Paper rather than replacing it

## Quick Start

1. Download or unpack the MCPServerV2 release folder
2. Double-click `start.bat`
3. Choose a Minecraft version
4. Choose a RAM amount
5. Wait for first-time setup to finish
6. Join with `localhost` on the host computer, or use the public join address shown by the tunnel helper

Important notes:
- Keep the server window open while the server is running
- `1.21.8` is the easiest reference version for MCP plugin development right now
- Different Minecraft versions may require different Java versions

## Creating MCP plugins

An MCP plugin is usually a folder that contains:
- `plugin.mcp`
- `plugin.lua`

The plugin folder goes into the active server plugin folder under:
- `plugins\\MCPPlugins\\<your-plugin-name>`

For the current `1.21.8` reference flow, that will usually be:
- `server\\plugins\\MCPPlugins\\<your-plugin-name>`

`plugin.mcp` describes the plugin and binds commands or events to Lua functions.

`plugin.lua` contains the Lua code that actually runs when those bindings are triggered.

Short example:

```text
plugin "my-first-plugin"
version "1.0.0"
main "plugin.lua"

command "starter" -> "onStarter"
event "player.join" -> "onPlayerJoin"
```

```lua
function onPlayerJoin(api, event)
    local playerName = event:get("player")
    api:reply("&aWelcome " .. playerName .. " from my-first-plugin!")
end

function onStarter(api, event)
    local sender = event:get("sender")
    api:reply("&bStarter command worked for " .. sender .. "!")
end
```

## Documentation

Detailed repo-side docs live in the [`docs`](docs) folder:
- [Getting Started](docs/getting-started.md)
- [Server Usage](docs/server-usage.md)
- [Plugin Development](docs/plugin-development.md)
- [Plugin Reference](docs/plugin-reference.md)
- [Releases](docs/releases.md)

## Releases and packages

The current release structure is intended to separate the full server package from the starter plugin package:
- `MCPServerV2.zip`: full server package for players, hosts, and testers
- `MCPPluginBase.zip`: starter MCP plugin template for plugin authors

## Project status

This repository is being used as the main documentation hub before the GitHub wiki is built out.

That means the README should help brand new users understand the product quickly, while the `docs/` folder should give plugin authors the deeper detail they need to start building.
