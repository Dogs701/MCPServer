# Getting Started

This guide is for people who want to run `MCPServerV2` for the first time.

## What MCPServerV2 is

MCPServerV2 is a Windows-friendly Minecraft server launcher built around Paper.

It helps prepare a server by automating the early setup steps that people usually do by hand:
- Java detection
- Paper server download
- EULA setup
- version selection
- RAM selection
- tunnel helper setup
- plugin host support through `MCPServerCore`

## First launch flow

1. Unzip the release folder anywhere you want
2. Double-click `start.bat`
3. Choose the Minecraft version you want to run
4. Choose how much RAM to give the server
5. Wait while MCPServer prepares the server files
6. If the tunnel helper shows a claim link, open it once in your browser
7. Wait for the server to finish loading

## Joining the server

Use one of these addresses depending on where you are playing from:
- `localhost` if you are joining from the same computer hosting the server
- the public join address if you are on another computer

The public join address is usually shown in the server output and saved to `JOIN-ADDRESS.txt`.

## What to expect on first startup

The first startup may take longer than later startups because MCPServer may need to:
- download the Paper server jar
- create the world and server files
- prepare folders
- download server-side runtime dependencies
- initialize the tunnel helper

This is normal.

## Recommended version for plugin testing

If you want to test or create MCP plugins, start with `1.21.8` first.

That is the cleanest reference version for the current MCP plugin host flow.

## Common beginner tips

- Keep the server window open while the server is running
- Use `stop.bat` if the server needs to be stopped and the original window is gone or stuck
- If Java is missing, install a JDK and run `start.bat` again
- Different Minecraft versions may need different Java versions

## Next docs

After this page, the most useful next pages are:
- [Server Usage](server-usage.md)
- [Plugin Development](plugin-development.md)
