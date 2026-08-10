# IELTS Extension Context

## Documentation Entry Point

The extension MVP documentation has been split into focused child files.

Start here:

`product/ielts-extension/index.md`

## Current Product Direction

The product direction has shifted from building a standalone IELTS practice importer first to building a Chrome extension companion for IELTSOnlineTests.

The extension should support learners while they practice on the original website, without copying and re-hosting IELTSOnlineTests material in the app.

## Main Learning Loop

MVP focus is practice-first, especially Listening.

Selected loop:
- User practices directly on IELTSOnlineTests.
- Extension observes the practice page and provides study tools.
- User saves unknown words, useful phrases, notes, and unsure questions.
- After submit/review, extension captures mistakes and weak question types where possible.
- Saved learning data syncs to the IELTS Study app knowledge hub.
- User returns to the app to review vocabulary and repeated mistakes using spaced repetition.

Planner-first and knowledge-hub-first workflows are future layers, not the first MVP focus.

## Extension MVP Scope

The extension should be a study assistant, not a test solver.

During a test, it should support:
- Highlight word or phrase.
- Show an inline dictionary card.
- Save word or phrase for review.
- Save source context: website, test title, URL, skill, question number, nearby sentence/context, and timestamp if available.
- Save exercise context for later personal revision, including source link, test metadata, question metadata, and limited surrounding content needed to understand the saved item.
- Mark unsure questions.
- Add lightweight notes.
- Detect the submitted review/result page where possible.
- Capture test score, wrong questions, question types, and mistake metadata into the dashboard.

The extension should avoid:
- Giving direct answer hints during test practice.
- Publicly re-hosting copied test content.
- Depending on copied IELTSOnlineTests materials as the public product model.

## Vocabulary Card Decision

Selected MVP behavior: inline dictionary card.

When a learner highlights a word or phrase, show:
- English meaning.
- Vietnamese translation.
- Pronunciation if available.
- Example sentence.
- Source test and question number.
- Save button.
- Optional learner note, such as "I heard this wrong" or "I don't know this word."

AI enrichment can be added later, but the MVP should not require AI for every lookup.

## Storage And Sync Decision

Selected approach: hybrid sync.

The extension should save locally first so it works immediately without login. When the learner connects or logs into the IELTS Study app, local saved items should sync to the backend knowledge hub.

Selected sync behavior: auto-sync plus session-end summary.

When the learner is logged into the IELTS Study app, the extension should sync eligible local data in the background. After the learner finishes a practice session or reaches a review/result page, the extension should show a clear session summary and sync status.

Local-first data should include:
- Saved words and phrases.
- User notes.
- Unsure question markers.
- Source page/test metadata.
- Exercise context for personal revision.
- Basic timestamps.
- Sync status.

Backend-synced data should support:
- Knowledge hub review.
- Spaced repetition.
- Mistake history.
- Weak skill/question-type tracking.
- Future planner recommendations.

## Backend Architecture Decision

Backend implementation should use microservices, with Clean Architecture inside each service.

Domain language should be defined before coding so entities, use cases, repositories, API contracts, and Linear tickets use the same words.

Core services:
- Identity Profile Service.
- Practice Capture Service.
- Vocabulary Service.
- Dictionary Service.
- Review Service.
- Dashboard Analytics Service.
- Parser Health Service.
- AI Speech Service.

The microservice choice is intentional even though it is harder. It means service ownership, API/event contracts, observability, local orchestration, retries, and contract tests are part of MVP architecture.

Canonical MVP use cases:
- `ConnectExtensionProfile`
- `UpdateLearnerExtensionPreferences`
- `UpdateLearnerAiAccess`
- `GetExtensionSyncStatus`
- `SaveHighlightedVocabulary`
- `LookupDictionaryCard`
- `SaveExerciseContext`
- `MarkQuestionUnsure`
- `CapturePracticeResult`
- `StoreCompletedTest`
- `MergeResultIntoExerciseContext`
- `GetVocabularyReviewQueue`
- `GetDueReviewCards`
- `SubmitReviewAttempt`
- `PromoteOrDemoteReviewStage`
- `GetScoreDashboard`
- `GetSingleSessionSummary`
- `GetMistakeDashboard`
- `RecordParserHealthEvent`
- `AggregateParserHealth`

