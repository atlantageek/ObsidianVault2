Below is a **handoff-ready roadmap** for your **Fiber Technician AI Helper Agent**, formatted for **engineering, design, and leadership**. It turns your brief into a practical product plan with phases, feature descriptions, user stories, acceptance criteria, dependencies, and measurable outcomes. 

---

# Fiber Technician AI Helper Agent Roadmap

## 1. Executive Summary

The Fiber Technician AI Helper Agent should evolve from a basic Q&A assistant into a **workflow-aware field copilot** that helps technicians complete jobs faster, reduce mistakes, understand test results, and troubleshoot issues in real time.

The agent should support fiber workflows such as:

* Job preparation
* Fiber installation
* OTDR testing
* PON/power testing
* RF/channel testing if applicable
* Waiting during test execution
* Test result explanation
* Failure troubleshooting
* Upload/save guidance
* Escalation and supervisor handoff

The goal is not just to make the AI “smarter,” but to make it **context-aware, technician-friendly, proactive, and safe**.

---

# 2. Product Goals

| Goal                       | Description                                                                                  | Business Outcome                                   |
| -------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| Make the agent smarter     | Give the AI access to job context, test state, device data, result files, and SOPs           | Fewer support calls and better technician guidance |
| Make it more natural       | Short, field-friendly responses with conversational follow-ups                               | Higher technician adoption                         |
| Support real workflows     | Guide technicians before, during, and after tests                                            | Faster job completion                              |
| Handle edge cases          | Support failures, offline mode, upload issues, wrong location, missing data, abnormal traces | Less rework and fewer failed jobs                  |
| Help during test wait time | Use idle time to prepare techs for next steps                                                | Reduced downtime                                   |
| Create a phased build plan | Build in realistic increments                                                                | Easier engineering execution                       |

---

# 3. Recommended MVP Scope

The MVP should focus on **high-value workflow support**, not advanced prediction.

## MVP Should Include

1. **Knowledge-grounded technician Q&A**
2. **Workflow-specific guidance**
3. **Test waiting assistant**
4. **Basic result explanation**
5. **Failure troubleshooting decision tree**
6. **Upload/save guidance**
7. **Escalation summary generation**
8. **Technician feedback capture**

## MVP Should Not Include Yet

* Personalized technician coaching
* Historical prediction models
* Advanced AI result comparison
* Fully autonomous recommendations
* Complex supervisor analytics
* Full multilingual support unless required by customers

---

# 4. Phased Roadmap Overview

| Phase   | Name                    | Goal                                                              | Timeline   | Primary Audience                 |
| ------- | ----------------------- | ----------------------------------------------------------------- | ---------- | -------------------------------- |
| Phase 1 | Foundation Agent        | Make AI useful and safe with grounded knowledge                   | 0–30 days  | Technicians, Support             |
| Phase 2 | Workflow-Aware Agent    | Make AI aware of job step and test status                         | 30–60 days | Technicians                      |
| Phase 3 | Troubleshooting Agent   | Help technicians resolve failed/abnormal tests                    | 60–90 days | Technicians, Supervisors         |
| Phase 4 | Proactive Field Copilot | Predict issues, personalize guidance, support leadership insights | 90+ days   | Technicians, Ops, QA, Leadership |

---

# 5. Phase 1: Foundation Agent

## Goal

Create a reliable AI assistant that can answer fiber technician questions using approved company knowledge, SOPs, test procedures, and device documentation.

## Key Features

### Feature 1.1 — Knowledge-Grounded Technician Q&A

**Description**
The agent answers technician questions using approved fiber installation guides, device manuals, SOPs, troubleshooting docs, and test procedure documentation.

**User Story**
As a field technician, I want to ask the AI questions about fiber testing and installation so I can get quick answers without calling support.

**Example Questions**

* “What does this OTDR event mean?”
* “What should I check before running the test?”
* “What is a good power level?”
* “How do I know if the result is acceptable?”
* “What should I do before uploading?”

**Acceptance Criteria**

