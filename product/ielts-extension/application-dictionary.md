# Application Dictionary

## Purpose

Define ubiquitous language for product specs, diagrams, API contracts, database models, code names, Linear issues, and design artifacts.

## Core Learner Terms

- Learner: the person studying IELTS.
- Local Profile: anonymous extension profile before app login.
- Connected Account: app account linked to extension data.
- Learner Extension Preferences: extension-level settings such as result autosave and dictionary lookup mode.
- Learner AI Usage: app-provided quota and learner-provided AI access state.
- Result Autosave: preference that stores completed-test result data automatically after opt-in.

## Practice Terms

- Practice Session: one attempt at an IELTSOnlineTests exercise.
- Exercise Context: source and question-level context captured for private revision.
- Test Result: score and result-screen data from a completed practice session.
- Mistake Record: question-level incorrect answer data, when visible after review.
- Mistake Tag: fixed enum describing why a mistake likely happened.
- Unsure Marker: learner flag set during practice before result review.

## Mistake Tags

- `misheard_word`
- `spelling`
- `missed_keyword`
- `distractor_trap`
- `synonym_gap`
- `number_or_date`
- `plural_or_word_form`
- `timing`
- `instruction_misread`
- `unknown`

## Vocabulary Terms

- Saved Vocabulary: a word or phrase saved by the learner.
- Term: single saved word.
- Phrase: multi-word saved expression.
- Source Context: limited surrounding text, question, timestamp, and URL needed for private revision.
- Learner Note: optional note added by the learner.

## Dictionary Terms

- Dictionary Entry: reusable meaning, translation, pronunciation, and example record.
- Definition: English meaning of a term or phrase.
- Translation: Vietnamese translation or explanation.
- Pronunciation: phonetic text, audio URL, or pronunciation guidance.
- Example Sentence: example usage shown in the vocabulary card or review flow.
- Lookup Source: cache, FreeDictionaryAPI, translation provider, or AI enrichment.
- Attribution: source metadata required for dictionary/provider content.

## Review Terms

- Review Card: one reviewable item generated from saved vocabulary.
- Review Stage: recognition, context, pronunciation, or usage.
- Review Attempt: learner response to one review card.
- Speech Assessment: evaluation of learner-spoken pronunciation for a review card.
- Due Review: review card scheduled for practice now.
- Ease: spaced-repetition difficulty factor.
- Interval: time until the next review.

## Dashboard Terms

- Score History: learner's completed practice-session scores over time.
- Mistake Pattern: repeated mistake trend across sessions.
- Question Type Breakdown: mistake grouping by IELTS question type.
- Part Breakdown: mistake grouping by Listening part.
- Not Enough Data State: dashboard state shown before enough volume exists for meaningful trends.

## Parser Terms

- Parser Event: telemetry event emitted by the extension parser.
- Parser Health: aggregate view of whether IELTSOnlineTests markup parsing still works.
- Parser Version: version of the extension parser that emitted the event.
- Parse Outcome: success or failure for a parser step.
- Parser Error Code: stable error code describing why parser extraction failed.