Core domain terms:
- Learner.
- Local Profile.
- Connected Account.
- Learner Extension Preferences.
- Result Autosave.
- Practice Session.
- Exercise Context.
- Test Result.
- Mistake Record.
- Mistake Tag.
- Unsure Marker.
- Saved Vocabulary.
- Term.
- Phrase.
- Source Context.
- Dictionary Entry.
- Lookup Source.
- Attribution.
- Review Card.
- Review Stage.
- Review Attempt.
- Due Review.
- Score History.
- Mistake Pattern.
- Parser Event.
- Parser Health.

The detailed component map, use cases, ports, and ubiquitous language live in:
- `product/ielts-extension/backend-clean-architecture.md`
- `product/ielts-extension/microservices-architecture.md`
- `product/ielts-extension/application-dictionary.md`

## Linear Documentation

Planning and architecture context is also stored in Linear under the `IELTS Study App MVP` project.

Linear project:
- `IELTS Study App MVP`
- URL: `https://linear.app/sieu-nguyen/project/ielts-study-app-mvp-823d44f4fed6`

Linear documents:
- Backend Clean Architecture Component Map: `https://linear.app/sieu-nguyen/document/backend-clean-architecture-component-map-0a24c3d67579`
- Application Dictionary And Ubiquitous Language: `https://linear.app/sieu-nguyen/document/application-dictionary-and-ubiquitous-language-adfae4ce2fb3`
- System Architecture Diagrams: `https://linear.app/sieu-nguyen/document/system-architecture-diagrams-530ed3444364`

The System Architecture Diagrams document uses Mermaid diagrams and includes:
- System Context.
- Clean Architecture Backend.
- Vocabulary Capture and Dictionary Lookup Flow.
- Practice Result Capture Flow.
- Review Ladder Flow.
- Dashboard Data Availability.

Hidden/system concerns represented in the diagrams:
- Anonymous local profile vs connected account.
- Local-first storage and sync queue.
- Result autosave preference.
- Parser health telemetry.
- Review-page validation gate.
- Cache-first dictionary lookup.
- FreeDictionaryAPI attribution.
- AI fallback.
- Terms/account-risk gate.
- Private revision boundary.

Future planning should keep Linear and local docs aligned. If domain terms change, update both the local spec/context and the Linear Application Dictionary.

## Website Review Experience Decision

Selected first website experience: vocabulary review.

The extension should sync saved words and phrases into the website knowledge hub. The website should then help the learner remember and use those words over time.

Vocabulary review should include:
- Recognition cards: show the word or phrase, ask the learner to recall the meaning, then reveal English meaning, Vietnamese translation, and example usage.
- Context cards: show the original or generated sentence with the saved word hidden, then ask the learner to choose or type the missing word.
- Pronunciation practice: ask the learner to speak the word and compare against expected pronunciation where feasible.
- Usage practice: ask the learner to use the word in a short spoken answer or written sentence to deepen memory.

Recognition cards are the first build priority because they work for every saved word. Context, pronunciation, speaking usage, and writing usage are important follow-up review modes.

Selected progression model: automatic ladder.

Each saved word should start with recognition review. As the learner succeeds, the app should unlock harder review modes:
1. Recognition.
2. Context recall.
3. Pronunciation.
4. Speaking or writing usage.

The learner should not need to manually decide the right next mode for every word. The review engine should choose the next appropriate prompt based on recall history.

