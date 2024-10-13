# About

`snippets` plugin is designed to work with simple Vim `.snippets` snippets (e.g. [these][honza/vim-snippets])

The plugin is shipped with snippets, typically at `~/.config/micro/plug/snippets/snippets/[filetype].snippets`.

Add custom snippets there, or submit a pull request to include the snippets in the next version.

## Commands

The plugin provides the following commands:

| Command         | Key     | Description                                                                     |
|-----------------|---------|---------------------------------------------------------------------------------|
| `snippetinsert` | `Alt+S` | Insert a snippet: specify in parameter, or word left to the cursor will be used |
| `snippetnext`   | `Alt+W` | proceeds to the next placeholder                                                |
| `snippetcancel` | `Alt+D` | removes all the current snippet                                                 |
| `snippetaccept` | `Alt+A` | finishes the snippet editing for the current snippet                            |

## Snippet File syntax

Extension is designed with *tab stops* snippet syntax in mind.

* Lines starting with `#` are comments & are not interpreted;
* Lines starting with `snippet` mark a beginning of a new snippet;
	* This keyword supports multiple shortcuts, e.g. `snippet name1 name2`, at least one shortcut is required;
* Every line of the snippet starts with a tab (`\t`);
* Snippets support *tab stop* placeholders indexed by numbers - `${num[:name]}`:
	* Placeholders have shared value by number:
		* E.g. `$1` or `${1}` placed anywhere in the snippet will be repplaced with the same value;
	* Placeholders can have an optional default value:
		* E.g. `${2:default}` will insert `default` text in place of an unfilled placeholder;
* Backtick ` [``] ` syntax can be used for [sunbstitution][subs] functions.

Plugins can provide additional `.snippets` files as *runtime* files. Execute `help plugins` for additional details.

### Substitutions

*TODO*

### Examples

+ `go.snip`:

```
# creates a function that prints a value
snippet fmtfunc
	func ${0:name}() {
		fmt.Println("${0} prints:", ${1:value})
	}
```

## Custom Key Bindings

Changes to the keybindings should be specified in `~/.config/micro/bindings.json`.

Execute `help keybindings` for details.

### Examples

```json
{
	"Alt-w": "snippets.Next",
	"Alt-a": "snippets.Accept",
	"Alt-s": "snippets.Insert",
	"Alt-d": "snippets.Cancel"
}
```

### Raw key codes

You can use `raw` command in `micro` command line (accessed through `Ctrl+E` by default) to capture & display escape sequences for every event in the terminal.

This shows you what `micro` actually receives from the terminal and helps you determine which bindings aren't possible and why. Useful for keybinding debug.

Execute `help keybindings` for details.

#### Examples

+ `"\u001bctrlback": "DeleteWordLeft"`

[subs]: #Substitutions
[honza/vim-snippets]: https://github.com/honza/vim-snippets/tree/master/snippets
