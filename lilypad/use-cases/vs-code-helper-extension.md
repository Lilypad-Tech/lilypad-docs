---
description: >-
  An integrated development environment for running AI workloads on the Lilypad
  Network directly within Visual Studio Code.
---

# 💻 VS Code Helper Extension

The **Lilypad VS Code Extension** allows developers to interact with the Lilypad Anura API within Visual Studio Code. By highlighting code blocks, users can query the available LLMs on Lilypad  for explanations, improvements, or suggestions, receiving responses in a formatted webview panel.

### Features

* **AI-Powered Code Assistance** – Select any code in your editor, choose an AI model, and ask Lilypad questions about it
* **Formatted Responses** – View AI-generated insights in a structured webview panel
* **Secure API Configuration** – Store your Lilypad API token securely
* **Context Menu Integration** – Quickly access the extension’s features via the right-click menu

### Installation

From the Repository

1. Get [Anura API key](https://anura.lilypad.tech/).
2. Clone the repo: `git clone git@github.com:PBillingsby/lilypad-vscode-extension.git`
3. Install the extension in VS Code: `code --install-extension lilypad-vscode-extension.vsix`
4. Add Anura API key to `.env`:  `LILYPAD_API_TOKEN=<ANURA_API_KEY>`
5. If you make changes to the extension and need to recompile it:
   1. Recompile the code: `npm run compile`
   2. Repackage the extension: `vsce package`
   3. Reinstall the updated `.vsix` file: `code --install-extension lilypad-vscode-extension.vsix`

### **Usage**

1. **Select a block of code** in your editor.
2. **Right-click** and select **"Ask Lilypad about this code"**, or:
   * Open the **Command Palette** (`Ctrl+Shift+P`) and select **"Ask Lilypad about this code"**.
3. **Choose an AI model** to process the query.
4. **Enter your question** related to the selected code.
5. **Wait for Lilypad AI** to process your query.
6. **View the AI’s response** in the webview panel that opens.

<figure><img src="../.gitbook/assets/Screenshot 2025-03-10 at 3.05.20 PM.png" alt=""><figcaption><p>Example use</p></figcaption></figure>

### Resources

* [Source code](https://github.com/PBillingsby/lilypad-vscode-extension)

