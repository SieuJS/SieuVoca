# Data Model

## Purpose

Define records and fields for the MVP domain.

## Extension Local Record

- `localId`
- `remoteId`
- `type`
- `sourceSite`
- `sourceUrl`
- `canonicalUrl`
- `testTitle`
- `skill`
- `partNumber`
- `questionNumber`
- `questionType`
- `listeningTimestampSec`
- `createdAt`
- `updatedAt`
- `syncStatus`
- `syncError`

## Learner Extension Preferences

- `localProfileId`
- `remoteUserId`
- `resultAutosaveEnabled`
- `resultAutosavePromptedAt`
- `dictionaryLookupMode`
- `aiAccessMode`
- `createdAt`
- `updatedAt`

`resultAutosaveEnabled` controls whether completed-test results sync automatically after the result/review page is detected.

`aiAccessMode` selects how AI-backed features should be attempted, such as app quota first or learner API key. It does not store API-key setup state.

## Learner AI Usage

- `learnerId`
- `freeQuotaLimit`
- `freeQuotaUsed`
- `freeQuotaResetsAt`
- `learnerApiKeyStatus`
- `preferredAiProvider`
- `createdAt`
- `updatedAt`

Raw API keys must be stored only in the secure secret mechanism chosen by implementation, not in ordinary domain tables or logs.

`learnerApiKeyStatus` is the source of truth for whether a learner-provided API key is configured. Do not duplicate this state in Learner Extension Preferences.

## Saved Vocabulary

- `term`
- `normalizedTerm`
- `language`
- `meaningEn`
- `translationVi`
- `pronunciation`
- `exampleSentence`
- `learnerNote`
- `sourceContext`
- `exerciseContextId`
- `reviewStage`
- `reviewDueAt`
- `reviewStats`

## Exercise Context

- `sourceSite`
- `sourceUrl`
- `canonicalUrl`
- `collectionTitle`
- `testTitle`
- `skill`
- `quizId`
- `durationMinutes`
- `partNumber`
- `questionNumber`
- `questionType`
- `listeningTimestampSec`
- `promptContext`
- `nearbyText`
- `userAnswer`
- `correctAnswer`
- `isCorrect`
- `markedUnsure`

## Practice Session

- `sourceSite`
- `sourceUrl`
- `testTitle`
- `skill`
- `startedAt`
- `completedAt`
- `rawScore`
- `totalQuestions`
- `percentCorrect`
- `durationMinutes`
- `capturedFromReviewPage`
- `syncSource`

## Mistake Record

- `practiceSessionId`
- `exerciseContextId`
- `questionNumber`
- `partNumber`
- `questionType`
- `userAnswer`
- `correctAnswer`
- `markedUnsure`
- `mistakeTags`
- `createdAt`

## Review Card State

- `savedVocabularyId`
- `stage`
- `stageAttemptStreak`
- `stageFailureStreak`
- `dueAt`
- `intervalDays`
- `ease`
- `lastResult`
- `attemptCount`
- `correctCount`
- `incorrectCount`

Allowed `stage` values:
- `recognition`
- `context`
- `pronunciation`
- `usage`