* The AI only answers from approved knowledge sources.
* The AI can cite or reference the source category internally.
* If the AI is unsure, it says it is unsure and suggests escalation.
* The AI avoids guessing on safety, compliance, or pass/fail rules.
* Responses are short and technician-friendly by default.

**Dependencies**

* Approved knowledge base
* Document ingestion pipeline
* RAG/search layer
* AI safety rules
* Basic chat UI

**Measurable Outcomes**

* 30% reduction in basic support questions
* 70%+ helpful rating from technician feedback
* Less than 5% unsafe or ungrounded answers in QA review



---

### Feature 1.2 — Workflow-Specific Suggested Prompts

**Description**
Show contextual prompt buttons based on where the technician is in the app.

**Examples**

On job start:

* “What should I check first?”
* “Help me prepare for this install”
* “What tools do I need?”

On test screen:

* “Explain this test”
* “What happens if this fails?”
* “What should I do while waiting?”

On result screen:

* “Explain this result”
* “Why did this fail?”
* “What should I try next?”

**User Story**
As a technician, I want suggested questions so I do not have to type everything manually in the field.

**Acceptance Criteria**

* Prompt suggestions change based on screen or workflow step.
* Prompts are short and action-oriented.
* Prompts are available in chat and test screens.
* Tapping a prompt sends the question to the agent with current screen context.

**Dependencies**

* App screen/state detection
* Prompt configuration file
* Chat integration

**Measurable Outcomes**

* 40%+ of AI interactions started from suggested prompts
* Increased AI usage during test workflows
* Reduced typing burden in field conditions

---

### Feature 1.3 — Basic Test Explanation

**Description**
The agent explains what each supported test does, what the technician should expect, and what a pass/fail means in plain language.

**User Story**
As a technician, I want the AI to explain the test I am running so I understand what is happening and what result to expect.

**Acceptance Criteria**

* AI can explain OTDR, PON/power, and RF/channel scan tests where applicable.
* AI provides plain-English explanation first.
* AI can provide technical detail if the technician asks.
* AI explains what the technician should avoid during the test.

**Dependencies**

* Test type metadata
* Test procedure documentation
* UI integration with current test screen

**Measurable Outcomes**

* Improved technician understanding score in pilot survey
* Reduced incorrect test execution issues
* Reduced repeat questions about common tests

---

### Feature 1.4 — Feedback Capture

**Description**
Technicians can rate AI responses and flag incorrect, unclear, or unhelpful answers.

**User Story**
As a technician, I want to quickly tell the system if the AI helped me so the team can improve it.

**Acceptance Criteria**

* Each AI response has thumbs up/down feedback.
* Negative feedback asks for optional reason.
* Feedback is logged with job ID, screen, test type, and AI response ID.
* Admin/reporting view can export feedback.

**Dependencies**

* Logging framework
* Feedback database table
* Admin reporting or export

**Measurable Outcomes**

* Feedback captured on at least 20% of AI interactions during pilot
* Weekly improvement backlog generated from feedback

---

# 6. Phase 2: Workflow-Aware Agent

## Goal

Make the AI aware of the technician’s current job step, test status, and workflow context so it can provide better next-step guidance.

---

### Feature 2.1 — Job Context Awareness

**Description**
The agent understands basic job metadata such as job type, customer/site, required tests, completed tests, pending tests, current location, and selected test location.

**User Story**
As a technician, I want the AI to know what job I am working on so I do not have to explain the context every time.

**Acceptance Criteria**

* AI receives job metadata when opened from a job.
* AI knows completed, pending, and failed tests.
* AI can answer “What should I do next?”
* AI does not expose irrelevant or unavailable data.
* AI warns when required tests are incomplete.

**Dependencies**

* Job metadata API
* Required test rules
* Current workflow state
* Conversation context injection

**Measurable Outcomes**

* 25% reduction in incomplete job submissions
* Increased use of “What should I do next?” prompt
* Reduced incorrect workflow steps

---

### Feature 2.2 — Test State Awareness

**Description**
The agent knows whether a test is not started, running, completed, failed, cancelled, timed out, or uploaded.

