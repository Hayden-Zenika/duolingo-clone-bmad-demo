# Epics and Stories

**Project:** Duolingo Clone (SEA Focus)
**Date:** 2025-12-01
**Status:** DRAFT

---

## 1. Workflow Context

**Mode:** CREATE
**Context Loaded:**
- ✅ PRD (Required)
- ✅ Architecture (Technical decisions incorporated)
- ❌ UX Design (Not found - using standard patterns)

---

## 2. Functional Requirements Inventory

| ID | Requirement |
|---|---|
| **FR1** | Users can sign up/login using Email, Google, or Facebook. |
| **FR2** | Users can onboard by selecting a source language and a target language. |
| **FR3** | Users can take a placement test to skip beginner levels. |
| **FR4** | Users can manage their profile (avatar, display name, daily goal). |
| **FR5** | Users can view a linear learning path (Unit -> Chapter -> Lesson). |
| **FR6** | Users can complete interactive lessons with mixed question types (Translation, Listening, Matching, Speaking). |
| **FR7** | Users receive immediate feedback on every answer. |
| **FR8** | Users can listen to audio pronunciation of words and sentences. |
| **FR9** | Users can use the microphone to record speech for pronunciation assessment. |
| **FR10** | Users can enter a "Roleplay" mode to chat with an AI character. |
| **FR11** | AI characters simulate specific personas (e.g., "Market Vendor," "Taxi Driver"). |
| **FR12** | Users can see a transcript of the conversation. |
| **FR13** | Users receive AI-generated suggestions for better phrasing after the conversation. |
| **FR14** | Users earn XP (Experience Points) for completing lessons. |
| **FR15** | Users maintain a "Streak" by completing at least one lesson daily. |
| **FR16** | Users have a limited number of "Hearts" (lives) that deplete with wrong answers. |
| **FR17** | Users can view their position on a weekly Leaderboard. |
| **FR18** | Users earn badges/achievements for milestones. |
| **FR19** | Users can view a virtual shop. |
| **FR20** | Users can spend virtual currency (Gems) on items like "Streak Freeze" or "Heart Refill." |
| **FR21** | Users can watch video ads to regain Hearts (Freemium). |
| **FR22** | Admins (Experts) can create and edit course structures (Units, Lessons). |
| **FR23** | Admins can define "Golden Path" scripts for AI roleplays. |
| **FR24** | Admins can review flagged AI interactions for quality control. |

---

## 3. Epic Structure & Coverage

### Epic 1: Foundation & User Onboarding
**Goal:** Establish the technical foundation and enable users to create accounts and personalize their learning journey.
**FR Coverage:** FR1, FR2, FR4
**Value:** Users can access the platform and set their initial preferences.

### Epic 2: Core Learning Engine
**Goal:** Deliver the primary value proposition - interactive language lessons with immediate feedback.
**FR Coverage:** FR5, FR6, FR7, FR8, FR9
**Value:** Users can learn new language concepts through interactive exercises.

### Epic 3: Gamification & Progress
**Goal:** Drive retention and engagement through proven gamification mechanics.
**FR Coverage:** FR14, FR15, FR16, FR17, FR18
**Value:** Users are motivated to return daily and track their progress.

### Epic 4: AI Speaking Companion
**Goal:** Provide a safe, realistic environment for speaking practice with expert guardrails.
**FR Coverage:** FR10, FR11, FR12, FR13
**Value:** Users gain confidence in speaking without fear of judgment.

### Epic 5: Monetization & Shop
**Goal:** Implement the freemium economy to sustain the platform.
**FR Coverage:** FR19, FR20, FR21
**Value:** Users can manage their virtual resources and access premium options.

### Epic 6: Content Management System
**Goal:** Empower language experts to create and manage high-quality content.
**FR Coverage:** FR3, FR22, FR23, FR24
**Value:** Experts can maintain pedagogical quality and safety.

---

## 4. Detailed Epic Breakdown

### Epic 1: Foundation & User Onboarding (DC-1)
**Goal:** Establish the technical foundation and enable users to create accounts and personalize their learning journey.

