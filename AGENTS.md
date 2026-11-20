# AGENTS.md

Guidance for AI agents working in this repo. Humans: see `README.md`.

## What this is

`backbone-ripple` (package `backbone-ripple`, repository URL in `package.json` says `backbone-sync-ripple`) is a dormant, half-built 2014 library of Backbone models and collections for the Ripple-REST API. Version 0.1.0. Treat it as a historical showcase.

## Stack

- Node.js, CommonJS, no build step.
- Dependencies: `backbone ^1.1.2`, `jquery ^2.1.1`, `superagent ^0.18.2`, `bluebird ^2.3.2`.
- Tests: mocha (`mocha -R spec test/`), not listed as a dependency.
- Default branch: `master`.

## Layout

- `index.js`: exports Account, Balance, Balances, Payment, Payments.
- `lib/`: one file per model or collection, plus `backbone.js` which wires jQuery into Backbone.
- `test/account.js`, `test/balances.js`: sketches that call live Ripple services.
- `docs/STATUS.md`: current state and gap to the repo standard.

## Commands

- Install: `npm install` (not verified on a current Node; jQuery 2 under Node may also need a DOM such as jsdom, **(inference)**).
- Test: `npm install --no-save mocha && npm test`. Known not to work as written: `test/balances.js` uses `Balances` without requiring it and calls `lookupName`, which does not exist.
- Run: it is a library; there is nothing to start.

## Rules

- Add or update tests with every code change. Prefer tests that stub HTTP.
- Never commit secrets. There are none in the repo today.
- Use Conventional Commits.
- Keep `docs/STATUS.md` current.

## What agents may and may not do

- May: improve docs, fix clear bugs, add tests, open pull requests.
- May not: archive the repo, publish to npm, rewrite git history, or rename the default branch without Steven's say-so.
