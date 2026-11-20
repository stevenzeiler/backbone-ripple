# Status

Last reviewed: 2026-11-20 (github-audit pass 02, docs only).

## What works

Nothing was run in this pass. By reading the code, five small Backbone classes exist (Account, Balance, Balances, Payment, Payments), each a few lines long.

## What is broken or unknown

- `TrustLine`, `TrustLines` and `Notification`, listed in the original README, were never written.
- `Account.setBalances` calls `balances.setAccount`, which `Balances` does not define, so the account to balances link is incomplete.
- `Balances` and `Payments` use relative URLs (`/v1/accounts/...`) and no Ripple-REST base URL is configurable.
- `Account` points at `https://id.ripple.com/v1/authinfo`, a 2014 endpoint that may no longer exist.
- `test/balances.js` does not require `Balances`, calls `lookupName` (not defined), and `test/account.js` calls the network and passes without asserting anything.
- mocha is not a declared dependency.
- The package name (`backbone-ripple` vs `backbone-sync-ripple` in the URLs) is inconsistent, and `package.json` has an empty author.
- Whether jQuery 2 and Backbone work together in Node without a DOM was not checked.

## What's next

1. Decide whether to keep this as a read-only showcase or archive it (Steven's decision).
2. If keeping it: add a configurable base URL, finish or delete the promised models, fix the tests.

## Not yet from the standard

- CONTRIBUTING.md
- SECURITY.md
- .editorconfig
- .github issue and pull request templates
- Dependabot configuration
- `ci.yml` with gitleaks
- Rename `master` to `main`
- CloudEvents catalog
- Product one-pager
