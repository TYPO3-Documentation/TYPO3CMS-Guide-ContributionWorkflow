# AGENTS.md — Contribution Guide: Core Development

## Repo structure

```
Documentation/                   # the actual manual (reST source, published to docs.typo3.org)
CONTRIBUTING.md                  # how to contribute
```

## Commands

- `make docs` — render the manual locally with Docker
- `make test-docs` — render in minimal-test mode (the same validation CI runs); use this to validate any change before committing
- `pre-commit run --all-files` — apply the whitespace hooks
  (`trailing-whitespace`, `end-of-file-fixer`) configured in
  `.pre-commit-config.yaml`; `pre-commit install` wires them into `git commit`

## Scope

This manual documents the *process* of contributing to the TYPO3 Core:
accounts, Gerrit and the review workflow, coding guidelines, bug fixing,
testing, and the responsibilities of Core mergers. It is about how people
work together, not about the TYPO3 API.

Two consequences follow:

- The facts to verify are the **process and the tooling** — Gerrit, Forger,
  forge.typo3.org, the relevant GitHub repositories — not PHP signatures.
  These change independently of TYPO3 releases, so check the real service
  before describing a workflow.
- **Do not confuse the two contribution workflows.** Changes to the TYPO3
  Core itself go through Gerrit; changes to the documentation go through
  GitHub pull requests. This manual describes the former but is itself
  edited through the latter.

## Documentation writing rules

Follow the official TYPO3 documentation writing conventions (see
https://github.com/TYPO3-Documentation/TYPO3CMS-Guide-HowToDocument):

1. **reST, not Markdown** — everything under `Documentation/` is reStructuredText.
2. **Sentence case headlines** — first word and proper nouns only:
   https://docs.typo3.org/permalink/h2document:content-styleguide-title-capitalization
3. **4-space indentation** for directive bodies, 2 spaces after `..` markers:
   https://docs.typo3.org/permalink/h2document:cgl-indenting
4. **Single backticks over double**, unless the content needs a literal
   backtick: https://docs.typo3.org/permalink/h2document:inline-code
5. **Every headline needs a `..  _anchor:` target** directly above it
   (https://docs.typo3.org/permalink/h2document:link-anchor), and anchors are
   never removed once published
   (https://docs.typo3.org/permalink/h2document:anchor-persistence).
6. **Validate before committing** — run `make test-docs`, and run the
   pre-commit hooks (see Commands).
7. **Never commit or push without being asked.**

## Commit message format

Follow https://docs.typo3.org/m/typo3/docs-how-to-document/main/en-us/Howto/EditLocal.html:

- Prefix the subject line with `[TASK]`, `[BUGFIX]`, or `[FEATURE]`,
  followed by a short, imperative summary.
- Explain *why* the change is needed in the body — the diff already shows
  what changed.
- End with a `Signed-off-by: Your Name <email>` trailer.
- If AI assistance went beyond basic spelling/grammar checks, add an
  `Assisted-by: <tool/model name> <contact>` trailer, e.g.
  `Assisted-by: Claude Sonnet 5 <noreply@anthropic.com>`.
- **No `Releases:` trailer.** This manual is unversioned: it has only a
  `main` branch and no LTS branches, so the backporting conventions and
  `backport <version>` labels described in the how-to-document guide do
  not apply here.

## Pull requests

- When a commit is the only commit in the PR, the PR title and body must
  match the commit's subject and body exactly.

## References

- [TYPO3CMS-Guide-HowToDocument](https://github.com/TYPO3-Documentation/TYPO3CMS-Guide-HowToDocument) — official writing style guide and reST reference
- https://docs.typo3.org/m/typo3/docs-how-to-document/main/en-us/Howto/EditLocal.html — commit/PR conventions
