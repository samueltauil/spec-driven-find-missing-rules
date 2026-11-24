# Exercise outline: Find the Missing Rules Before You Build

## Logistics

- **Exercise title:** Find the Missing Rules Before You Build
- **Repository name candidates:** `spec-driven-find-missing-rules`, `spec-driven-retro-spec`, `find-missing-rules`
- **Recommended repository name:** `spec-driven-find-missing-rules` — keeps the series prefix and says what the
  learner practices.
- **Learner copy name:** `skills-spec-driven-find-missing-rules`
- **Experience level:** Beginner
- **Target owner:** samueltauil (assumed; confirm at publish)
- **Copyright holder:** acworkma
- **Series:** Spec-Driven Delivery workshop, exercise 2 of 4. Previous: Trace the Loop: From Intent to Evidence.
  Next: Deliver an Approved Behavior with Copilot.
- **Environment:** GitHub Codespaces (Node.js 22 and the OpenSpec CLI preinstalled), Copilot Chat
- **exercise-toolkit version:** v0.9.3

## Learner

- **Persona:** The mixed-role delivery team member from exercise 1 (product owner, analyst, tester, developer or
  architect) at Contoso Health Plan.
- **Can already:** Branch, commit, push and open a pull request; read an OpenSpec requirement and scenario and
  trace it to evidence (exercise 1).
- **New to:** Writing requirements and exception scenarios themselves; using clarifying questions to find missing
  rules before build.
- **Likely misconceptions:** "A user story with acceptance criteria is a spec." "Missing rules are found in
  testing." "If Copilot drafts the requirements, they are right."
- **Motivation:** Late surprises (UAT and production defects) cost their team rework every release.
- **Constraints:** About 45 minutes; no coding.
- **Access needs to design for:** Keyboard-only use, screen readers, non-native English readers.

## Objective and evidence

**Exercise objective:** Turn a real-looking epic into a validated OpenSpec change by asking clarifying questions,
writing testable requirements with exception scenarios, and measuring which late-found gaps the spec catches.

| Step | Objective (observable) | Activity that performs it | Evidence afterwards | Automated check (what it proves) | Not proven by the check | Feedback if it fails |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Generate clarifying questions about an epic before seeing answers | Read the epic; write at least four questions; compare with Copilot's | `retro/questions.md` on `vision-retro` | At least 5 numbered questions ending in `?` | Question quality | Add numbered lines that end with a question mark |
| 2 | Write a valid OpenSpec change from the epic and the clarified answers | Draft the proposal; draft requirements with Copilot; review and validate | `openspec/changes/add-vision-rider/**` | Proposal has Why and What Changes; at least 3 requirements; strict validation passes | That every requirement is faithful to the answers | Run the validator; read its errors; add MUST and a scenario |
| 3 | Compare the spec with the late-found gaps and close one | Fill the gap comparison; add a requirement for a missed gap; open a pull request | `retro/gap-comparison.md`; pull request | All 8 gaps have a "Caught by" value; the named added requirement exists in the delta; validation passes | That the added requirement closes the gap well | Write "Missed" if not caught; copy the requirement name exactly |

## Story

In 2025, Contoso Health Plan's product configuration team built a vision rider from a five-story epic. Eight
rules surfaced late, most of them in user acceptance testing or production, costing weeks of rework
(illustrative). Your team is starting a similar rider next quarter. Before it does, you replay the 2025 epic: would
spec-driven questions and exception scenarios have caught the missing rules before build?

## README

- **One-line description:** Replay a real-looking epic, ask the questions it never answered, and catch missing
  rules before anyone builds.
- **Who is this for:** Product owners, analysts, testers, developers and architects who finished Trace the Loop
  or can read an OpenSpec spec.
- **What you'll learn:** How clarifying questions and exception scenarios turn an epic into testable requirements.
- **What you'll build:** A validated OpenSpec change and a gap comparison, in a pull request.
- **Prerequisites:** Exercise 1 (recommended); GitHub Codespaces; Copilot Chat (Copilot Free is enough).
- **How long:** Less than 50 minutes.
- **In this exercise, you will:** (1) question an epic before seeing answers, (2) write a validated OpenSpec
  change with exception scenarios, (3) measure your spec against the gaps found late and close one.

## Support curve and learning moves

| Step | Support level | Retrieval or generation moment | Prediction or reflection prompt |
| --- | --- | --- | --- |
| 1 | Guided: five question lenses, one example question | Generate at least four questions before Copilot | "Which story would fail first in production?" |
| 2 | Worked example then completion: one full requirement given; learner and Copilot write the rest | Recall from exercise 1: what makes a scenario checkable | Review checklist on Copilot's draft |
| 3 | Independent: learner judges coverage and writes a requirement alone | Compare own questions to the gap log | "Which move would have caught the most?" |

## Steps

### Step 1 - Question the epic

- **Question this step answers:** What does the epic leave unsaid?
- **Estimated learner time:** 12 minutes (including codespace start).

