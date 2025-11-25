# Offline Form

This project provides a simple and effective way to save and restore HTML form data, allowing for offline usage and re-editable forms. The script captures the current state of all form fields and saves the entire HTML page with the data embedded.

## Features

- **Save Form Data**: Save the current state of your form, including text inputs, textareas, checkboxes, radio buttons, and select fields.
- **Offline Usage**: The saved file is a self-contained HTML document that can be opened and edited without an internet connection.
- **Data Restoration**: When the saved HTML file is opened, the form fields are automatically repopulated with the saved data.
- **No Dependencies**: The script is written in plain JavaScript and requires no external libraries.

## How to Use

1.  **Add the script to your HTML**: Copy the following JavaScript code and place it within the `<head>` section of your HTML file.

    ```html
    <script>
        function saveAs() {
            const inputs = document.getElementsByTagName("input");
            const textareas = document.getElementsByTagName("textarea");
            const selects = document.getElementsByTagName("select");

            for (let input of inputs) {
                input.setAttribute("value", input.value);
                if (input.type === "checkbox" || input.type === "radio") {
                    input.checked ? input.setAttribute("checked", "checked") : input.removeAttribute("checked");
                }
            }

            for (let textarea of textareas) {
                textarea.innerHTML = textarea.value;
            }

            for (let select of selects) {
                for (let option of select.options) {
                    option.selected ? option.setAttribute("selected", "selected") : option.removeAttribute("selected");
                }
            }

            const contentToSave = document.documentElement.outerHTML;
            const blob = new Blob([contentToSave], { type: "text/html;charset=utf-8" });
            const url = URL.createObjectURL(blob);
            const a = document.createElement("a");
            a.href = url;
            a.download = `${document.title.replace(/ /g, "_")}_${new Date().toISOString().slice(0, 10)}.html`;
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(url);
        }

        // Restore saved values when the document is loaded
        document.addEventListener("DOMContentLoaded", function() {
            const inputs = document.getElementsByTagName("input");
            const textareas = document.getElementsByTagName("textarea");
            const selects = document.getElementsByTagName("select");

            for (let input of inputs) {
                if (input.hasAttribute("value")) {
                    input.value = input.getAttribute("value");
                }
                if (input.hasAttribute("checked")) {
                    input.checked = true;
                }
            }

            for (let textarea of textareas) {
                textarea.value = textarea.innerHTML;
            }

            for (let select of selects) {
                for (let option of select.options) {
                    if (option.hasAttribute("selected")) {
                        option.selected = true;
                    }
                }
            }
        });
    </script>
    ```

2.  **Add a "Save" button**: Place a button in your HTML's `<body>` section to trigger the save function.

    ```html
    <button type="button" onclick="saveAs()">Save to Disk</button>
    ```

Now, when you open the HTML file in a browser, you can fill out the form and click the "Save to Disk" button. A new HTML file with the entered data will be downloaded to your computer. When you open the downloaded file, the form will be pre-filled with your data.

## Examples

You can find more examples of how to use this script in the `examples/` directory.

## Contributing

Contributions are welcome! If you have any improvements or bug fixes, feel free to open an issue or submit a pull request.