**User Story**
As a technician, I want the AI to understand the current test status so it can guide me based on what is actually happening.

**Acceptance Criteria**

* AI receives current test status.
* AI can explain the current state.
* AI provides different guidance for running, failed, passed, and timed-out tests.
* AI does not recommend actions that could interrupt a running test.
* AI can tell the technician what to prepare next while the test runs.

**Dependencies**

* Test status API/event stream
* Test screen integration
* State-to-prompt mapping
* Safety rules for running tests

**Measurable Outcomes**

* Reduced test interruption issues
* Reduced technician idle time
* Higher AI engagement during test execution

---

### Feature 2.3 — Waiting-for-Test Assistant

**Description**
While a test is running, the agent uses wait time productively by explaining the test, showing what to prepare next, reminding the technician of quality checks, and warning against risky actions.

**User Story**
As a technician, I want useful guidance while I wait for a test to finish so I can prepare the next step instead of wasting time.

**Acceptance Criteria**

* When a test starts, the UI shows a “While you wait” assistant panel.
* AI explains what the test is doing.
* AI shows estimated wait time if available.
* AI reminds technician what to prepare next.
* AI warns not to disconnect, move, or interrupt equipment if applicable.
* AI provides troubleshooting guidance if the test runs longer than expected.
* AI can summarize job progress so far.

**Example AI Messages**

Running normally:

> “This OTDR test is checking the fiber path for loss, reflection, and possible breaks. While it runs, keep the connection stable and avoid disconnecting the fiber. Next, prepare to review event distance, loss, and pass/fail status.”

Preparing next step:

> “While this test runs, confirm the next required location is Ground Block. You have already completed TAP. After this result saves, run the remaining required test before closing the job.”

Taking too long:

> “This test is taking longer than expected. Do not disconnect yet. Check that the device still has signal, battery is stable, and the app has not lost connection. If it times out, rerun once before escalating.”

**Dependencies**

* Test status
* Expected duration by test type
* Job progress data
* Required test rules
* UI waiting screen

**Measurable Outcomes**

* 15% reduction in average idle time
* 20% reduction in incomplete test sequences
* Increased technician satisfaction during long tests

---

### Feature 2.4 — Basic Result Explanation

**Description**
After a test completes, the agent explains the result in plain English and identifies the next best action.

**User Story**
As a technician, I want the AI to explain the test result so I know whether I can proceed, rerun, troubleshoot, or escalate.

**Acceptance Criteria**

* AI can explain PASS, FAIL, warning, incomplete, and upload error states.
* AI identifies key result values if available.
* AI provides next best action.
* AI separates “what happened” from “what to do next.”
* AI avoids overriding deterministic backend pass/fail rules.

**Dependencies**

* Result parser
* Test result schema
* Threshold/profile rules
* Backend pass/fail output

**Measurable Outcomes**

* Reduced support calls for result interpretation
* Reduced incorrect reruns
* Reduced premature escalations

---

# 7. Phase 3: Troubleshooting Agent

## Goal

Help technicians diagnose and resolve failed or abnormal tests with structured troubleshooting flows.

---

### Feature 3.1 — Failure Troubleshooting Decision Trees

**Description**
For common failures, the AI guides technicians through step-by-step checks.

**User Story**
As a technician, I want the AI to walk me through troubleshooting when a test fails so I can fix the issue without calling support immediately.

**Acceptance Criteria**

* AI identifies failure type.
* AI starts with simple physical checks before advanced steps.
* AI asks one question at a time.
* AI tracks completed troubleshooting steps.
* AI recommends escalation after defined failure conditions.
* AI logs all troubleshooting steps for supervisor review.

**Example Flow**

Failure: Low optical power

1. Confirm fiber is fully seated.
2. Inspect/clean connector.
3. Confirm correct port/location.
4. Rerun test.
5. If still low, check upstream component or escalate.

**Dependencies**

* Failure code/result mapping
* Troubleshooting SOPs
* Step-tracking state
* Result history for current job

**Measurable Outcomes**

* 20% reduction in support calls for common failures
* 10% reduction in repeat truck rolls
* Increased first-time-right completion rate