**📖 Theory:** A user story names who wants what and why; it rarely states the rules. Missing rules hide in five
places: who decides, when (dates, lead times, waiting periods), who else is affected (dependents, partners), what
proves readiness, and what stops or undoes the change. Questions asked before build are the cheapest place to find
them.

**⌨️ Activity 1:** Open the codespace; create the `vision-retro` branch.

**⌨️ Activity 2:** Read the epic; write at least four questions using the lenses; ask Copilot (read-only) for more
and keep the good ones; commit and push.

**Transition**

- **Actions trigger:** `push` to `vision-retro` with `paths: retro/questions.md`.
- **Copy-time safety:** `vision-retro` does not exist in the template.
- **Grading checks:** at least 5 numbered lines ending in `?` in `retro/questions.md`.
- **Failure feedback:** row "Your question list has at least five questions"; tips: one question per numbered line
  ending with `?`.
- **Learner artifact:** `retro/questions.md`.

### Step 2 - Turn answers into testable requirements

- **Question this step answers:** How do answers become rules a team can check?
- **Estimated learner time:** 18 minutes.

**📖 Theory:** An OpenSpec change has a proposal (why and what changes) and a spec delta. Under
`## ADDED Requirements`, each `### Requirement:` states one rule with MUST or SHALL, and each has at least one
`#### Scenario:` with GIVEN, WHEN and THEN lines. Exception scenarios (what happens when things go wrong) catch the
costliest gaps. `openspec validate --strict` checks the format, not the truth: people still check every rule.

**⌨️ Activity 1:** Read the product owner's seven answers (revealed in this step); write the proposal.

**⌨️ Activity 2:** Paste the worked requirement; ask Copilot to draft the rest from the answers; review against a
checklist; validate; commit and push.

**Transition**

- **Actions trigger:** `push` to `vision-retro` with `paths: openspec/changes/**`.
- **Copy-time safety:** branch filter.
- **Grading checks:** proposal has `## Why` and `## What Changes`; at least 3 `### Requirement:`; strict
  validation of `add-vision-rider` passes.
- **Failure feedback:** rows per check; tips: run the validator in the terminal and fix the first error; check
  the folder names.
- **Learner artifact:** the OpenSpec change.

### Step 3 - Measure your spec against the gap log

- **Question this step answers:** Would this spec have caught the 2025 gaps?
- **Estimated learner time:** 15 minutes.

**📖 Theory:** A retro-spec compares what a spec would have caught with what actually surfaced late. Four moves
catch most gaps: Clarify (ask), Make it testable (exception scenarios), Quality checklist (review the spec for
missing roles and data), and Plan (find dependencies early). The costs here are illustrative, not measured.

**⌨️ Activity 1:** Create `retro/gap-comparison.md` from the given table; fill "Caught by" with a requirement name,
a question number, or `Missed`.

**⌨️ Activity 2:** Add one requirement (with a scenario) for a gap you missed; record it; validate; push; open a
pull request.

**Transition**

- **Actions trigger:** `pull_request` to `main`, types `opened`, `synchronize`, `reopened`.
- **Copy-time safety:** not a push event.
- **Grading checks:** 8 gap rows with a non-empty "Caught by"; the requirement named under "Added after the
  retro" exists in the delta; strict validation passes.
- **Failure feedback:** rows per check; tips: write `Missed`; copy the requirement name exactly.
- **Learner artifact:** pull request.

## Review

- **Recap:** You questioned an epic, wrote testable requirements with exception scenarios, and measured coverage.
- **Recall questions:** Which question lens finds the most expensive gaps? Why does strict validation not prove a
  requirement is right?
- **Transfer prompt:** Take an epic in your backlog; write five lens questions before refinement.
- **What's next:** Exercise 3, Deliver an Approved Behavior with Copilot.

## File map

| File | Purpose |
| --- | --- |
| `.github/exercise-outline.md` | This outline |
| `README.md`, `LICENSE` | Landing page; MIT |
| `.github/steps/1-step.md` … `3-step.md`, `x-review.md` | Content |
| `.github/workflows/0-start-exercise.yml`, `1-step.yml`, `2-step.yml`, `3-step.yml` | Automation |
| `.github/copilot-instructions.md` | Spec-driven rules for Copilot |
| `.devcontainer/devcontainer.json` | Node.js 22, `npm ci`, Copilot Chat |
| `retro/original-epic.md` | The 2025 epic, unchanged |
| `retro/questions.md` | Learner question list (one example) |
| `openspec/specs/member-eligibility/spec.md` | Format example of a living spec |
| `package.json`, `package-lock.json` | Pinned OpenSpec CLI |

## Test plan

- **Walkthrough personas:** product owner with no terminal experience; developer skimmer.
- **Negative tests:** 4 questions only; requirement without MUST; requirement without scenario; change folder
  misnamed; gap row with empty "Caught by"; added requirement name not in the spec.
- **Environments to test:** personal account, Codespaces, Copilot Free.

## Risks and open questions

- Copilot may invent rules beyond the answers; the review checklist and theory address this.
- Learners may name the folder differently; feedback names the exact path.

## Future considerations

- A team variant where pairs compare question lists before the reveal.