#### Story 1.1: Project Setup & Infrastructure (DC-2)
**User Story:** As a developer, I want the project structure, database connection, and core dependencies set up so that I can start building features.
**Acceptance Criteria:**
- [x] Next.js 14+ (App Router) project initialized with TypeScript.
- [x] Tailwind CSS and Shadcn UI configured with project theme colors.
- [x] PostgreSQL database (Neon) connected via Drizzle ORM.
- [x] Clerk authentication provider configured and wrapped around the app.
- [x] PWA manifest and service worker (Serwist) basic setup for offline capability.
- [x] Folder structure matches Architecture guidelines (`actions`, `app`, `components`, `db`, `lib`).
**Technical Notes:**
- Follow "Project Initialization" in Architecture.md.
- Ensure strict linting (ESLint) and formatting (Prettier) are active.

#### Story 1.2: User Authentication (FR1) (DC-3)
**User Story:** As a user, I want to sign up or log in using my email or social accounts so that I can access the app and save my progress.
**Acceptance Criteria:**
- [x] Sign-up page available at `/sign-up` with Email, Google, and Facebook options.
- [x] Log-in page available at `/sign-in` with same options.
- [x] Successful auth redirects to `/learn` (or onboarding if new).
- [x] Protected routes (e.g., `/learn`, `/profile`) redirect unauthenticated users to `/sign-in`.
- [x] Auth state persists across sessions and page reloads.
**Technical Notes:**
- Use Clerk's `<SignUp />` and `<SignIn />` components.
- Customize Clerk appearance to match "Playful" design system.

#### Story 1.3: Onboarding & Language Selection (FR2) (DC-4)
**User Story:** As a new user, I want to select my source and target languages so that I am placed in the correct course.
**Acceptance Criteria:**
- [x] Onboarding screen presents "I speak..." (Source) and "I want to learn..." (Target) options.
- [x] Supported pairs: Vietnamese -> English, Indonesian -> English, English -> Vietnamese.
- [x] Selection creates a `user_progress` record linking user to the specific `course`.
- [x] User is prompted to "Start from scratch" or "Find my level" (Placement Test placeholder).
**Technical Notes:**
- Check `db/schema.ts` for `courses` and `user_progress` relations.
- Default to "Start from scratch" flow for this story (Placement Test is Epic 6).

#### Story 1.4: Profile Management (FR4) (DC-5)
**User Story:** As a user, I want to customize my profile and set goals so that I feel personal ownership of my learning journey.
**Acceptance Criteria:**
- [ ] Profile page displays current avatar, display name, and join date.
- [ ] "Edit Profile" modal allows changing display name and avatar (select from presets).
- [ ] User can set a "Daily Goal" (e.g., 10 XP, 20 XP, 50 XP).
- [ ] Changes are saved to the database and reflected immediately in the UI.
**Technical Notes:**
- Avatar presets can be static assets in `public/avatars`.
- Daily goal is stored in `user_progress`.

#### Story 1.5: Placement Test (FR3) (DC-6)
**User Story:** As a user with prior knowledge, I want to take a test to skip beginner content so that I don't get bored.
**Acceptance Criteria:**
- [ ] "Find my level" option in onboarding flow.
- [ ] Presents a shortened lesson (10 mixed challenges).
- [ ] If score > 80%, unlock Unit 1 and Unit 2, and mark lessons as completed.
- [ ] If score < 80%, recommend starting from Unit 1.
**Technical Notes:**
- Reuse `Lesson Runner` component but with a special `isPlacement` flag.
- Logic to batch insert `challenge_progress` for skipped lessons.

---

### Epic 2: Core Learning Engine (DC-7)
**Goal:** Deliver the primary value proposition - interactive language lessons with immediate feedback.

#### Story 2.1: Course Structure Visualization (FR5) (DC-8)
**User Story:** As a user, I want to see a clear path of units and lessons so that I know what to learn next and can track my progress.
**Acceptance Criteria:**
- [x] "Learn" page displays a scrollable list of Units.
- [x] Each Unit contains a header (Title, Description) and a list of Lesson nodes.
- [x] Lesson nodes show status: Completed (Gold), Active (Color), Locked (Gray).
- [x] Clicking the Active lesson node navigates to the Lesson Runner.
- [x] Clicking Locked nodes shows a "Complete previous lessons to unlock" tooltip.
**Technical Notes:**
- Fetch hierarchy: `Course` -> `Units` -> `Lessons`.
- Use `user_progress` to determine current active lesson.

