# Releases

This page explains the intended package structure around `MCPServerV2`.

## Full server package

### `MCPServerV2.zip`

This is the main package for:
- server owners
- testers
- players hosting a server for friends
- plugin authors who want the full runtime environment

It should contain the full server launcher package, including:
- startup scripts
- setup files
- server folders
- plugin host source/runtime pieces
- sample MCP plugin content

Use this package if you want to actually run MCPServerV2.

Direct repo file:
- [downloads/MCPServerV2.zip](../downloads/MCPServerV2.zip)

## Plugin starter package

### `MCPPluginBase.zip`

This is the starter package for plugin authors.

It should contain a simple MCP plugin template, usually including:
- `plugin.mcp`
- `plugin.lua`
- a short README or usage note

Use this package if you want a starting point for building your own plugin folder.

Direct repo file:
- [downloads/MCPPluginBase.zip](../downloads/MCPPluginBase.zip)

## Recommended use flow

### If you want to host a server
Download and use:
- `MCPServerV2.zip`

### If you want to learn plugin creation
Download and study:
- `MCPPluginBase.zip`

### If you want both
Start with:
- `MCPServerV2.zip`

Then use:
- `MCPPluginBase.zip`

## Current documentation assumption

The repository docs currently describe MCP plugin creation using the `1.21.8` reference flow first.

That is the easiest place to understand and test the current plugin host behavior before expanding to additional version-specific flows.
