# Day 1: Terrabitez Launchpad Setup 🚀

Welcome to my first **Terrabitez** challenge! Today, it's all about getting my Cloud IaC workstation ready. No fluff, just the essentials to kick off this legendary journey. 🛠️✨

---

## The Essentials: My IaC Toolbox 📦

Here’s the fast-track to setting up my environment, primarily using PowerShell!

### 1. Visual Studio Code: My Code Canvas 🎨
* **Download:** Grab it from [code.visualstudio.com](https://code.visualstudio.com/).
* **Install:** Follow the prompts. Done!

### 2. Git: Version Control Virtuoso 🔄
* **Download:** Get the installer from [git-scm.com/downloads](https://git-scm.com/downloads).
* **Install:** Run the executable; defaults are usually fine.
* **Verify in PS:** `git --version` (Confirms Git is ready to roll!)

### 3. AWS CLI: Cloud Communicator ☁️
* **Download:** Get the `.msi` installer from [aws.amazon.com/cli](https://aws.amazon.com/cli/).
* **Install:** Run it and follow the wizard.
* **Verify in PS:** `aws --version` (Should show version details!)

### 4. Terraform CLI: The Infrastructure Sculptor 🏗️
* **Download:** Find the `.zip` for Windows at [developer.hashicorp.com/terraform/downloads](https://developer.hashiCorp.com/terraform/downloads).
* **Install:** Unzip the `terraform.exe` file and move it to a folder already in your system's PATH (like `C:\Windows\System32` or your custom bin folder).
* **Verify in PS:** `terraform --version` (Look for version details!)

### 5. VS Code Extensions: Supercharge My Editor 💻
* **Open VS Code.**
* **Extensions View:** Click the 🧩 icon (or `Ctrl+Shift+X`).
* **Install These Essentials:**
    * **Terraform** (by HashiCorp) - *The absolute must-have for HCL!*
    * **Material Icon Theme** (for pretty icons!)
    * **Indent Rainbow** (for visual clarity!)

---

## Verification Checkpoint ✅

Quick check in PowerShell to confirm everything's humming:

* `code --version`
* `git --version`
* `aws --version`
* `terraform --version`

---

### Troubleshooting `PATH` Errors (The Common Culprit! 😤)

If you see an error like `'aws' is not recognized...` or `'git' is not recognized...`, it means your system can't find the executable. Don't fret! It's almost always a **`PATH` environment variable** issue.

**Quick Fixes:**
1.  **Restart PowerShell/Terminal:** Sometimes, new `PATH` changes just need a refresh.
2.  **Verify PATH:** Ensure the folder containing `git.exe`, `aws.exe`, and `terraform.exe` is correctly added to your system's `PATH` environment variable. (A quick Google for "add to system path Windows" helps here!)
3.  **Reinstall:** If all else fails, a fresh reinstall of the tool often resolves the `PATH` configuration automatically.

---

## What's Next? ➡️

Setup complete! Time to start crafting some **TerraBitez!** My first challenge awaits!