#### Story 2.2: Lesson Runner UI Shell (FR6) (DC-9)
**User Story:** As a user, I want a distraction-free interface for taking lessons so that I can focus on learning.
**Acceptance Criteria:**
- [x] Full-screen layout (no sidebar/footer).
- [x] Header: Exit button (X) and Progress Bar (0% to 100%).
- [x] Footer: "Check" button (initially disabled until answer provided).
- [x] Exit button triggers a confirmation modal ("Quit? You'll lose progress").
- [x] Answering correctly advances progress bar.
**Technical Notes:**
- State management: `useLesson` store (Zustand) to track current question index and answers.

#### Story 2.3: Translation Challenge (FR6) (DC-10)
**User Story:** As a user, I want to translate sentences between languages so that I can practice grammar and vocabulary.
**Acceptance Criteria:**
- [x] Display prompt sentence in Source or Target language.
- [x] "Word Bank" mode: User taps word bubbles to form the sentence.
- [x] Selected words move to the answer area.
- [x] User can remove words from answer area back to bank.
- [x] "Check" button validates the order of words.
**Technical Notes:**
- Challenge type: `SELECT`.
- Data: `challenge` table with `type="SELECT"`.

#### Story 2.4: Listening Challenge (FR6, FR8) (DC-11)
**User Story:** As a user, I want to listen to a sentence and transcribe it so that I can improve my listening comprehension.
**Acceptance Criteria:**
- [ ] Display "Audio" button (large speaker icon).
- [ ] Clicking plays the sentence audio (TTS).
- [ ] User selects words from a bank to transcribe what they heard.
- [ ] "Turtle" button plays audio at 0.75x speed.
**Technical Notes:**
- Use `lib/audio/tts.ts` (Architecture decision).
- Fallback to Web Speech API if cloud TTS fails/offline.

#### Story 2.5: Speaking Challenge (FR6, FR8) (DC-12)
**User Story:** As a user, I want to speak a sentence into the microphone so that I can practice pronunciation.
**Acceptance Criteria:**
- [ ] Display the sentence to be spoken.
- [ ] "Microphone" button to start recording.
- [ ] Visual feedback (waveform or color change) while recording.
- [ ] Simple validation (mock or basic Web Speech API) to verify input.
**Technical Notes:**
- Use `lib/audio/stt.ts` (Web Speech API) for client-side speech-to-text.
- Fuzzy string matching (Levenshtein distance) to allow minor errors.

#### Story 2.6: Immediate Feedback System (FR7) (DC-13)
**User Story:** As a user, I want to know immediately if I was right or wrong so that I can learn from my mistakes.
**Acceptance Criteria:**
- [x] Correct Answer: Green bottom sheet slides up. "Nice job!" text. "Continue" button. Play "Correct" sound.
- [x] Incorrect Answer: Red bottom sheet slides up. "Correct solution: [Answer]" text. "Continue" button. Play "Wrong" sound.
- [x] "Continue" moves to the next challenge.
**Technical Notes:**
- Audio files in `public/sounds`.
- Haptic feedback on mobile (if supported).

#### Story 2.7: Offline Lesson Support (NFR4) (DC-14)
**User Story:** As a user, I want to complete my next lesson even if I lose internet connection so that I can learn on the go.
**Acceptance Criteria:**
- [ ] Service Worker caches the *active* lesson's data and assets (audio/images) when the user is on the Learn page.
- [ ] User can start and complete the lesson while offline.
- [ ] Lesson completion result is queued and synced when connection is restored.
**Technical Notes:**
- Use Serwist for SW generation.
- Use TanStack Query `persistQueryClient` for mutation queue.

---

### Epic 3: Gamification & Progress (DC-15)
**Goal:** Drive retention and engagement through proven gamification mechanics.

