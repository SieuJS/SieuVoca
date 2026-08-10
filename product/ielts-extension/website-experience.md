# Website Experience

## Purpose

Define website review and dashboard experiences.

## Vocabulary Review

The first website review experience is vocabulary.

Each saved word enters an automatic ladder:
1. Recognition.
2. Context recall.
3. Pronunciation.
4. Speaking or writing usage.

Recognition can use self-rating: Again, Hard, Good, Easy.

Context recall should support typed answers with fuzzy matching.

Pronunciation should support speech-to-text or pronunciation scoring when feasible.

Speaking/writing usage should support AI judgment when the user has free quota or their own API key connected.

## Review Ladder Rules

- New saved terms start at `recognition`.
- Promote from `recognition` to `context` after two successful reviews with `Good` or `Easy`, with no recent `Again`.
- Promote from `context` to `pronunciation` after two correct typed-context attempts.
- Promote from `pronunciation` to `usage` after two accepted pronunciation attempts.
- Demote one stage after two consecutive failures.
- Keep review due dates independent from stage promotion.

## Mistake Dashboard

Shows captured practice history from the extension.

MVP widgets:
- Recent Listening scores. Ship first because it is useful after one session.
- Raw correct count and total questions when available. Ship first because it is useful after one session.
- Wrong question count by test. Ship first if review capture exposes correctness.
- Mistakes by question type. Show only after at least three captured sessions or enough mistakes to make the pattern meaningful.
- Mistakes by part. Show only after at least three captured sessions or enough mistakes to make the pattern meaningful.
- Unsure questions that became wrong.
- Link back to original IELTSOnlineTests test.

Pattern widgets must show honest empty states such as "not enough data yet" instead of sparse charts.

## Knowledge Hub

MVP contents:
- Saved words and phrases.
- Exercise context.
- Notes.
- Unsure markers.
- Scores.
- Mistakes.
- Review state.

