# duolingo-clone - Product Requirements Document

**Author:** Hayden
**Date:** 2025-12-01
**Version:** 1.1

---

## Executive Summary

**Duolingo Clone (SEA Focus)** is a gamified, mobile-first language learning platform tailored specifically for the Southeast Asian market. Unlike generic global competitors, it combines proven gamification mechanics with hyper-localized content and an **AI-first approach guided by human experts**.

### What Makes This Special

The "Special Sauce" is the **User-Tailored AI-First Approach**:
1.  **AI Speaking Companion:** Solves the region's #1 pain point—speaking confidence—by simulating culturally relevant scenarios (e.g., "Talking to a Grab driver," "Ordering street food in Bangkok").
2.  **Expert-Aligned AI:** Language experts create key content anchors and moderate AI interactions to ensure pedagogical accuracy and cultural safety, preventing the "hallucinations" common in pure-AI tutors.
3.  **Hyper-Localization:** Content is not just translated but culturally adapted for SEA users learning English (and vice versa), bridging the gap between textbook learning and real-world usage.

---

## Project Classification

**Technical Type:** Web Application (PWA)
**Domain:** EdTech
**Complexity:** Medium

**Classification Notes:**
*   **Mobile-First PWA:** Chosen to address the high Android market share and data-conscious user base in SEA, allowing for offline capabilities without the friction of app store downloads.
*   **EdTech Domain:** Requires adherence to learning standards (CEFR alignment) and strict content moderation.
*   **AI-Integrated:** High complexity in the AI/LLM integration layer for the speaking companion.

### Domain Context

As an EdTech product in the SEA market, we must address:
*   **Connectivity:** Users often have spotty data; offline-first architecture is critical.
*   **Device Diversity:** Must perform well on low-end Android devices.
*   **Cultural Sensitivity:** Content must respect local customs and norms across diverse SEA countries (Indonesia, Vietnam, Thailand, etc.).

---

## Success Criteria

### User Success
*   **Speaking Confidence:** Users report reduced anxiety when speaking the target language in real-world situations.
*   **Habit Formation:** Users maintain a 7-day streak within their first month.
*   **Tangible Progress:** Users can pass "Checkpoint" assessments that correlate to real-world CEFR levels (A1/A2).

### Business Metrics
*   **Adoption:** Acquire 100,000 MAU within the first 12 months in Tier 1 markets (Indonesia, Vietnam).
*   **Retention:** Day-30 retention rate of >15% (industry standard for top apps).
*   **Monetization:** Conversion rate of 2% to paid micro-transactions or subscriptions.

---

## Product Scope

### MVP - Minimum Viable Product
*   **Core Gamification Loop:** XP, Streaks, Hearts, Leaderboards.
*   **Lesson Engine:** Multiple choice, listening, and basic speaking exercises.
*   **AI Speaking Companion (Beta):** Text and Voice-based roleplay for specific scenarios (A1 level).
*   **Curriculum:**
    *   English for Vietnamese Speakers.
    *   English for Indonesian Speakers.
    *   Vietnamese for English Speakers (Tourist focus).
*   **Platform:** PWA with offline support for current lesson.
*   **Monetization:** Ad-supported model.

### Growth Features (Post-MVP)
*   **Micro-transactions:** Sachet pricing for "Streak Freezes" and "Heart Refills" via local e-wallets (GoPay, MoMo).
*   **K-Wave Bridge:** Korean and Japanese courses for SEA speakers.
*   **Advanced AI:** Free-form conversation practice with dynamic difficulty adjustment.
*   **Social Features:** Friends quests, clans/clubs.

### Vision (Future)
To be the **primary language learning resource** for:
1.  SEA users learning English for economic mobility.
2.  Global users wanting to learn SEA languages for travel and culture.
Ultimately becoming the "Super App" for language education in the region.

---

## Domain-Specific Requirements (EdTech)

*   **Pedagogical Alignment:** Content must align with CEFR (Common European Framework of Reference for Languages) standards.
*   **Content Safety:** AI interactions must be strictly guardrailed to prevent inappropriate, offensive, or culturally insensitive outputs.
*   **Feedback Loops:** The system must provide immediate, corrective feedback to the user, not just "correct/incorrect."
*   **Progress Tracking:** Visual representation of learning path and mastery.

---

## Innovation & Novel Patterns