#### Story 3.1: XP System & Daily Goal (FR14) (DC-16)
**User Story:** As a user, I want to earn XP for my efforts and track it against a daily goal so that I feel a sense of accomplishment.
**Acceptance Criteria:**
- [x] Award 10 XP for completing a standard lesson.
- [x] Award 5 XP bonus for a "Perfect Lesson" (no mistakes).
- [x] Display XP animation at the end of a lesson.
- [ ] Daily Goal widget shows progress ring (e.g., 10/20 XP).
- [ ] "Goal Met" notification when target reached.
**Technical Notes:**
- Update `points` in `user_progress`.

#### Story 3.2: Streak System (FR15) (DC-17)
**User Story:** As a user, I want to maintain a daily streak so that I am motivated to build a consistent learning habit.
**Acceptance Criteria:**
- [x] Completing at least one lesson in a day (local time) increments the streak counter.
- [x] Missing a day resets the streak to 0 (unless a Streak Freeze is active).
- [x] Flame icon in the header displays the current streak count.
- [ ] "Streak Extended!" full-screen animation upon first lesson completion of the day.
**Technical Notes:**
- Logic to check `last_active_date` vs `current_date`.
- Handle timezone differences (store UTC, calculate local day).

#### Story 3.3: Hearts System (FR16) (DC-18)
**User Story:** As a user, I want to have a limited number of "lives" so that I am encouraged to answer carefully.
**Acceptance Criteria:**
- [x] User starts with max 5 Hearts.
- [x] Answering incorrectly deducts 1 Heart.
- [x] If Hearts reach 0, the lesson is paused/failed. User is prompted to "Practice to earn hearts" or "Buy refill".
- [x] Hearts regenerate automatically (1 heart every 4 hours).
- [ ] Timer for next heart displayed in the Hearts modal.
**Technical Notes:**
- Store `hearts` (int) and `last_heart_refill` (timestamp) in `user_progress`.

#### Story 3.4: Leaderboard (FR17) (DC-19)
**User Story:** As a user, I want to see how I rank against other learners so that I feel a sense of competition.
**Acceptance Criteria:**
- [x] Leaderboard page displays a list of users ranked by "XP earned this week".
- [x] Resets every Sunday at midnight.
- [x] Top 3 users get Gold, Silver, Bronze styling.
- [x] Current user's row is highlighted.
- [x] Infinite scroll or pagination for top 50 users.
**Technical Notes:**
- DB query: Sum XP from `user_progress` (or separate `xp_history` table) filtered by current week range.

#### Story 3.5: Quests & Achievements (FR18) (DC-20)
**User Story:** As a user, I want to complete daily challenges so that I have clear short-term objectives.
**Acceptance Criteria:**
- [x] Display 3 Daily Quests (e.g., "Earn 20 XP", "Complete 1 Lesson", "Score 90% accuracy").
- [x] Progress updates in real-time.
- [ ] User can "Claim" a reward (Gems/XP) when a quest is completed.
- [x] "Quests" widget in the sidebar/feed.
**Technical Notes:**
- `quests` table defines types. `user_quests` tracks daily progress.

---

### Epic 4: AI Speaking Companion (DC-21)
**Goal:** Provide a safe, realistic environment for speaking practice with expert guardrails.

#### Story 4.1: AI Chat Interface (FR10) (DC-22)
**User Story:** As a user, I want a familiar chat interface to interact with the AI character so that I can focus on the conversation.
**Acceptance Criteria:**
- [ ] Chat UI with message bubbles (User right, AI left).
- [ ] Avatar for the AI character displayed next to their messages.
- [ ] Typing indicator ("...") while AI is generating response.
- [ ] Auto-scroll to bottom on new message.
**Technical Notes:**
- Use Vercel AI SDK `useChat` hook for streaming responses.

#### Story 4.2: Scenario Selection (FR11) (DC-23)
**User Story:** As a user, I want to choose a specific real-world scenario so that I can practice relevant vocabulary.
**Acceptance Criteria:**
- [ ] "Speak" tab displays a grid of available scenarios (e.g., "Ordering Coffee", "Taxi Ride").
- [ ] Each card shows: Title, Difficulty (A1/A2), and Persona (e.g., "Barista").
- [ ] Locked scenarios require a certain XP level or previous completion.
**Technical Notes:**
- `scenarios` table in DB.

