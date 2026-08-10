# Validation Gates

## Purpose

Capture assumptions that must be validated before implementation depends on them.

## Review Page Capture Gate

Score and mistake capture is a load-bearing assumption. The only inspected artifact so far is a pre-submit logged-in Listening page export. A real submitted review/result page must be captured and analyzed before committing to per-question mistake parsing.

Before dashboard implementation starts, capture and inspect at least one real submitted IELTSOnlineTests Listening review/result page.

Validation questions:
- Does the result page expose raw score, percentage, or band-like feedback?
- Does it expose per-question correctness?
- Does it expose the user's answer?
- Does it expose the correct answer?
- Does review data persist after navigation/reload, or is it transient?
- Does access require a paid tier or account state beyond normal login?
- Is the review page rendered in DOM, loaded through an API, or both?

Outcomes:
- If score and per-question correctness are available, implement score history and mistake dashboard.
- If only score is available, implement score history first and defer per-question mistakes.
- If neither score nor correctness is available, keep local vocabulary/exercise context and remove dashboard work from MVP.

## Terms And Account-Risk Gate

Before launch, explicitly review IELTSOnlineTests terms and account-risk implications for a browser extension that reads logged-in page DOM for a learner's private study history.

The product should not ask users to provide IELTSOnlineTests passwords, cookies, or tokens. The extension should operate only in the user's browser session and should avoid automated bulk extraction behavior that looks like crawling.

## Dictionary Provider Gate

Validate FreeDictionaryAPI and fallback enrichment for:
- English meaning.
- Vietnamese translation.
- Pronunciation.
- Example sentence.
- Latency.
- Attribution.
- Rate limits.

## Speech Assessment Gate

Validate pronunciation assessment before implementing pronunciation-stage review.

Candidate path:
- Browser Web Speech API for speech-to-text where supported.
- Server-side speech-to-text or pronunciation assessment provider behind `SpeechAssessmentProvider` if browser support is not enough.
- Manual self-rating fallback when speech assessment is unavailable.

