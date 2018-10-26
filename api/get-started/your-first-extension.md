---
Order: 1
Area: get-started
TOCTitle: Your First Extension
PageTitle: Your First Extension
---

# Your First Extension

In this section, we'll teach you fundamental concepts for building VS Code extensions. The following topics are centered around the [Hello Code](https://github.com/Microsoft/vscode-extension-samples/tree/ext-docs/hellocode-sample) sample extension. Download and run it:

```
git clone https://github.com/Microsoft/vscode-extension-samples
cd vscode-extension-samples/hellocode-sample
npm install
code .
# Press F5 in editor
# Run the `Hello Code` command
```

(Gif for running Hello Code extension here)

You should see the `Hello Code` information dialog showing up. Success!

## Behind the Scenes

When you type a URL and press Enter in a browser, you go to a website. However, [a lot happens](https://github.com/alex/what-happens-when) behind that seemingly simple action. Simiarly, when you press `Hello Code`, a lot happens behind the scene:

- VS Code launches the extension in an **"Extension Host"**, as specified in `.vscode/launch.json`
  - The `Run Extension` launch config contains a `preLaunchTask`. The task compiles `src/extension.ts` to `out/extension.js`.
  - VS Code starts in extension development mode and loads the extension.
  - VS Code executes `out/extension.js`, as specified in the `main` field of `package.json`.
- In `package.json`, VS Code finds an **[Activation Event](/api/references/activation-events)**: `"onCommand:extension.helloCode"`.
- In `package.json`, VS Code also finds a **[Contribution Point](/api/references/contribution-points)**: the `Hello Code` command with id `extension.helloCode`.
- `Hello Code` command becomes available in the [Command Palette](/docs/getstarted/userinterface#_command-palette).
- You run the `Hello Code` command.
- The extension is activated.
  - The `activate` function in `our/extension.js` is invoked.
  - `vscode.commands.registerCommand('extension.helloCode', callback)` registers the `extension.helloCode` command.
  - The extension calls the command callback that uses `vscode.window.showInformationMessage` **[vscode API](/api/references/vscode-api)**.
- The message `Hello Code` appears.

This is a long list! Don't worry — in the following section, [Extension Anatomy](/api/getting-started/extension-anatomy), we'll explain these concepts in detail:

- Extension Host
- [Activation Events](/api/references/activation-events)
- [Contribution Points](/api/references/contribution-points)
- [vscode API](/api/references/vscode-api)

However, if you can't wait to start writing code, try these things:

- Give `Hello Code` command a new name.
- Make the extension display a new message.
- Replace the `vscode.window.showInformationMessage` with another [vscode API](/api/references/vscode-api) call to show a warning message.

Once you make some change, run the `Reload Window` command in the extension development window and you'll be running the new version of the extension. The TypeScript task defined in `.vscode/tasks.json` compiles the code as you make changes.

## Using JavaScript

In this guide, we mainly describe how to develop VS Code extension with TypeScript, because we believe TypeScript gives you the best developing experience. However, if you prefer to use JavaScript, you can still follow along using [hellocode-minimap-sample](https://github.com/Microsoft/vscode-extension-samples/tree/ext-docs/hellocode-minimal-sample).