# Response Letter Requirements

These instructions apply to every file under `response/`.

## Reviewer comments: verbatim source text

- Treat `response/[SPAM] TACO-2026-55_ Decision.eml` as the single authoritative source for all Associate Editor and reviewer comments.
- Every `Reviewer comment` block in `response/response.tex` must reproduce the corresponding text from the decision email verbatim.
- Do not paraphrase, shorten, combine, silently correct, or otherwise edit the reviewer's wording, spelling, capitalization, punctuation, or terminology.
- LaTeX-only escaping is allowed when required for compilation, for example `\%`, `\&`, `\_`, `$\times$`, and `---`. Such escaping must not change the visible text in the compiled PDF.
- If a response draft contains a shortened or paraphrased `Comment`, do not copy that version into the final response letter. Locate and copy the complete original passage from the decision email.
- After adding or editing a question, compare the rendered reviewer comment against the decoded plain-text content of the decision email before considering the change complete.

## Paper cross-reference verification after every edit

- After every modification to `response/response.tex`, comprehensively verify every cited section, figure, table, equation, appendix, and reference against the current paper under `TACO_2026_FlusArch/`.
- Do not assume numbering recorded in an older Markdown response draft is still current.
- Check both explicit numeric references such as `Fig. 13`, `Table 4`, and `Section 6.5`, and descriptive references such as ``the load-balance table'' or ``the hierarchical-scalability figure.''
- Confirm that each response claim points to the paper location that actually contains the stated revision, data, or wording.
- Confirm that figure subpanels, table captions, section titles, and ranges such as `Fig. 13(c,d)` match the current compiled paper.
- Prefer stable LaTeX labels from the paper when the response build can resolve them reliably. If the response is compiled as a standalone document and cannot import the paper's labels, use the currently verified visible number and recheck it after subsequent paper edits.
- Search the entire response for `Fig.`, `Figure`, `Table`, `Section`, `Eq.`, `Appendix`, and LaTeX `\ref`/`\autoref` uses as part of every verification pass.
- Compile `response/response.tex` after editing and resolve undefined references, stale numbers, and compilation errors before reporting completion.
- Report explicitly which paper source/version was checked and identify any reference that could not be verified. Never present an unverified reference as confirmed.

## Required completion check

A response edit is complete only when all three conditions hold:

1. Reviewer comments visibly match the decision email verbatim.
2. All manuscript cross-references have been checked against the current paper.
3. `response/response.tex` compiles successfully and the rendered PDF has been inspected for comment colors and reference presentation.
