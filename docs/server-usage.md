# Server Usage

This page explains the important files, folders, and runtime behavior of `MCPServerV2`.

## Important files

These are the files most users will interact with:
- `start.bat`: starts the setup and launch flow
- `stop.bat`: stops a running server if needed
- `setup.txt`: plain-language setup and plugin guide
- `JOIN-ADDRESS.txt`: saved public join address for friends
- `logs/`: launcher logs and troubleshooting output

## Important folders

### Main server folder
For the current default `1.21.8` reference flow, the active server is usually under:
- `server`

### Version instances
For other supported versions, MCPServer may prepare instance folders such as:
- `server\\instances\\<minecraft-version>`

That means different Minecraft versions may not all share the exact same active server folder.

## Plugin folders

There are two plugin concepts in MCPServerV2:

### Paper plugin host
`MCPServerCore` is a Paper plugin jar that acts as the custom MCP plugin host.

### MCP plugin folders
Your custom MCP plugins go into the active server's MCP plugin folder:
- `plugins\\MCPPlugins\\<plugin-name>`

For the normal `1.21.8` reference setup, that usually means:
- `server\\plugins\\MCPPlugins\\<plugin-name>`

## Stop and restart behavior

Use `stop.bat` if:
- the server window is gone but the process is still running
- the port still looks busy
- you want a cleaner forced stop before restarting

Use `start.bat` again after stopping if you need to relaunch the server.

## Logs

If something goes wrong, check:
- the newest file in `logs/`
- the active server's own log files

Logs are useful for checking:
- startup failures
- Java issues
- Paper download problems
- MCP plugin load messages
- Lua/plugin runtime errors

## Version behavior

MCPServer supports multiple Minecraft versions, but plugin testing is easiest on `1.21.8` first.

Why:
- it is the main reference path for the current MCP plugin system
- the `MCPServerCore` host flow is easiest to validate there first
- older versions may need different Java/runtime preparation steps

## Troubleshooting basics

### Java missing
Install a JDK, then run `start.bat` again.

### Server says it is already running
Use `stop.bat`, then start again.

### First launch is slow
That is normal while files and runtime dependencies are being prepared.

### Public address not showing up yet
Wait for the tunnel helper to finish initializing and watch the logs/output for the join address.