### AI-First with Human Guardrails
*   **Pattern:** "Expert-in-the-Loop" AI.
*   **Implementation:** Language experts define the "Golden Path" of a conversation. The AI guides the user along this path but allows for natural deviations. If the user strays too far or the AI detects confusion, it gently nudges them back to the expert-defined curriculum.
*   **Validation:** A/B test AI-generated feedback vs. static feedback to measure impact on learning retention.

---

## Web App (PWA) Specific Requirements

### Platform Support
*   **Responsive Design:** Mobile-first UI (360px width min) that scales up to tablet/desktop.
*   **PWA Capabilities:** Manifest file for "Add to Home Screen," Service Workers for offline caching of assets and next lessons.
*   **Browser Support:** Chrome (Android), Safari (iOS), Firefox.

### Device Capabilities
*   **Audio Input:** Robust microphone access and permission handling for speaking exercises.
*   **Audio Output:** Text-to-Speech (TTS) integration for lesson audio.
*   **Haptics:** Vibration feedback for correct/incorrect answers (where supported).

---

## User Experience Principles

*   **"Snackable" Learning:** Lessons must be completeable in < 5 minutes.
*   **Playful & Encouraging:** Bright colors, mascots, positive reinforcement (sound effects, animations).
*   **Forgiving:** Mistakes are part of learning; "Hearts" mechanic balances challenge with frustration.
*   **Culturally Resonant:** UI themes and illustrations should reflect SEA aesthetics and contexts (e.g., scooters, street food stalls).

---

## Functional Requirements

### User Management
*   **FR1:** Users can sign up/login using Email, Google, or Facebook.
*   **FR2:** Users can onboard by selecting a source language and a target language.
*   **FR3:** Users can take a placement test to skip beginner levels.
*   **FR4:** Users can manage their profile (avatar, display name, daily goal).

### Learning Engine
*   **FR5:** Users can view a linear learning path (Unit -> Chapter -> Lesson).
*   **FR6:** Users can complete interactive lessons with mixed question types (Translation, Listening, Matching, Speaking).
*   **FR7:** Users receive immediate feedback on every answer.
*   **FR8:** Users can listen to audio pronunciation of words and sentences.
*   **FR9:** Users can use the microphone to record speech for pronunciation assessment.

### AI Speaking Companion
*   **FR10:** Users can enter a "Roleplay" mode to chat with an AI character.
*   **FR11:** AI characters simulate specific personas (e.g., "Market Vendor," "Taxi Driver").
*   **FR12:** Users can see a transcript of the conversation.
*   **FR13:** Users receive AI-generated suggestions for better phrasing after the conversation.

### Gamification & Progress
*   **FR14:** Users earn XP (Experience Points) for completing lessons.
*   **FR15:** Users maintain a "Streak" by completing at least one lesson daily.
*   **FR16:** Users have a limited number of "Hearts" (lives) that deplete with wrong answers.
*   **FR17:** Users can view their position on a weekly Leaderboard.
*   **FR18:** Users earn badges/achievements for milestones.

### Monetization (Shop)
*   **FR19:** Users can view a virtual shop.
*   **FR20:** Users can spend virtual currency (Gems) on items like "Streak Freeze" or "Heart Refill."
*   **FR21:** Users can watch video ads to regain Hearts (Freemium).

### Content Management (Admin)
*   **FR22:** Admins (Experts) can create and edit course structures (Units, Lessons).
*   **FR23:** Admins can define "Golden Path" scripts for AI roleplays.
*   **FR24:** Admins can review flagged AI interactions for quality control.

---

## Non-Functional Requirements

### Performance
*   **NFR1:** Lesson load time must be < 2 seconds on 4G networks.
*   **NFR2:** AI response latency must be < 1.5 seconds to maintain conversational flow.
*   **NFR3:** App bundle size (initial load) must be < 5MB.

### Reliability & Offline
*   **NFR4:** Users can complete the *next* lesson even without an active internet connection (cached).
*   **NFR5:** Progress syncs automatically when connection is restored.

### Security & Privacy
*   **NFR6:** User data (especially voice recordings) must be encrypted in transit and at rest.
*   **NFR7:** AI inputs must be sanitized to prevent prompt injection attacks.

### Accessibility
*   **NFR8:** High contrast mode support.
*   **NFR9:** Screen reader compatibility for core navigation.

---

_This PRD captures the essence of Duolingo Clone (SEA Focus) - A hyper-localized, AI-powered language learning companion._

_Created through collaborative discovery between Hayden and AI facilitator._
