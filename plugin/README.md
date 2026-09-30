# Receipts: prove the fix

A green test suite says the tests pass. It does not say they would have caught the bug.

This plugin gives Claude the `prove-fix` skill. After Claude fixes a bug or refactors code, it runs every test it added or edited twice: once with the change, and once with the changed source files reverted to the base branch. A test for a fix must fail on the old code and pass on the new one. If it passes both ways, it proves nothing, and Claude rewrites it around the input that was actually broken before it says the work is done.

![A test for 1900 passes with the fix and fails without it: PROVEN. A test for 2020 passes both times: THEATER.](https://raw.githubusercontent.com/syntaxixr/receipts/main/docs/media/how-it-works.gif)

## Verdicts

- **PROVEN**: fails without the change, passes with it. The test catches the bug.
- **GUARD**: passes both ways, next to a proving test. It guards the neighboring behavior.
- **THEATER**: passes both ways and no test proves the change.
- **WEAK**: fails on the old code only because a name it imports did not exist yet.
- **BROKEN** and **FLAKY**: fails with the change, or gives different results on the same code.
- **PRESERVED** and **CHANGED**: for a refactor, tests must pass on both sides.

## Use

Claude runs the skill on its own after a fix. You can also call it with `/receipts-check:prove-fix`.

It works in any git repository with pytest, vitest or jest. It needs Node.js 20 or newer and git. There are no other dependencies, no network calls and no LLM in the check: the verdict is a run of your own tests. The red run edits files in place and restores every byte afterwards.

An optional Stop hook blocks Claude from ending a turn while its changed tests prove nothing. It is off by default, because it runs the repository's tests. Turn it on for a repository you trust with `git config receipts.hook true`.

## More

The GitHub Action, the command line tool and a study of 181 real changes are in the main repository: https://github.com/syntaxixr/receipts

MIT license.
