# Risk And Compliance

## Purpose

Capture privacy, copyright, ToS, account-risk, and parser-health concerns.

## Privacy And Copyright Boundaries

The product stores learner-owned study records for private revision.

The extension may capture limited surrounding context so the learner can understand saved words and mistakes later. The app must not publish, share, or market copied IELTSOnlineTests content as its own test library.

The app should link back to the original source page when revision depends on third-party exercise context.

Secrets such as site cookies, login tokens, and passwords must not be stored by the extension or backend.

## Terms And Account Risk

Before public launch, confirm that the extension's read-only DOM capture of a user's logged-in IELTSOnlineTests session does not violate IELTSOnlineTests terms or create account-risk for learners.

If terms are incompatible, ship only local/private capture, require explicit user export, or change the product direction.

This is a product/legal checklist concern, not a bounded component or domain entity.

## Parser Health

Because the product depends on one third-party site's markup, parser health is part of MVP quality.

Track aggregate parser outcomes:
- supported page detected
- test metadata parsed
- question metadata parsed
- vocabulary context parsed
- result page detected
- score parsed
- per-question correctness parsed
- parser error code
- parser version
- source page path

Alerting can be lightweight at first, but the team should be able to see when a markup change causes a spike in parser failures.

