## Step 2: Turn answers into testable requirements

Good questions, @{{ login }}! The product owner sat down with your team and answered seven of them. In 2025, the team learned each of these answers only during build, in acceptance testing or after go-live. Now turn them into rules a team can check before anyone builds. Copilot drafts; you decide what stays.

### 📖 Theory: Testable requirements and exception scenarios

An [OpenSpec change](https://github.com/Fission-AI/OpenSpec/blob/main/docs/concepts.md) is a folder under `openspec/changes/` with a **proposal**, `proposal.md`, that says why the change matters and what changes, and a **spec delta**, `specs/<capability>/spec.md`, that holds the rules. Under `## ADDED Requirements`, each `### Requirement:` states one rule with MUST or SHALL, and each has at least one `#### Scenario:` with **GIVEN**, **WHEN** and **THEN** lines. **Exception scenarios** show what happens when something goes wrong, such as a start date that is too close, a partner that says no or a group that leaves, and they catch the costliest gaps. `openspec validate --strict` checks the format, not the truth: people still check every rule against the answers.

<img width="800" alt="Anatomy of a testable requirement. Under ADDED Requirements, the requirement Setup lead time says: A vision rider MUST take effect on the first day of a month at least 30 calendar days after its configuration is approved, unless and so on. Its scenario, Short-notice start needs approval: GIVEN a configuration approved on 2025-06-10, WHEN the group asks to start on 2025-07-01, THEN the setup is held until the product owner and underwriting approve the exception. Callouts: ADDED, MODIFIED or REMOVED says how the change affects the current spec; one rule per requirement, written with MUST or SHALL; at least one scenario, where exception scenarios catch the costly gaps; GIVEN, WHEN, THEN give the context, the event and a result someone can observe. Footer: openspec validate --strict checks the format; people check that each rule is right" src="../images/requirement-anatomy.png">

### ⌨️ Activity 1: Read the answers and write the proposal

1. In your codespace, create `retro/answers.md` and paste the product owner's answers into it. Read them as you go.

   ```markdown
   # Product owner's answers

   1. Who reviews and approves a configuration?
      A second configuration analyst, never the analyst who built it.
   2. Are dependents covered?
      Yes, when the group covers dependents on its medical plan, with the same
      age limit as that plan.
   3. When does a new hire in a waiting period get the rider?
      When their medical coverage starts.
   4. How much lead time does setup need?
      A rider starts on the first day of a month at least 30 calendar days after
      its configuration is approved. A shorter start needs approval from both the
      product owner and underwriting.
   5. What must be true before go-live?
      Fabrikam Vision Services accepts a synthetic test eligibility file, and the
      eight standard test claims pay as expected.
   6. What happens if a group's coverage ends before go-live?
      Cancel the request and tell Fabrikam Vision Services to drop the group.
   7. For a rider that starts mid-year, are allowances and frequency limits prorated?
      No. They start fresh on the rider's effective date.
   ```

1. Compare the answers with your `retro/questions.md`. Which answers did one of your questions ask for, and which would have stayed hidden? Keep that in mind for step 3.

1. Create `openspec/changes/add-vision-rider/proposal.md` with this outline, and replace each comment with your own words.

   ```markdown
   ## Why
   <!-- What went wrong with the 2025 epic, and what this change prevents next time. -->

   ## What Changes
   <!-- One short bullet per rule this change adds. -->
   ```

   > 💡 **Tip:** To create the folder and the file at once, right-click `openspec/changes` in the Explorer, select **New File...**, and type `add-vision-rider/proposal.md`.

1. Save the file. You'll commit it together with your requirements at the end of the next activity.

<details>
<summary>Having trouble? 🤷</summary><br/>

- **Not sure what to write under Why:** One or two sentences are enough: rules surfaced late in 2025 and cost rework, and this change states them before build.

- **None of your questions matched an answer:** That's useful evidence, not a mistake. Note which lens you skipped; step 3 measures what it would have cost.

- **The folder has another name:** The folder must be exactly `openspec/changes/add-vision-rider`, all lowercase with hyphens. Right-click it in the Explorer and select **Rename...**.

</details>

### ⌨️ Activity 2: Draft, review and validate the requirements

1. Before you write a rule, answer from memory: what makes a scenario checkable? Then check yourself.

   <details>
   <summary>Show the answer</summary>

   Concrete values, one event, and a **THEN** result that someone can observe. In exercise 1, a passing scenario proved only what its check asserted, so a vague **THEN** proves nothing.

   </details>

1. Create `openspec/changes/add-vision-rider/specs/vision-rider/spec.md` and paste this worked requirement. It turns answer 4 into a rule and an exception scenario.

   ```markdown
   ## ADDED Requirements

   ### Requirement: Setup lead time
   A vision rider MUST take effect on the first day of a month at least 30 calendar
   days after its configuration is approved, unless the product owner and
   underwriting approve an exception.

   #### Scenario: Short-notice start needs approval
   - **GIVEN** a configuration approved on 2025-06-10
   - **WHEN** the group asks to start on 2025-07-01
   - **THEN** the setup is held until the product owner and underwriting approve the exception
   ```

1. In Copilot Chat, with **Ask** selected as in step 1, ask Copilot to draft the other rules.

   > ![Copilot prompt](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > Do not edit any files. Read retro/answers.md and
   > openspec/changes/add-vision-rider/specs/vision-rider/spec.md.
   > Draft more requirements in the same format as "Setup lead time": one rule per
   > "### Requirement:" with MUST or SHALL, and at least one "#### Scenario:" with
   > GIVEN, WHEN and THEN lines. Add an exception scenario wherever something can
   > go wrong. Say which answer each rule comes from. Use only the answers; do not
   > add rules, numbers or roles that they do not state.
   > Put all the requirements in one markdown code block.
   > ```

1. Review Copilot's draft against this checklist before you keep anything:

   - Each rule traces to an answer: you can name its number.
   - Each rule uses MUST or SHALL.
   - Each requirement has a scenario, and every rule that can go wrong has an exception scenario.
   - Nothing is invented: no rule, number, age or role that the answers don't state.

1. Paste the requirements that pass the checklist below the worked requirement, under the same `## ADDED Requirements` heading. Use the code block's copy button so the `###` and `####` markers come with it. Fix or delete the rest. Keep at least two, so the delta has at least three requirements.

1. Predict whether strict validation will pass on the first try. Then run it.

   > ![Terminal command](https://img.shields.io/badge/Terminal-text?style=flat&logo=gnometerminal&labelColor=1f2328&color=eee)
   >
   > ```bash
   > npx openspec validate add-vision-rider --strict
   > ```

1. Fix every error until the output says `Change 'add-vision-rider' is valid`. Then check that the file has at least three `### Requirement:` headings.

1. Save, then commit `retro/answers.md` and the `openspec/changes` folder with your own message, and push to `vision-retro` as you did in step 1.

1. Go back to this issue in your browser. Wait a moment for Mona to check your work, provide feedback, and share the next lesson.

<details>
<summary>Having trouble? 🤷</summary><br/>

- **`should contain SHALL or MUST`:** Write the keyword in capitals in the rule text, on the lines between the `### Requirement:` heading and its first scenario.

- **`must include at least one scenario`:** Scenario headings need exactly four `#` characters: `#### Scenario:`.

- **`Change must have at least one delta`:** Check the path, `specs/vision-rider/spec.md` inside `openspec/changes/add-vision-rider`, and the heading `## ADDED Requirements`.

- **Mona counts fewer requirements than you pasted:** Copied chat text can lose its `#` characters. Each rule needs its own `### Requirement:` line and each scenario its own `#### Scenario:` line.

- **Copilot added a rule the answers don't state,** such as an age limit or a number of days: Delete it, or write it down as a new question for the product owner. A plausible rule that nobody decided is still a guess.

- **Copilot stops answering or says you've reached a limit:** Write the two requirements yourself. Copy the shape of `Setup lead time` and turn answers 1 and 6 into rules.

- **`git commit` says nothing added to commit:** New files must be added first: `git add retro/answers.md openspec/changes`, then commit and push.

- **`npx` asks to install a package:** Answer `n`, run `npm ci`, then run the command again.

- **Mona did not respond:** Check that you pushed to `vision-retro` and that a file under `openspec/changes` changed. You can watch the run in the [Actions tab](https://github.com/{{ full_repo_name }}/actions).

</details>
