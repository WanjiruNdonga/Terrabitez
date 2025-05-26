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
* **Download:** Get the `.msi` installer from [docs.aws.amazon.com/cli](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).
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
    * **Hashicorp Terraform** - *The absolute must-have for HCL!*
    * **Hashicorp HCL** - *Helps with syntax & code magic!*
    * **AWS Toolkit** (by Amazon Web Services) - *Directly manage AWS resources right from VS Code! Essential for AWS interaction.*
    * **Material Icon Theme** (for pretty icons!)
    * **Indent Rainbow** (for visual clarity!)

![VS extensions](https://github.com/user-attachments/assets/fef04f61-233d-4258-a5a2-bb2b6441c01b)


![AWS IAM](https://github.com/user-attachments/assets/e7b518aa-e6a0-43c9-a415-ae23394577be)

---

## Challenge Repo: Get It Local! 📦

Now that your tools are ready, it's time to get the actual challenge code onto your machine!

### The Fork 🍴 (Before You Clone!)
**Why:** You need your own personal copy of the main challenge repository to work on and submit your solutions without affecting the original.
**How:**
1.  Go to the official challenge repo on GitHub (e.g., `https://github.com/Challenge-Repo-`).
2.  In the top-right corner, click the **"Fork"** button.
3.  Confirm to create your copy under your GitHub account (e.g., `github.com/YourUsername/Challenge-Repo-`).

#### Cloning Your Fork (Bring Your Copy Local!) 📥
**What:** Download *your own forked repo* from GitHub onto your computer.
**How:** 
1.  Go to *your personal fork* of the challenge repo on GitHub.
2.  Click the green **`< > Code`** button.
3.  Make sure "HTTPS" is selected, and click the copy icon next to the URL.
4.  In your PowerShell (or preferred terminal), navigate to where you want to store your projects (e.g., `cd C:\Users\YourUser\Documents\GitHub`).
5.  Run the `git clone` command, pasting the URL you copied:
   ```bash
   git clone [paste your forked repo's HTTPS URL here]
   # Example: git clone [https://github.com/YourUsername/Challenge-Repo-.git]
   ```

---

## Verification Checkpoint ✅

Quick check in PowerShell to confirm everything's humming:

* `code --version`
* `git --version`
* `aws --version`
* `terraform --version`

![Versions](https://github.com/user-attachments/assets/0ac9e0b7-e769-46c7-866c-5ca117f746c5)

---

## Troubleshooting `PATH` Errors (The Common Culprit! 😤)

#### 1. "Command Not Found" (PATH Errors 🚧) 
If you see an error like `'aws' is not recognized...` or `'git' is not recognized...`, it means your system can't find the executable. Don't fret! It's almost always a **`PATH` environment variable** issue.

**Quick Fixes:**
1.  **Restart PowerShell/Terminal:** Sometimes, new `PATH` changes just need a refresh.
2.  **Verify PATH:** Ensure the folder containing `git.exe`, `aws.exe`, and `terraform.exe` is correctly added to your system's `PATH` environment variable. (A quick Google for "add to system path Windows" helps here!)
3.  **Reinstall:** If all else fails, a fresh reinstall of the tool often resolves the `PATH` configuration automatically.

#### 2. "fatal: not a git repository" (The Classic! 😂)
Ah, the infamous one! This means you're not in the correct directory where your Git repository lives. You probably ran a Git command *outside* the folder you just cloned.

**How to Fix:**
1.  **Your Current Location?** First, run `pwd` (or `cd` by itself) to see which folder you're currently in.
2.  **What's Here?** Next, use `ls` (or `dir`) to list the contents of your current folder and look for your cloned repo folder (e.g., `30-Day-Terraform-challenge-`).
3.  **Navigate!** Once you find it, use `cd` to enter that folder: `cd 30-Day-Terraform-challenge-` (Remember `Tab` for autocompletion!).
4.  **Verify:** Now, `git status` should work perfectly! You should see something like "On branch main" instead of the fatal error.

![Git Clone](https://github.com/user-attachments/assets/68185879-0238-4cda-b191-046862844890)

---

## What's Next? ➡️

Setup complete! Time to start crafting some **TerraBitez!** My first challenge awaits!
