# Protocol: Multi-Issue PR Scope & Comments

## Applies When
A branch/PR accumulates multiple tracked issues before merging to `main` (a rolling
milestone or epic branch) instead of one issue per PR.

## Scope Integrity (STRICT)
- The PR body's issue checklist reflects only `base...head` — never the full
  epic/milestone list.
- Before writing or editing the PR body, confirm scope with
  `git log --oneline <base>..<head>` (or `git diff <base>...<head> --stat`).
- An issue already merged into `base` via a prior PR is **not** in scope here — cite it
  under References (`Base: #<PR> — #X, #Y merged, not part of this diff`), never as a
  checklist item. Being listed in the same epic/milestone is not the same as being in
  this diff.
- Re-check scope every time a new issue lands on the branch — don't reuse a stale
  checklist from an earlier state of the PR.

## PR Body Template
```
## Scope
<one line, link the epic/milestone if any>

- [ ] #<issue> — <title>   (one row per issue actually in this diff)

<draft-until note, or omit once ready for review>

## References
- <architecture doc, if relevant>
- Epic: #<epic issue>
- Base: #<prior PR>   (only if this branch continues a prior merged PR)
```

## Per-Issue PR Comments
- When an issue's implementation is committed to the branch, post one PR comment
  summarizing that issue alone — not the whole branch. This lets reviewers read a
  multi-issue PR one issue at a time.
- Structure: `## ✅ #<issue> — <title>`, commit ref(s), what landed, any decisions worth
  flagging for review, verification evidence, the issue's own acceptance criteria as a
  checklist.
- Draft the comment to a scratch file first, then post with
  `gh pr comment <PR> --body-file <file>` — PR comments are outward-facing and
  effectively permanent, so review the draft before posting.