---

### Feature 3.2 — OTDR Trace Guidance

**Description**
The AI helps explain common OTDR trace issues such as high loss, reflection, distance mismatch, macro-bend suspicion, end-of-fiber events, or abnormal events.

**User Story**
As a technician, I want help understanding abnormal OTDR results so I know what to inspect.

**Acceptance Criteria**

* AI can explain common OTDR event types.
* AI can identify likely technician actions based on trace summary.
* AI does not claim certainty if trace data is incomplete.
* AI can recommend inspection points based on event distance when available.
* AI can escalate with a structured trace summary.

**Dependencies**

* OTDR result parser
* Event table extraction
* OTDR knowledge base
* Distance/event metadata

**Measurable Outcomes**

* Reduced OTDR-related support escalations
* Improved technician confidence score
* Reduced incorrect interpretation of OTDR failures

---

### Feature 3.3 — Upload and Save Issue Assistant

**Description**
The AI guides technicians when result upload, save, GPS, network, or offline behavior fails.

**User Story**
As a technician, I want help when upload or save fails so I do not lose test results or close the job incorrectly.

**Acceptance Criteria**

* AI detects upload failure, offline mode, missing GPS, or save error.
* AI explains whether the result is saved locally or not.
* AI tells technician what not to do to avoid data loss.
* AI recommends retry, reconnect, save locally, or escalate.
* AI logs error state and device details.

**Dependencies**

* Upload status
* Local/offline queue status
* Network status
* GPS permission/status
* Error code mapping

**Measurable Outcomes**

* Reduced failed uploads
* Reduced lost result cases
* Reduced incorrect job closures

---

### Feature 3.4 — Escalation Summary Generator

**Description**
When a technician needs help, the AI generates a structured summary for supervisor/support.

**User Story**
As a technician, I want the AI to summarize the issue so I do not have to manually explain everything when escalating.

**Acceptance Criteria**

* Summary includes job ID, test type, location, result status, error codes, troubleshooting steps attempted, device status, and technician notes.
* Technician can review/edit before sending.
* Summary can be copied, attached, or submitted to support.
* AI does not include unsupported assumptions.

**Dependencies**

* Job metadata
* Test results
* Troubleshooting log
* Device/app logs
* Support/escalation channel

**Measurable Outcomes**

* Reduced escalation handling time
* Improved support team first-response quality
* Reduced back-and-forth between technician and support

---

# 8. Phase 4: Proactive Field Copilot

## Goal

Move from reactive assistance to proactive recommendations, personalized coaching, and operational intelligence.

---

### Feature 4.1 — Historical Pattern Comparison

**Description**
Compare current test issues with historical passed/failed patterns for similar job types, locations, device types, or failure categories.

**User Story**
As a supervisor, I want the system to identify recurring issue patterns so we can reduce repeated failures.

**Acceptance Criteria**

* System can compare current failure to similar historical failures.
* AI can say “similar past issues were usually caused by…”
* Confidence level is shown.
* AI does not present predictions as facts.
* Supervisors can view trend summaries.

**Dependencies**

* Historical result database
* Failure taxonomy
* Analytics layer
* Pattern detection model/rules

**Measurable Outcomes**

* Reduced repeat failures
* Improved QA insight
* Faster root-cause identification

---

### Feature 4.2 — Technician Coaching Mode

**Description**
The AI provides coaching based on repeated technician patterns, common mistakes, and missed steps.

**User Story**
As a technician, I want helpful coaching so I can avoid repeating mistakes and improve my workflow.

**Acceptance Criteria**

* Coaching is framed positively, not punitively.
* AI identifies repeated missed steps or common failure points.
* Coaching is based on actual workflow data.
* Supervisors can configure whether coaching is enabled.
* Coaching does not expose sensitive performance judgments directly without policy approval.

**Dependencies**

* Technician activity history
* QA policy
* Supervisor configuration
* Privacy/compliance review

**Measurable Outcomes**

* Reduced repeated technician errors
* Increased first-time-right completion
* Improved training effectiveness

