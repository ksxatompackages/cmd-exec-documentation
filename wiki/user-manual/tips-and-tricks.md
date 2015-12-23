
# Tips and Tricks

## Quick close

*Description: when you open a console, you may want to close it quickly without having to use your mouse, the following instructions will show you how to close that console by pressing <kbd>ESC</kbd>.*

**First of all**, you need [this package](https://atom.io/packages/enable-pane-item-control-helper)
```bash
	apm install enable-pane-item-control-helper
```

### Type 1: Close console immediately when press <kbd>ESC</kbd>

*Description: When you press <kbd>ESC</kbd>, the pane item which contains the console will be destroyed instantly.*

Steps:

1. Open your config.cson, go to the command which you want to add this feature

2. Set property `classes` to be an array which contains `"enable-pane-item-control-helper"` and `"able-to-be-closed"`

3. Open your keymap.cson, and add:
```coffeescript
	'.enable-pane-item-control-helper.able-to-be-closed':
		'esc': 'package-pane-item-control-helper:close'
```

### Type 2: Press <kbd>ESC</kbd> to clear input box or close console

*Description: When you press <kbd>ESC</kbd>, Atom would close the pane item which contains the console if the input box is empty, or clear the input otherwise*

Steps:

1. *(Same as step 1 above)*

2. Set property `classes` to be an array which contains `"enable-pane-item-control-helper"` and `"check-before-close"`

3. Open your keymap.cson, and add:
```coffeescript
	'.enable-pane-item-control-helper.check-before-close':
		'esc': 'package-pane-item-control-helper:close-if-accepted'
```
