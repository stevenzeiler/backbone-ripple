# Backbone Ripple

A set of Backbone models and collections meant to sync with the Ripple-REST API server.

> **Status: dormant since 2014, and only partly built.** The last commit is from October 2014 (version 0.1.0). This was a 2014 experiment on the Ripple network. The README below was written first and promises more than the code delivers. This documentation pass did not run it.

Ripple-REST is documented at http://dev.ripple.com/ripple-rest.html (the 2014 docs address).

## What exists today

| Piece | In the code? |
|---|---|
| `Account` model (its `fetch` calls the Ripple name lookup URL) | yes |
| `Balance` model and `Balances` collection | yes |
| `Payment` model and `Payments` collection | yes |
| `TrustLine` model, `TrustLines` collection | planned, not written |
| `Notification` model | planned, not written |

## Install

The repo is named `backbone-ripple`, but `package.json` says `backbone-sync-ripple` in its repository URL. Install from a clone:

    git clone https://github.com/stevenzeiler/backbone-ripple
    cd backbone-ripple
    npm install

The README originally suggested `npm install --save backbone-ripple`. Whether that package exists on npm was not checked.

## Usage

    var BackboneRipple = require("backbone-ripple");

    // Models
    BackboneRipple.Account
    BackboneRipple.Balance
    BackboneRipple.Payment

    // Collections
    BackboneRipple.Balances
    BackboneRipple.Payments

`Balances` and `Payments` build their URL from an account (`/v1/accounts/<address>/balances` and `/payments`) and need an `account` property that nothing sets yet (`Account` calls `balances.setAccount`, which is not defined). `Account` looks up a name at `https://id.ripple.com/v1/authinfo`, a 2014 Ripple endpoint. Treat these as sketches.

## Configuration

None. No environment variables or keys. Server addresses are written into the `lib/` files.

## How it works

Each file in `lib/` extends `Backbone.Model` or `Backbone.Collection` with a `url` and a `parse` function that unwraps the Ripple-REST response (for example `response.balances`). `lib/backbone.js` attaches jQuery to Backbone so `fetch` can make HTTP calls in Node.

## Tests

    npm test

Runs `mocha -R spec test/`. mocha is not listed in `package.json`, so install it first (`npm install --no-save mocha`). The tests call live Ripple services and the balances test calls `lookupName`, which does not exist, so do not expect them to pass. See `docs/STATUS.md`.

## License

ISC, as declared in `package.json`. See `LICENSE`.