---

### Feature 4.3 — Voice-First Field Assistant

**Description**
Enable hands-free interaction for technicians who are working in the field.

**User Story**
As a technician, I want to ask the AI questions by voice so I can keep working without typing.

**Acceptance Criteria**

* Technician can ask common workflow questions by voice.
* AI responses are short enough for audio playback.
* Voice mode supports confirmation for critical actions.
* App handles noisy environments gracefully.
* Voice logs are handled according to privacy policy.

**Dependencies**

* Speech-to-text
* Text-to-speech
* Mobile app voice UI
* Noise handling
* Privacy approval

**Measurable Outcomes**

* Increased AI usage during active field work
* Reduced typing burden
* Improved technician satisfaction

---

# 9. UX Requirements for Design

## Core UX Principles

1. **Minimal distraction**
2. **Short answers first**
3. **One next action at a time**
4. **Contextual, not generic**
5. **Technician-friendly language**
6. **Voice-ready**
7. **Escalation-ready**
8. **Clear uncertainty handling**

---

## Key Screens

### Screen 1 — AI Helper Chat

**Purpose**
General assistant for job, test, and troubleshooting questions.

**UI Elements**

* Chat input
* Voice button
* Suggested prompts
* Current job context chip
* Current test context chip
* Feedback buttons
* Escalate button

---

### Screen 2 — Test Waiting Assistant

**Purpose**
Appears while a test is running.

**UI Elements**

* Test progress/status
* Estimated wait time
* “What this test is doing”
* “What to prepare next”
* “Do not do this while test is running”
* Suggested questions
* Voice ask button

---

### Screen 3 — Result Explanation Panel

**Purpose**
Explains test result after completion.

**UI Elements**

* Plain-English result summary
* Key values
* Pass/fail reason
* Next recommended action
* Rerun guidance if applicable
* Troubleshoot button
* Escalate button

---

### Screen 4 — Troubleshooting Wizard

**Purpose**
Step-by-step issue resolution.

**UI Elements**

* Failure summary
* Step-by-step checks
* Yes/no technician inputs
* Rerun test button
* Escalation summary button
* Progress tracker

---

### Screen 5 — Escalation Summary Review

**Purpose**
Allow technician to send a clean summary to support/supervisor.

**UI Elements**

* Auto-generated issue summary
* Job/test metadata
* Steps attempted
* Result details
* Technician notes
* Submit/copy/share action

---

# 10. Engineering Architecture

## Recommended Components

| Component              | Responsibility                                               |
| ---------------------- | ------------------------------------------------------------ |
| LLM layer              | Natural language response generation                         |
| RAG knowledge layer    | Retrieve approved documentation and SOPs                     |
| Workflow state engine  | Track job step, required tests, completed tests, next step   |
| Test state integration | Know if test is running, passed, failed, timed out, uploaded |
| Result parser          | Extract useful values from test result files                 |
| Rules engine           | Handle safety, compliance, thresholds, required-test logic   |
| Conversation memory    | Remember context within the current job/session              |
| Offline fallback       | Provide cached guidance when network is unavailable          |
| Logging/analytics      | Track usage, feedback, errors, outcomes                      |
| Escalation service     | Generate and send structured support summaries               |

---

## AI vs Rules vs Backend Logic

| Area                           | Should Be Handled By             |
| ------------------------------ | -------------------------------- |
| Conversational explanation     | AI                               |
| Pass/fail determination        | Backend/rules                    |
| Safety/compliance instructions | Rules + approved knowledge       |
| Required test completion       | Backend/rules                    |
| Suggested next action          | Rules + AI explanation           |
| Result interpretation summary  | Parser + AI                      |
| Troubleshooting flow           | Rules/tree + AI wording          |
| Escalation summary             | Backend data + AI formatting     |
| Historical pattern detection   | Analytics/model + AI explanation |

---

# 11. Data Dependencies

## Required for MVP

