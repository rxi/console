# Console
A console plugin for the [Lite XL text editor](https://github.com/lite-xl/lite-xl)

This version of the plugin is adapted from the [console plugin](https://github.com/rxi/console) for the [lite editor](https://github.com/rxi/lite).

![gif](https://user-images.githubusercontent.com/3920290/81343656-49325a00-90ad-11ea-8647-ff39d8f1d730.gif)

## Install
Navigate to the `data/plugins` folder and run the following command:
```bash
git clone https://github.com/franko/console
```
Alternatively the `init.lua` file can be renamed `console.lua` and dropped in
the `data/plugins` folder.

## Basic Usage
A basic command can be ran in the console by using the `console:run` command
(`ctrl+shift+.`). The default console view at the bottom of the screen can be
toggled with `ctrl+.`; additional console views can be opened with the
`console:open-console` command.

## Build Systems
Following is an example of how you can set up a build system for a project. This
code should be put in the project module (accessed by running the
`core:open-project-module` command):

```lua
local core = require "core"
local command = require "core.command"
local keymap = require "core.keymap"
local console = require "plugins.console"

command.add(nil, {
  ["project:build-project"] = function()
    core.log "Building..."
    console.run {
      command = "./build.sh",
      file_pattern = "(.*):(%d+):(%d+): (.*)$",
      cwd = "."
      on_complete = function(retcode) core.log("Build complete with return code "..retcode) end,
    }
  end
})

keymap.add { ["ctrl+b"] = "project:build-project" }
```

The `console.run` function can be also invoked with an additional option named `file_prefix`.
If specified the prefix will be added to the file names reported in the console to help resolve them within the project.
It can be useful when the build happens in a subdirectory of the project.

## License
This project is free software; you can redistribute it and/or modify it under
the terms of the MIT license. See [LICENSE](LICENSE) for details.