Review scoring should support objective checks, not only self-rating:
- Recognition can use self-rating for MVP.
- Context recall should support typed answers with fuzzy matching.
- Pronunciation should use speech-to-text or pronunciation scoring where feasible.
- Speaking usage should use AI to judge whether the learner used the word naturally.
- Writing usage should use AI to judge correctness, grammar, and whether the word fits the context.

Selected AI access model: hybrid.

The app should provide a small free AI quota for a smooth first-time experience. Advanced or heavy AI features should support the learner's own API key. This balances onboarding friction, app operating cost, and power-user flexibility.

AI usage should have an explicit data model:
- `learnerId`
- `freeQuotaLimit`
- `freeQuotaUsed`
- `freeQuotaResetsAt`
- `learnerApiKeyStatus`
- `preferredAiProvider`
- `createdAt`
- `updatedAt`

Raw learner API keys must be stored only in the secure secret mechanism chosen by implementation, not in ordinary domain tables or logs.

`learnerApiKeyStatus` in Learner AI Usage is the source of truth for learner-provided API key setup. Do not duplicate that setup state in Learner Extension Preferences.

Pronunciation assessment should use the `SpeechAssessmentProvider` port. Candidate path:
- Validate browser Web Speech API first for MVP speech-to-text.
- Add a server-side speech-to-text or pronunciation assessment adapter if browser support is not enough.
- If speech assessment is unavailable, pronunciation review can fall back to manual self-rating.

## IELTSOnlineTests Page Investigation

An exported logged-in listening test page exists at:

`crawl/IELTS Mock Test 2025 February Listening Practice Test 1.html`

Observed from the exported HTML:
- Test title: IELTS Mock Test 2025 February Listening Practice Test 1.
- Original URL includes `mode=practice_test`, `parts=full`, and `duration=32`.
- Page is a logged-in listening test page.
- The test contains 40 questions.
- There are 4 parts, 10 questions each.
- The page includes an audio URL.
- The page includes "Listen from here" timestamps.
- Question types observed:
  - `q_type=6`: multiple choice / radio.
  - `q_type=8`: likely checkbox / multi-select.
  - `q_type=9`: fill in the blank.
- The exported HTML did not include answer keys, transcript, explanations, or final result data.

Product implication:
- The extension can read page structure, question numbers, question types, user selections, and timestamps.
- Mistake capture likely needs access to the post-submit review/result state.
- The app should store learner-owned metadata and notes, not copy and republish the original test content.

## Mistake Dashboard Decision

The MVP should include automatic score and mistake capture from IELTSOnlineTests result/review pages where technically possible.

This is a validation gate, not a proven implementation detail. The only inspected exported page is a pre-submit exercise page. Before building dashboard parsing, capture and inspect a real submitted review/result page.

Review page validation must answer:
- Whether score is visible.
- Whether per-question correctness is visible.
- Whether user answers and correct answers are visible.
- Whether result data persists or is transient.
- Whether access requires a paid tier or other account state.

Selected result-screen behavior:
- When the learner reaches the result/review screen, the extension should automatically detect and read the visible score.
- If the learner is connected and has enabled result autosave, store/sync the practice session, score, and any visible mistake metadata without a per-test prompt.
- If the learner is anonymous, show a local session summary with a combined connect + enable autosave CTA.
- If the learner is connected but result autosave is disabled, show a one-time "always save my results" setting.
- The learner should be able to change result autosave later in extension settings.
- The extension should not submit the test for the learner or interfere before submission.

The extension should collect:
- Test title.
- Test URL.
- Skill, starting with Listening.
- Completion date.
- Overall score or raw correct count when visible.
- Question-level correctness when visible.
- User answer and correct answer when visible on the review page.
- Question type.
- Part number.
- Unsure marker if the user marked it during practice.
- Limited exercise context needed for personal revision.

The website dashboard should show score history and mistake patterns. This is separate from direct answer hints during practice; the extension should analyze results after the learner submits.