| Data Source             | Needed For               |
| ----------------------- | ------------------------ |
| Fiber installation SOPs | Grounded Q&A             |
| Test procedure docs     | Test explanation         |
| Device manuals          | Device-specific guidance |
| Error codes             | Troubleshooting          |
| Job metadata            | Context-aware answers    |
| Test status             | Waiting assistant        |
| Test result status      | Result explanation       |
| Required test rules     | Next-step guidance       |
| Upload status           | Save/upload support      |
| Feedback logs           | Product improvement      |

## Required Later

| Data Source             | Needed For             |
| ----------------------- | ---------------------- |
| Historical test results | Pattern detection      |
| Technician history      | Coaching               |
| QA review results       | Model improvement      |
| Supervisor notes        | Escalation improvement |
| Regional/site patterns  | Predictive guidance    |

---

# 12. Edge Cases and Required Behavior

| Edge Case                       | Detection Signal                      | AI Response                                               | Escalation Path                    | Logs to Capture                  |
| ------------------------------- | ------------------------------------- | --------------------------------------------------------- | ---------------------------------- | -------------------------------- |
| Test takes too long             | Running longer than expected duration | Tell tech not to disconnect; suggest basic checks         | Escalate after timeout/retry       | Test ID, duration, device status |
| Test fails                      | FAIL result                           | Explain likely cause and start troubleshooting            | Supervisor/support after checklist | Result file, thresholds, steps   |
| Test passes but tech sees issue | PASS + technician concern             | Validate concern and suggest physical checks              | Escalate if mismatch persists      | Tech note, photos if available   |
| Missing data                    | Empty/incomplete result fields        | State data is incomplete; recommend rerun or upload check | Support if repeated                | Result payload, error code       |
| Device offline                  | Network unavailable                   | Explain offline behavior and save guidance                | Support if result not queued       | Network status, queue status     |
| Upload fails                    | Upload error                          | Explain retry/local save steps                            | Support if repeated                | Upload error, file path/status   |
| GPS unavailable                 | Permission/signal missing             | Ask tech to enable/check location or continue per policy  | Supervisor if required             | GPS status, timestamp            |
| Wrong job selected              | Job/test mismatch                     | Warn tech before saving/uploading                         | Supervisor if already saved        | Job ID, selected job, result ID  |
| Wrong test location             | Location mismatch                     | Ask tech to confirm location before save                  | Supervisor/QA if saved             | Selected location, GPS, result   |
| OTDR abnormal trace             | Event/loss/reflection flag            | Explain likely inspection points                          | Support if unresolved              | Trace summary, event table       |
| Low battery                     | Battery threshold                     | Tell tech to charge before continuing critical test       | N/A unless job blocked             | Battery level                    |
| App crash/freeze                | App restart/error                     | Explain recovery and check saved queue                    | Support if result lost             | Crash log, job/test state        |
| AI unsure                       | Low confidence/no source              | Say unsure and suggest escalation                         | Support/supervisor                 | Question, retrieved docs         |

---

# 13. Success Metrics

## Technician Productivity

| KPI                               | Target        |
| --------------------------------- | ------------- |
| Average job completion time       | Reduce 10–15% |
| Time spent waiting without action | Reduce 15–20% |
| Support calls per job             | Reduce 20–30% |
| Escalation time                   | Reduce 20%    |

## Job Quality

| KPI                                 | Target        |
| ----------------------------------- | ------------- |
| First-time-right completion         | Increase 10%  |
| Incomplete required tests           | Reduce 20%    |
| Failed uploads                      | Reduce 25%    |
| Repeat truck rolls                  | Reduce 10–15% |
| Incorrect test location submissions | Reduce 15–20% |

## AI Adoption

| KPI                                   | Target                  |
| ------------------------------------- | ----------------------- |
| AI usage per job                      | 50%+ in pilot group     |
| Suggested prompt usage                | 40%+ of AI interactions |
| Technician helpful rating             | 70%+ positive           |
| Negative feedback due to wrong answer | Under 5–8% after tuning |

---

# 14. 30/60/90-Day Execution Plan

## First 30 Days — Foundation MVP

### Build

* Knowledge-grounded AI Q&A
* Basic chat UI
* Suggested prompts
* Basic test explanations
* Feedback capture
* Initial AI safety rules

