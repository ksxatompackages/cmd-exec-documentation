
# User Manual

## Create/Modify commands

### Open config.cson

In Atom's menu bar, go to File &rarr; Open Your Config.
Or, open Command Palette, type: "Application: Open Your Config" (which is `application:open-your-config`)

### Create `cmd-exec.commands`

 * See this [example config.cson](../../examples/config.cson#L12)
 * See this [specs](../specs/config.cmd-exec.commands.txt)

Create property `cmd-exec` to store an object, and property `commands` of this object is an array, each element of that array is an object which has the following structure

 - Property `target`: An array which contains "target" strings which commands will be registered in, e.g. `"atom-workspace"`, `"atom-text-editor"`...

 - Property `data`: *An array* which contains *key-value pair objects* has the structure below

  - Key: An atom command which will be registered to `atom.commands` (e.g. `"my-cmd:bash"`, `my-cmd:compile`), so it available in Command Palette, and you are able to create shortcut key and menu item for it.

  - Value: A string which contains shell command (as same as `path` of Command Properties Structure when `type` is `"spawn"`) or an object of which has *Command Properties Structure* (see below).

 - Command Properties Structure

  - Property `type` (required): One of `"spawn"`, `"fork"`, `"require"`, `"eval"`.

  - Property `path` (required): A string. If `type` is `"spawn"`, `path` is a shell command which would be executed. If `type` is `"fork"`, `path` should leads to a JavaScript file which would run as a independent [node](https://nodejs.org) process. If `type` is `"require"`, `path` should leads to a node module, would be executed once, and return a function which would be invoked when you execute the command (see "Key" above), by this way, you can hack atom UI. If `type` is `"eval"`, `path` should leads to a JavaScript file which would be executed in an isolated context.

  - Property `useJSTemplateString` (optional): If `true`, `path` will be read as a JavaScript template string, this property is `false` by default.

  - Property `wdir` (optional): Determines "current working directory", makes sense only if `type` is `"spawn"` or `"fork"`. If not specified, use directory of activated file (which opened by the activated tab).

  - Property `console` (optional): If `true`, a console would be opened, makes sense only of `type` is `"spawn"` or `"fork"`, this property is `false` by default.
  
  - Property `attached` (optional): If `true`, the spawned child process would be attach to atom process. Learn more: [child_process](https://nodejs.org/api/child_process.html#child_process_child_process_spawn_command_args_options); [options.detached](https://nodejs.org/api/child_process.html#child_process_options_detached)

  - Property `closeOnExit` (optional): If `true`, console would be closed right after stdio stream is close (i.e. all processes which uses that stream finished), makes sense only if `console` is `true`, this property is `false` by default.

  - Property `hideInputText` (optional): If `true`, console would not display text which was entered by the user, makes sense only if `console` is `true`. this property is `false` by default.

  - Property `utils` (optional): An array which contains names of some special utilities which would be executed instead of being written to stdin when console is opening, e.g. `"clear"`, `"exit"`, `"start"`, `"beep"` and [more](https://github.com/ksxatompackages/cmd-exec/blob/master/lib/special-commands.js#L98).

  - Property `paneItemPosition` (optional): Either `"left"`, `"right"`, `"up"`, or `"down"`, it would override `config.command-executor.pane-item-position`, determine where console should be located, makes sense only if `console` is `true`.

  - Property `classes` (optional): An array contains CSS classes which would be added to console view.

## Executing command

Open Command Palette, type command from that "Key" (see above: Property `data`)

## See also
 * [Tips and Tricks](./tips-and-tricks.md)

# FAQ

## I want to copy selected text in console
This package is for you: https://atom.io/package/enable-clipboard-helper
