# Original epic: Offer a vision rider to employer groups

> Copied from the work tracker as written in 2025, before build started. Kept unchanged, gaps and all. Fictional.

**Epic**: EP-2025-0412  |  **State**: Closed (delivered 2025)  |  **Owner**: Product owner, Product Configuration  |  **Target**: live for July 1 effective dates

## Description

Employer groups keep asking for vision coverage they can add to their medical plan, and sales wants a vision rider in market for July 1. Fabrikam Vision Services will administer the benefit: eye exams, lenses, frames and contact lenses. We need to set up the rider so account managers can sell it, eligibility goes to Fabrikam and claims pay correctly. It should work like our dental rider setup.

**Done when**: UAT is signed off and the first groups are live.

## User stories

### Story 1: Request the vision rider

As an account manager, I want to request the vision rider for my group so that the group can offer vision coverage.

- Account manager fills in the rider request form.
- The form includes group name, plan and effective date.
- The form is emailed to Product Configuration.

### Story 2: Configure vision benefits

As a configuration analyst, I want to set up the vision benefits so that claims pay correctly.

- Copays and allowances match the benefit grid.
- Configuration is reviewed.

### Story 3: Send eligibility to Fabrikam

As an eligibility analyst, I want to add rider members to the eligibility file so that Fabrikam Vision Services knows who is covered.

- Employees with the rider are on the file.
- The file goes to Fabrikam weekly.

### Story 4: Test vision claims

As a tester, I want to test vision claims so that we know the benefits pay.

- Exam, lens and frame claims pay per the benefit grid.
- Defects are logged and fixed before go-live.

### Story 5: Go live

As a product owner, I want to turn on the rider for each group so that members can use their vision benefits.

- The rider is active on the group's effective date.
- The account manager is notified.
