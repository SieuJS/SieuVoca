# IELTS Study App Context

## Current Product Direction

Build an IELTS study application for both learners and tutors over time, but start learner-first.

MVP direction selected by the user:
- Target user: both learners and tutors eventually, but learner-first.
- MVP focus: full IELTS study planner first, covering Listening, Reading, Writing, and Speaking lightly.
- Timeline assumption: 8-week MVP.

Recommended MVP product concept:
An IELTS study companion where a learner enters their target band, exam type, exam date, available study time, and weak areas. The app generates a daily/weekly study plan, assigns practice tasks across the four IELTS skills, tracks progress, and gives light AI feedback.

## Documentation Strategy

Use Linear for product planning and execution:
- Product brief
- MVP scope
- Roadmap
- Milestones
- Backlog issues
- Weekly tasks

Use Mintlify later for code/developer documentation:
- Architecture
- Setup guide
- API docs
- Database schema docs
- AI prompt/evaluation docs
- Deployment docs

Do not store the main product planning document in the repository unless the user asks. This file is only a short handoff note for the next Codex session.

## MCP Status

Mintlify MCP:
- Added globally.
- OAuth login completed successfully.

Linear MCP:
- Added globally with URL `https://mcp.linear.app/mcp`.
- OAuth login completed successfully.
- A new Codex session is likely required before Linear MCP tools are available in the active tool set.

## Next Session Task

Create a Linear project named:

`IELTS Study App MVP`

Store the product planning document in the Linear project description. Then create Linear issues/milestones for an 8-week MVP.

Suggested Linear project content:
- Product overview
- Target users
- Problem statement
- MVP scope
- Non-goals
- Core user journey
- Feature list
- 8-week timeline
- Risks and assumptions
- Next steps

Suggested 8-week timeline:
- Week 1: Product definition, user flows, database model, app architecture
- Week 2: Auth, onboarding, target band, exam date, current level setup
- Week 3: Study plan generator and learner dashboard
- Week 4: Daily task system and progress tracking
- Week 5: Practice flows for Listening, Reading, Writing, and Speaking
- Week 6: Light AI feedback for Writing and Speaking
- Week 7: Review dashboard, weak-area recommendations, polish
- Week 8: QA, seed content, beta launch, feedback collection

Recommended first build priority:
Start with onboarding and the study plan engine, not a large content library.
