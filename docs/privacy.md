# Privacy

Receipts collects nothing.

- **No data leaves your machine.** The plugin, the skill and the command line tool run your project's own tests locally. There are no network calls, no analytics and no telemetry, and no LLM is involved in the check.
- **No accounts and no keys.** Receipts does not ask for credentials and does not store any.
- **Files stay where they are.** The red run edits files in your working tree and restores every byte afterwards. A backup journal in `.git/receipts-backup` holds the originals during a run and is removed once they are restored.
- **The GitHub Action** runs inside your own GitHub Actions workflow. It posts one comment on the pull request with the workflow's own token, updates that same comment on later runs, and sends nothing anywhere else. Secrets in test output are redacted before the comment is posted.

Questions: open an issue at https://github.com/syntaxixr/receipts/issues
