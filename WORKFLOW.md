# Workflow: Vague vs Precise Prompting

## The Feature
A settings form with username, email, and password fields, built twice using two different prompting approaches.

## Round 1: Vague Prompt
**Prompt used:** "banao ek settings form" (build a settings form — no other detail given)

**What came out:**
A minimal form with three text inputs and a save button. The password field used `type="text"` instead of `type="password"`, exposing the input in plain view. Validation only checked whether the username was empty — email and password had no checks at all. Errors were shown through a plain `alert()` popup instead of inline feedback. The form had no `preventDefault()`, so submitting it reloaded the page and lost all entered data. There were no `label for` attributes, so screen readers would not correctly associate labels with inputs.

## Round 2: Precise Prompt
**Prompt used:** A detailed prompt specifying exact validation rules (username ≥ 3 characters, valid email format via regex, password ≥ 8 characters with at least one number), a requirement for real-time inline error messages instead of alerts, accessible `label for` attributes, and a requirement that the form must not reload the page on submit. The prompt also asked for the code to be written and then manually verified against those rules.

**What came out:**
A form with real-time validation on each field as the user types, inline error messages tied to inputs via `aria-describedby`, a proper `password` input type, `preventDefault()` on submit, and a success message shown only when all fields pass validation. The structure was cleaner and closer to something usable in a real project.

## Correctness
Round 1 technically "worked" in the sense that clicking Save didn't crash anything, but it accepted invalid emails, weak passwords, and reloaded the page on submit — a real user could break it in seconds. Round 2 correctly rejected invalid input in each field and gave the user immediate, specific feedback without losing form state.

## Edge Cases
Round 1 missed almost every edge case: no email format check, no password strength check, and no handling of whitespace-only input in the username field. Round 2 still had a minor gap I caught on review — it does not trim the password field before checking length, so a password entirely made of leading/trailing spaces could technically pass the number check if a digit was embedded. I noted this rather than silently accepting it, since the exercise brief asks to name at least one AI mistake caught during review.

## Review Effort
Round 1 took very little time to generate but a lot longer to actually trust — every field needed to be re-checked manually, and the security issue with the password field type would have gone unnoticed without a close read. Round 2 took longer to prompt (I had to think through the exact rules up front) but needed far less fixing afterward. Overall, Round 2 was slower to start but faster end-to-end once review and fixing time is included in Round 1.

## Takeaway
A vague prompt shifts the verification burden entirely onto the reviewer, and it's easy to miss subtle issues like an insecure input type when nothing in the code visibly looks "broken." A precise prompt with explicit constraints and a verification step produces code that still needs review, but the review is faster and catches smaller things because the reviewer isn't also re-deriving what the requirements should have been in the first place.