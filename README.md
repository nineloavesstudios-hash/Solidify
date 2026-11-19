# Solidify

Solidify is a lightweight, browser-based tool that converts code into an SVG file by embedding a webpage inside an SVG `<foreignObject>`. The generated SVG uses an HTML iframe with `srcdoc` to display the embedded content.

It is useful for packaging HTML-based projects into a single SVG file that can be opened or embedded in supported browsers and applications.

## Features

- **Paste code:** Add your code directly into the editor.
- **Upload files:** Load local text-based code files from your device.
- **Multiple input formats:** Choose how the input should be interpreted.
- **Live preview:** Preview the generated page inside the tool.
- **SVG source:** View and copy the complete generated SVG markup.
- **Download:** Save the result as an `.svg` file with a customizable filename.
- **Local processing:** Your input is read and converted in your browser. The tool does not send it to a server.
- **Simple interface:** A compact, dark-gray workspace with separate input and output panels.

## Supported Input Formats

| Format | What it does |
| --- | --- |
| **Complete HTML document** | Uses the supplied HTML document as-is. |
| **HTML fragment** | Wraps the supplied markup in a basic HTML document. |
| **JavaScript** | Places the supplied JavaScript inside a `<script>` element in a basic HTML document. |
| **CSS** | Places the supplied CSS inside a `<style>` element in a basic HTML document. |
| **Plain text** | Displays the supplied text in a preformatted code-style block. HTML-sensitive characters are escaped so the text is displayed rather than interpreted as markup. |

## How to Use

1. Open `SolidifySVGConverter.html` in a modern web browser.
2. Choose an input format from the format dropdown.
3. Paste your code into the editor, or select **Choose file** to upload a text-based code file. You can also drop a file into the upload area.
4. Select **Generate SVG**.
5. Use the **SVG code** tab to view the generated markup, or select **Preview** to view the embedded page.
6. Select **Copy code** to copy the SVG markup, or enter a filename and select **Download SVG** to save the file.

Select **Clear** to reset the input and generated output. You can also press `Ctrl + Enter` (or `Cmd + Enter` on macOS) while focused in the code editor to generate the SVG.

## How the SVG Works

The tool converts the selected input into an HTML document, then URL-encodes that document and places it inside an SVG wrapper. The wrapper contains:

- An SVG `<foreignObject>` element, which allows HTML content inside the SVG.
- An XHTML `<div>` that fills the available viewport.
- An HTML `<iframe>` that displays the page through its `srcdoc` attribute.
- A small SVG script that decodes the embedded document and assigns it to the iframe.

The result keeps the supplied HTML document inside the SVG instead of requiring a separate HTML file for the embedded page itself.

## Important Notes

- **Use a compatible display method.** Open the generated SVG directly, or embed it with an `<object>` or `<iframe>`. Browsers generally disable SVG scripting when an SVG is used through a normal `<img>` element, so the embedded page may not run that way.
- **Browser support can vary.** SVG `<foreignObject>`, SVG scripting, and iframe `srcdoc` behavior depend on the browser and how the SVG is loaded.
- **External resources remain external.** If your code references remote scripts, stylesheets, images, fonts, or other files, those resources still need to be reachable when the SVG is opened.
- **Preview is sandboxed.** The preview iframe allows scripts, forms, and modal dialogs, but does not grant every browser permission. Its behavior may differ from opening the downloaded SVG.
- **Only upload text-based files.** The tool reads uploaded files as text; it is not intended for binary files.
- **Review code before previewing it.** HTML and JavaScript you provide can run in the preview. Only preview code you trust.

## Privacy

The conversion happens locally in the browser. The tool does not include an API endpoint or upload your code to a server. External resources referenced by the code may still make their own network requests when the preview or generated SVG is opened.

## License

This project is licensed under the [MIT License](LICENSE).
