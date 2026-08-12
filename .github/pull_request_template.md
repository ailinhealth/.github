<!--
  Title format: [AIL-123] Short description in the imperative
  This PR is the change record. Write it for someone reading it in two years
  who wasn't here. Delete nothing — write "None" or "N/A — reason" instead.
-->

## Summary

**Jira:** AIL-
**Type:** feature / fix / hotfix / chore / refactor

<!-- Two or three sentences: what changes and why. Not a commit log. -->

---

## Traceability

**Implements / affects:**
<!-- Requirement, user need, or risk control from the risk file. Give the ID if there is one. -->

**Design documentation:**
<!-- Path to the in-repo design doc updated in this PR, or "No design change — <why>". -->

**Touches a class C software item:** yes / no / pending item-level classification

---

## Verification

### Automated

- [ ] Unit tests added or updated for the changed units
- [ ] Full suite green in CI
- [ ] Production build succeeds on Linux

**What the new or changed tests cover:**
<!-- One or two lines. "Added tests" is not an answer. -->

### System testing

Pick one.

**Verified on `pre`:**

- Manifest comment: <!-- link to the deploy:pre bot comment on this PR -->
- Verified by: @
- Date:
- **What was exercised:**
  <!-- The actual scenarios walked through. This is the §5.7 record and the part
       an auditor will read first. Be specific: which flows, which roles, which data. -->

**Not deployed to `pre`, because:**
<!-- Justification. Valid: no runtime behaviour change, no external service involved,
     fully covered by the automated suite. Not valid: "small change", "in a hurry". -->

### Known anomalies at merge

<!-- Anything not working, working partially, or working differently than specified —
     including things you have decided not to fix now. Write "None" if there are none.
     Blank is not an acceptable answer. -->

---

## Data, configuration and rollback

**Migration:** none / expand phase / contract phase
<!-- If expand or contract, name the release the paired change ships in. -->

**Configuration changes:** <!-- env vars, secrets, .ebextensions, EB platform, IaC. "None" if none. -->

**Feature flag:** `flagID` / none

**Rollback plan:**
<!-- Default is: redeploy the previous build, then open a revert PR.
     If that is NOT sufficient — because of a migration or a config change — say what is. -->

---

## Review
<!-- Fill the mention if needed, leave 'not needed' if not -->

- [ ] Copilot review addressed
- [ ] Design review — @ / not required
- [ ] Clinical or product review — @ / not required
- [ ] Release-note label applied

<!--
  REVIEWERS: do not edit the section above — it belongs to the author.
  Paste the checklist below into your review comment. Your GitHub approval is the
  mp.sw.2 acceptance signature: attributed, timestamped, and not editable afterwards.
  The PR body is the evidence; your review is the signature.

  ### Reviewer checklist
  - [ ] I am not the author of this change
  - [ ] The change does what the summary says, and nothing else
  - [ ] Design documentation matches the code as merged
  - [ ] Test coverage is proportionate to the risk of the change
  - [ ] The verification record above is specific enough to stand on its own
  - [ ] Known anomalies are stated and acceptable
  - [ ] Rollback is possible as described
  - [ ] If something merged ahead of this PR: re-verification rule considered
        (re-verify on `pre` if the changes touch the same files, or the same clinical function or data path)

  Approving means: this change is accepted for release.
-->
