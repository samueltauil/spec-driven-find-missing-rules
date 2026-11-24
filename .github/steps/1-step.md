## Step 1: Question the epic

<img width="800" alt="Exercise banner: Find the Missing Rules Before You Build, exercise 2 of 4 of the Spec-Driven Delivery workshop. Question a thin epic, then write the missing rules as a valid OpenSpec change" src="../images/banner.png">

Welcome to the Contoso Health Plan delivery team, @{{ login }}! :wave: In 2025, the team built a vision rider for employer groups from a five-story epic. Eight rules surfaced late, most of them in acceptance testing or after go-live. Your team starts a similar rider next quarter, so first you'll replay the 2025 epic: which questions would have found the missing rules before anyone built anything?

### 📖 Theory: Where missing rules hide

A user story names who wants what and why, but it rarely states the **rules**: the decisions a system and its people must follow, such as who approves, by when, and what happens when something goes wrong. Missing rules hide in five places, so read every story through five lenses. A question asked before build is the cheapest way to find a rule. The same rule found in acceptance testing or after go-live costs rework, and sometimes member calls.

<img width="800" alt="Five lenses for missing rules. Who decides: who reviews, who approves, and who can grant an exception. When: dates, lead times, waiting periods and deadlines. Who else is affected: family members, partners, other teams and other systems. What proves it is ready: tests, sign-offs and acceptance by a partner. What stops or undoes it: cancellations, terminations and reversals" src="../images/question-lenses.png">

### ⌨️ Activity 1: Open your codespace

Your copy of this repository comes with a ready-made [codespace](https://docs.github.com/en/codespaces/overview): an online editor with Node.js and the OpenSpec command-line tool already installed.

1. Right-click the button below and open it in a new tab, so you can keep these instructions open.

   [![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/{{ full_repo_name }}?quickstart=1)

1. On the codespace page, check that the repository is `{{ full_repo_name }}`, your copy, and not the original exercise. Then create the codespace.

1. Wait for the editor to open. The first start takes about 2 to 4 minutes. You are ready when the bottom-left of the Status Bar shows **Codespaces** followed by the codespace name, and the epic, `retro/original-epic.md`, is open.

   <img width="400" alt="Bottom-left corner of the editor: the Status Bar shows Codespaces followed by the codespace name, here expert couscous" src="../images/codespaces-status.png">

1. In the terminal, create a branch for your work.

   > ![Terminal command](https://img.shields.io/badge/Terminal-text?style=flat&logo=gnometerminal&labelColor=1f2328&color=eee)
   >
   > ```bash
   > git switch -c vision-retro
   > ```

<details>
<summary>Having trouble? 🤷</summary><br/>

- **No terminal is visible:** Open one from the editor menu with **Terminal** > **New Terminal**, or press `` Ctrl+` `` (`` ⌃` `` on Mac). The terminal is the **TERMINAL** tab of the panel at the bottom of the editor.

  <img width="460" alt="Panel tabs at the bottom of the editor: PROBLEMS, OUTPUT, DEBUG CONSOLE, TERMINAL and PORTS, with TERMINAL selected" src="../images/terminal-tab.png">

- **The codespace opened the original exercise:** Close that tab and use the button above, which points to your copy. You can also start one from your repository page: **Code** > **Codespaces** > **Create codespace on main**.

- **`npm ci` failed during setup:** Run `npm ci` yourself in the terminal. You need it in step 2.

- **Copilot Chat asks you to sign in:** Select the Copilot icon in the Status Bar, then sign in with your GitHub account.

</details>

### ⌨️ Activity 2: Question the epic

1. Read `retro/original-epic.md`: the description and its five user stories. To reopen it, press `Ctrl+P` (`Cmd+P` on Mac) and type `original-epic`.

1. Before you write anything, predict: which story would fail first in production? Note your guess. You'll check it in step 3.

1. Open `retro/questions.md`. Question 1 is an example through the **Who decides?** lens. Below it, write at least four questions of your own, numbered 2, 3, 4 and so on. Put each question on its own line and end it with `?`. Try a different lens for each one.

   > 💡 **Tip:** Ask for a rule, not a solution. "What happens if a group leaves before go-live?" finds a rule. "Should we build a cancel button?" picks a design.

1. Open Copilot Chat: select the chat icon at the top of the window, or press `Ctrl+Alt+I` (`⌃⌘I` on Mac). If the chat box shows a mode picker, choose **Ask**, so Copilot answers without editing files.

1. Ask Copilot for the questions you haven't thought of yet. The first sentence keeps it read-only.

   > ![Copilot prompt](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > Do not edit any files. Read retro/original-epic.md and retro/questions.md.
   > List up to 10 questions the product owner should answer before anyone builds
   > this rider. Use five lenses: who decides, when, who else is affected, what
   > proves it is ready, and what stops or undoes it. Skip questions already in
   > retro/questions.md. Only ask questions; do not answer them or propose a design.
   > ```

   > 💡 **Tip:** If Copilot answers without reading the files, add them to the chat: type `#` in the chat box and pick each file.

1. Compare Copilot's list with yours. Keep only the good ones: questions that ask for a rule the product owner could answer and that are not already on your list. Add them below your own questions, numbered in order.

1. Save the file, then commit and push your branch.

   > ![Terminal command](https://img.shields.io/badge/Terminal-text?style=flat&logo=gnometerminal&labelColor=1f2328&color=eee)
   >
   > ```bash
   > git add retro/questions.md
   > git commit -m "Ask what the vision rider epic leaves unsaid"
   > git push -u origin vision-retro
   > ```

1. Go back to this issue in your browser. Wait a moment for Mona to check your work, provide feedback, and share the next lesson.

<details>
<summary>Having trouble? 🤷</summary><br/>

- **Copilot answered the questions or drafted requirements:** Ignore the answers. Only the product owner can answer, and you'll get those answers in step 2. Ask again and repeat the last sentence of the prompt.

- **Copilot edited a file:** Check `retro/questions.md` and remove anything you didn't choose to keep. Then choose **Ask** in the chat and ask again.

- **Mona says there are fewer than five questions:** Mona counts numbered lines that end with `?`, such as `2. Who can approve a shorter lead time?`. The example question counts. Start each question on its own line with a number and a period.

- **Mona did not respond:** Check that you pushed to the `vision-retro` branch and that `retro/questions.md` changed. You can watch the run in the [Actions tab](https://github.com/{{ full_repo_name }}/actions).

</details>