#### Story 4.3: Voice Interaction (FR10) (DC-24)
**User Story:** As a user, I want to speak to the AI and hear it speak back so that it feels like a real conversation.
**Acceptance Criteria:**
- [ ] "Hold to Speak" button (or toggle mic).
- [ ] Speech-to-Text (STT) converts user audio to text input.
- [ ] AI response is streamed as text first, then audio (TTS) plays automatically.
- [ ] Audio visualizer animates during playback.
**Technical Notes:**
- Hybrid approach: Web Speech API for STT (low latency), OpenAI/ElevenLabs for TTS (high quality).

#### Story 4.4: Transcript & History (FR12) (DC-25)
**User Story:** As a user, I want to see the written transcript of the conversation so that I can review what was said.
**Acceptance Criteria:**
- [ ] Full text transcript is visible during the chat.
- [ ] User can tap a speaker icon on any message to replay the audio.
- [ ] Conversation history is saved to `ai_conversations` table.

#### Story 4.5: AI Feedback & Suggestions (FR13) (DC-26)
**User Story:** As a user, I want suggestions on how to improve my phrasing so that I can learn natural expressions.
**Acceptance Criteria:**
- [ ] "Magic Wand" icon appears next to user's messages.
- [ ] Clicking it expands a "Better way to say this" tip.
- [ ] Tip provides a more natural or grammatically correct version of the user's input.
**Technical Notes:**
- Can be a separate lightweight LLM call or part of the main response metadata.

#### Story 4.6: Golden Path Guardrails (FR23) (DC-27)
**User Story:** As a learner, I want the AI to guide me towards the learning goal so that the conversation remains productive.
**Acceptance Criteria:**
- [ ] AI System Prompt is dynamically updated based on the current "Stage" of the conversation (e.g., Stage 1: Greeting, Stage 2: Ordering).
- [ ] If user deviates, AI gently nudges them back ("That's interesting, but what would you like to order?").
- [ ] Conversation ends successfully when all stages are completed.
**Technical Notes:**
- Implement `StageManager` state machine as defined in Architecture.

---

### Epic 5: Monetization & Shop (DC-28)
**Goal:** Implement the freemium economy to sustain the platform.

#### Story 5.1: Shop Interface (FR19) (DC-29)
**User Story:** As a user, I want to browse a shop so that I can see what I can buy with my earned currency.
**Acceptance Criteria:**
- [x] Shop page accessible from sidebar.
- [x] Display user's current Gem balance.
- [ ] List items in categories: "Power-ups", "Cosmetics" (future).
- [x] Items show Icon, Name, Description, and Price.
- [x] "Buy" button (disabled if insufficient funds).

#### Story 5.2: Gem System (FR20) (DC-30)
**User Story:** As a user, I want to earn and spend virtual currency so that I can access premium features.
**Acceptance Criteria:**
- [x] Database field `gems` in `user_progress`.
- [x] Backend action to `spendGems(userId, amount)`.
- [x] Backend action to `earnGems(userId, amount)`.
- [x] UI updates immediately upon transaction.

#### Story 5.3: Power-up - Streak Freeze (FR20) (DC-31)
**User Story:** As a user, I want to buy a Streak Freeze so that I don't lose my progress if I miss a day.
**Acceptance Criteria:**
- [ ] Item: "Streak Freeze". Price: 200 Gems.
- [ ] User can hold max 2 freezes.
- [ ] If user misses a day (streak logic), check for freeze.
- [ ] If freeze exists: Consume 1 freeze, maintain streak, notify user ("Streak Freeze used!").
- [ ] If no freeze: Reset streak.

#### Story 5.4: Power-up - Heart Refill (FR20) (DC-32)
**User Story:** As a user, I want to refill my hearts instantly so that I can continue learning without waiting.
**Acceptance Criteria:**
- [ ] Item: "Refill Hearts". Price: 350 Gems.
- [ ] Only available if hearts < 5.
- [ ] Purchase restores hearts to 5 immediately.

#### Story 5.5: Ad Integration (FR21) (DC-33)
**User Story:** As a free user, I want to watch an ad to regain a heart so that I can keep playing without spending gems.
**Acceptance Criteria:**
- [ ] In the "Out of Hearts" modal, show "Watch Video (+1 Heart)" button.
- [ ] Clicking triggers video ad player (Mock component for MVP).
- [ ] Upon completion of video, award +1 Heart.
- [ ] Rate limit: Max 3 ads per hour.