### Design Deliverables

* Chat UI
* Suggested prompt patterns
* Response style guide
* Feedback controls

### Engineering Deliverables

* RAG pipeline
* Knowledge ingestion
* Chat API
* Logging table
* Feedback API
* Basic app integration

### Leadership Outcome

* Demonstrable AI assistant prototype
* Pilot-ready with limited technician workflow support

---

## Days 31–60 — Workflow Awareness

### Build

* Job context injection
* Test state awareness
* Waiting-for-test assistant
* “What should I do next?” guidance
* Basic result explanation

### Design Deliverables

* Test waiting assistant screen
* Result explanation panel
* Context chips
* Next-step recommendation UI

### Engineering Deliverables

* Job metadata API integration
* Test status integration
* Required test rules integration
* Result status parser
* Context management layer

### Leadership Outcome

* Agent becomes meaningfully useful during live jobs
* Clear reduction in idle time and incomplete steps

---

## Days 61–90 — Troubleshooting and Escalation

### Build

* Failure troubleshooting flows
* OTDR/power/RF issue guidance
* Upload/save issue assistant
* Escalation summary generator
* Supervisor/support handoff package

### Design Deliverables

* Troubleshooting wizard
* Escalation summary review screen
* Failure result UI patterns

### Engineering Deliverables

* Failure mapping
* Troubleshooting decision trees
* Result parser expansion
* Escalation summary generator
* Support handoff integration

### Leadership Outcome

* AI starts reducing support load and repeat troubleshooting effort
* Pilot can expand to more technicians or customers

---

# 15. Prioritized Feature Backlog

| Priority | Feature                  | Description                              | Effort | Owner              |
| -------- | ------------------------ | ---------------------------------------- | ------ | ------------------ |
| P0       | Knowledge-grounded Q&A   | AI answers from approved docs            | Medium | AI/Backend         |
| P0       | Suggested prompts        | Contextual prompts by screen             | Low    | Design/Frontend    |
| P0       | Feedback capture         | Rate responses and flag issues           | Low    | Frontend/Backend   |
| P0       | Basic test explanation   | Explain test purpose and expected result | Medium | AI/Product         |
| P1       | Job context awareness    | AI knows job and required tests          | Medium | Backend            |
| P1       | Test state awareness     | AI knows running/completed/failed status | Medium | Backend/Frontend   |
| P1       | Waiting assistant        | Guidance while test is running           | Medium | Design/Frontend/AI |
| P1       | Basic result explanation | Explain pass/fail in plain English       | Medium | Backend/AI         |
| P2       | Troubleshooting flows    | Step-by-step failure guidance            | High   | Product/Backend/AI |
| P2       | Upload/save assistant    | Handle offline/upload/GPS issues         | Medium | Mobile/Backend     |
| P2       | Escalation summary       | Auto-generate support handoff            | Medium | Backend/AI         |
| P3       | Voice assistant          | Hands-free usage                         | High   | Mobile/AI          |
| P3       | Historical comparison    | Compare against past failures            | High   | Data/AI            |
| P3       | Technician coaching      | Personalized improvement suggestions     | High   | Data/Product       |

---

# 16. Final Recommendation

## Build These First

1. **Knowledge-grounded Q&A**
2. **Workflow-specific suggested prompts**
3. **Test waiting assistant**
4. **Basic result explanation**
5. **Escalation summary generator**

## Top 5 Data Integrations Needed

1. Job metadata
2. Test status
3. Test result status/details
4. Required test rules
5. Upload/offline queue status

## Best Pilot Strategy

Start with a controlled pilot group of technicians using 2–3 common workflows:

* Standard fiber install
* OTDR test workflow
* Upload/save/result review workflow

Measure:

* AI usage
* Technician feedback
* Reduced support calls
* Reduced incomplete tests
* Reduced failed uploads
* Job completion time

The strongest MVP is not “AI that answers everything.” It is an AI helper that always knows: **what job the technician is on, what step they are in, what test is running, what happened, and what the technician should do next.**