Dashboard sequencing:
- Show recent Listening scores and raw score first because these are useful after one completed session.
- Show wrong count by test when correctness is available.
- Show mistake-by-type and mistake-by-part pattern widgets only after enough sessions or mistakes exist.
- Pattern widgets should show "not enough data yet" instead of sparse charts.

Mistake tags should use a fixed enum from day one:
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

## Exercise Context Decision

The extension should save the exercise the learner is currently doing so the app can support later revision.

For MVP, saved exercise context should include:
- Source website and canonical URL.
- Test title and collection name if available.
- Skill and part.
- Question number and question type.
- Listening timestamp when available.
- User answer.
- Correct answer if later visible on review page.
- Nearby sentence or prompt context required to understand the saved word, mistake, or unsure question.
- Link back to the original IELTSOnlineTests page.

The app should use saved exercise context for the learner's private revision workflow. It should not publish, share, or present copied third-party test content as the app's own content library.

## Product Risk Gates

Third-party site dependency:
- The extension depends on IELTSOnlineTests DOM structure.
- MVP should include parser-health tracking so markup breakage is visible in aggregate.
- Track parser version, page detection, metadata parse success, question parse success, result parse success, and parser error code.

Terms and account risk:
- Before public launch, review whether IELTSOnlineTests allows read-only extension capture from logged-in user pages for private study history.
- The extension should not ask for IELTSOnlineTests passwords, cookies, or login tokens.
- If terms are incompatible, change scope to local/private capture, explicit user export, or a different source model.

Conversion moment:
- Anonymous users should still get a local session-end summary.
- After saving words or finishing a test, show a soft signup CTA to keep scores and see patterns over time.
- On the result screen, avoid interrupting connected users who already opted into result autosave. For anonymous users, the session summary should include signup/connect as the next step.

Learner preference:
- Store result autosave as an extension-level learner preference, not on each synced record.
- Suggested fields: `localProfileId`, `remoteUserId`, `resultAutosaveEnabled`, `resultAutosavePromptedAt`, `dictionaryLookupMode`, `createdAt`, `updatedAt`.
- Anonymous users may have a local preference, but remote result sync starts only after connecting to the IELTS Study app.

Dictionary provider:
- The inline dictionary card requires English definition, Vietnamese translation, pronunciation, and examples.
- First candidate provider: FreeDictionaryAPI (`https://freedictionaryapi.com/`).
- FreeDictionaryAPI provides Wiktionary-backed structured entries, definitions, pronunciations, examples, optional translations, no API key, CORS support, and a 1,000 requests/hour/IP limit.
- Validate whether FreeDictionaryAPI reliably returns Vietnamese translations for IELTS vocabulary. If not, pair it with translation or AI enrichment.
- If lookup fails, allow raw save first and enrich later.
- Lookup order should be:
  1. Search our cached dictionary database.
  2. Search FreeDictionaryAPI through our backend on cache miss.
  3. Use AI to generate missing meaning/translation/example/pronunciation guidance.
  4. Store external and AI-enriched results in our database for reuse.
- FreeDictionaryAPI calls should be backend-proxied rather than called directly from the extension.
- Because the 1,000 requests/hour/IP limit would apply to the backend IP, cache-first lookup is a hard requirement.
- Backend tests should enforce cache-first lookup before FreeDictionaryAPI and persistence of external/AI-enriched dictionary entries.
- Stored dictionary entries should include attribution/source metadata when based on FreeDictionaryAPI/Wiktionary.

Review ladder rules:
- New terms start at recognition.
- Promote from recognition to context after two successful Good/Easy reviews with no recent Again.
- Promote from context to pronunciation after two correct context attempts.
- Promote from pronunciation to usage after two accepted pronunciation attempts.
- Demote one stage after two consecutive failures.

## Open Product Questions

- What exactly is available on a submitted IELTSOnlineTests review/result page?
- Which dictionary/translation providers should power the inline card?
- What is the acceptable legal/product scope after reviewing IELTSOnlineTests terms?
