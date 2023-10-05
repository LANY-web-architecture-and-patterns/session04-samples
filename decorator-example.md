# Decorator Pattern Example

Here's the complete HTML page integrating the JavaScript and CSS code for the enhanced web button using the Decorator pattern:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Decorator Pattern Example</title>
    <style>
        .tooltip-wrapper {
            position: relative;
            display: inline-block;
        }

        .tooltip-text {
            visibility: hidden;
            background-color: black;
            color: #fff;
            text-align: center;
            border-radius: 6px;
            padding: 5px;
            position: absolute;
            z-index: 1;
            bottom: 125%;
            left: 50%;
            margin-left: -60px;
            opacity: 0;
            transition: opacity 0.3s;
        }

        .tooltip-wrapper:hover .tooltip-text {
            visibility: visible;
            opacity: 1;
        }

        .shadow-wrapper button {
            box-shadow: 3px 3px 5px rgba(0, 0, 0, 0.3);
        }
    </style>
</head>
<body>

<script>
    class WebButton {
        render() {
            return `<button>Click me!</button>`;
        }
    }

    class TooltipDecorator {
        constructor(button, tooltipText) {
            this.button = button;
            this.tooltipText = tooltipText;
        }

        render() {
            return `
                <div class="tooltip-wrapper">
                    ${this.button.render()}
                    <span class="tooltip-text">${this.tooltipText}</span>
                </div>
            `;
        }
    }

    class ShadowDecorator {
        constructor(button) {
            this.button = button;
        }

        render() {
            return `
                <div class="shadow-wrapper">
                    ${this.button.render()}
                </div>
            `;
        }
    }

    const basicButton = new WebButton();
    const buttonWithTooltip = new TooltipDecorator(basicButton, "I am a tooltip!");
    const buttonWithTooltipAndShadow = new ShadowDecorator(buttonWithTooltip);

    // Render the enhanced button
    document.body.innerHTML = buttonWithTooltipAndShadow.render();
</script>

</body>
</html>
```

In this HTML page, the CSS is embedded within a `<style>` tag in the `<head>` section, and the JavaScript is embedded within a `<script>` tag in the `<body>`. When you open this HTML page in a browser, you'll see a button with a shadow. Hovering over the button will display a tooltip with the text "I am a tooltip!".