---

### Epic 6: Content Management System (DC-34)
**Goal:** Empower language experts to create and manage high-quality content.

#### Story 6.1: Admin Dashboard & Auth (FR22) (DC-35)
**User Story:** As an admin, I want a secure dashboard so that I can access content management tools.
**Acceptance Criteria:**
- [x] Route `/admin` is protected.
- [x] Only users with `role: admin` in metadata can access.
- [ ] Sidebar navigation: Courses, Units, Lessons, Challenges, Scenarios.
- [x] Use `react-admin` or similar for rapid CRUD UI generation (optional, or custom build).

#### Story 6.2: Course & Unit Management (FR22) (DC-36)
**User Story:** As an admin, I want to structure the curriculum so that learners have a logical path.
**Acceptance Criteria:**
- [x] CRUD interface for `courses` table (Title, Image, Source/Target Lang).
- [x] CRUD interface for `units` table (Title, Description, Order).
- [x] Ability to reorder units via drag-and-drop or input field.

#### Story 6.3: Lesson & Challenge Editor (FR22) (DC-37)
**User Story:** As an admin, I want to create interactive exercises so that the lessons have content.
**Acceptance Criteria:**
- [x] CRUD interface for `lessons` (Title, Order, Unit ID).
- [x] CRUD interface for `challenges` (Question, Type, Lesson ID).
- [x] CRUD interface for `challenge_options` (Text, Correct Boolean, Audio URL, Image URL).
- [x] Preview mode to see how the challenge looks to users.

#### Story 6.4: AI Scenario Builder (FR23) (DC-38)
**User Story:** As an admin, I want to define the "Golden Path" for AI conversations so that they are pedagogically sound.
**Acceptance Criteria:**
- [ ] Interface to create `scenarios` (Title, Difficulty, Persona).
- [ ] "Graph Builder" UI (or JSON editor) to define the conversation stages.
- [ ] For each stage: Define `system_prompt_additions` and `transition_criteria`.
- [ ] Save to `conversation_graph` structure in DB.

#### Story 6.5: AI Quality Review (FR24) (DC-39)
**User Story:** As an admin, I want to review flagged conversations so that I can ensure the AI is behaving correctly.
**Acceptance Criteria:**
- [ ] List view of `ai_conversations` where `flagged=true`.
- [ ] View full transcript.
- [ ] Action buttons: "Dismiss" (False positive) or "Mark Unsafe".
- [ ] "Mark Unsafe" allows adding notes for prompt engineering improvements.

---

## 5. FR Coverage Matrix

| FR ID | Requirement | Covered By |
|---|---|---|
| FR1 | Sign up/Login | Story 1.2 |
| FR2 | Onboarding/Lang Selection | Story 1.3 |
| FR3 | Placement Test | Story 1.5 |
| FR4 | Profile Management | Story 1.4 |
| FR5 | Learning Path | Story 2.1 |
| FR6 | Interactive Lessons | Story 2.2, 2.3, 2.4, 2.5 |
| FR7 | Immediate Feedback | Story 2.6 |
| FR8 | Audio Pronunciation | Story 2.4 |
| FR9 | Microphone Input | Story 2.5 |
| FR10 | AI Roleplay Mode | Story 4.1, 4.3 |
| FR11 | AI Personas | Story 4.2 |
| FR12 | Conversation Transcript | Story 4.4 |
| FR13 | AI Suggestions | Story 4.5 |
| FR14 | XP System | Story 3.1 |
| FR15 | Streak System | Story 3.2 |
| FR16 | Hearts System | Story 3.3 |
| FR17 | Leaderboard | Story 3.4 |
| FR18 | Badges/Achievements | Story 3.5 |
| FR19 | Virtual Shop | Story 5.1 |
| FR20 | Virtual Currency (Gems) | Story 5.2, 5.3, 5.4 |
| FR21 | Video Ads | Story 5.5 |
| FR22 | Admin Course Mgmt | Story 6.1, 6.2, 6.3 |
| FR23 | Golden Path Scripts | Story 6.4, 4.6 |
| FR24 | AI Quality Review | Story 6.5 |

---
