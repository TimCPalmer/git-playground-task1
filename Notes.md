I renamed the store variable to v_store

I change console message on line 22 of notes.js to YOU GOT NO NOTES YET



What claude told me changes : - it found the stray change

What changed
1. notes.js (the two edits you asked me for):
   - The store variable is now v_store, on line 2 and at its three uses on lines 15, 20 and 32.
   - The message for an empty list is now "YOU GOT NOT NOTES YET".
2. scripts/check.js: someone replaced a blank line with bawbag random edit on line 7. I didn't make this change.
3. Notes.md: this is a new, untracked file of 114 bytes.

Looks unintended
- scripts/check.js:7 will break CI. bawbag random edit isn't valid JavaScript, so node scripts/check.js crashes with a syntax error before it checks anything. Every pull request would fail the "Submission check" workflow. To undo it: git restore scripts/check.js.
- Notes.md has the wrong capitalisation. check.js looks for lowercase notes.md. Windows ignores case in file names, so it will pass on your machine, but CI runs on Ubuntu, where the check would fail with "notes.md is missing". To rename it: git mv -f Notes.md notes.md, or rename it and then git add notes.md. It also isn't staged yet.
- The new message probably has a typo. "YOU GOT NOT NOTES YET" was probably meant to be "NO NOTES". The change also dropped the old hint "Add one with: notes add <text>".

Fine as-is
- The rename to v_store is complete. No other files use that variable, and lib/store.js is unchanged.
- Git warns that line endings in notes.js will be converted from LF to CRLF on Windows. That warning is harmless.
