# Command Pattern

Let's take the example of a simple web-based text editor that uses the Command pattern to implement undo and redo actions.

## HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Command Pattern Example: Text Editor</title>
</head>
<body>
    <div>
        <button onclick="addTextCmd.execute()">Add Text</button>
        <button onclick="undo()">Undo</button>
        <button onclick="redo()">Redo</button>
    </div>
    <div id="editor" contenteditable="true" style="border: 1px solid black; min-height: 200px;"></div>

    <script>
        class Command {
            execute() {}
            undo() {}
        }

        class AddTextCommand extends Command {
            constructor(editor, text) {
                super();
                this.editor = editor;
                this.text = text;
                this.previousText = '';
            }

            execute() {
                this.previousText = this.editor.innerHTML;
                this.editor.innerHTML += this.text;
                commandHistory.push(this);
            }

            undo() {
                this.editor.innerHTML = this.previousText;
            }
        }

        let commandHistory = [];
        let undoStack = [];
        const editorElement = document.getElementById('editor');
        const addTextCmd = new AddTextCommand(editorElement, '<br>Hello, World!');

        function undo() {
            if (commandHistory.length > 0) {
                const lastCommand = commandHistory.pop();
                lastCommand.undo();
                undoStack.push(lastCommand);
            }
        }

        function redo() {
            if (undoStack.length > 0) {
                const lastUndoneCommand = undoStack.pop();
                lastUndoneCommand.execute();
                commandHistory.push(lastUndoneCommand);
            }
        }
    </script>
</body>
</html>

```

**In this example**:

- The `Command` class provides a basic structure for commands with `execute()` and `undo()` methods.
- The `AddTextCommand` class extends `Command` and represents an action to add text to the editor. It also remembers the previous state of the editor to perform the undo operation.
- `commandHistory` keeps track of executed commands.
- `undoStack` keeps track of commands that have been undone.
- The buttons in the HTML allow the user to add text, undo the last action, or redo an undone action.

When you load this HTML in a browser, you can add text to the editor with the "Add Text" button. The "Undo" and "Redo" buttons allow you to undo or redo the addition of the text. This demonstrates the Command pattern in action, providing an extensible system for managing operations and their inversions.