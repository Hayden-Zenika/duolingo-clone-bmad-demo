# API Contracts

## Overview
The application uses Next.js App Router API routes for backend functionality.

## Endpoints

### Challenges
- `GET /api/challenges` - List challenges
- `POST /api/challenges` - Create challenge
- `GET /api/challenges/[challengeId]` - Get challenge details
- `PUT /api/challenges/[challengeId]` - Update challenge
- `DELETE /api/challenges/[challengeId]` - Delete challenge

### Courses
- `GET /api/courses` - List courses
- `POST /api/courses` - Create course
- `GET /api/courses/[courseId]` - Get course details
- `PUT /api/courses/[courseId]` - Update course
- `DELETE /api/courses/[courseId]` - Delete course

### Challenge Options
- `GET /api/challengeOptions` - List challenge options
- `POST /api/challengeOptions` - Create challenge option
- `GET /api/challengeOptions/[challengeOptionId]` - Get challenge option details
- `PUT /api/challengeOptions/[challengeOptionId]` - Update challenge option
- `DELETE /api/challengeOptions/[challengeOptionId]` - Delete challenge option

### Lessons
- `GET /api/lessons` - List lessons
- `POST /api/lessons` - Create lesson
- `GET /api/lessons/[lessonId]` - Get lesson details
- `PUT /api/lessons/[lessonId]` - Update lesson
- `DELETE /api/lessons/[lessonId]` - Delete lesson

### Units
- `GET /api/units` - List units
- `POST /api/units` - Create unit
- `GET /api/units/[unitId]` - Get unit details
- `PUT /api/units/[unitId]` - Update unit
- `DELETE /api/units/[unitId]` - Delete unit

### Webhooks
- `POST /api/webhooks/stripe` - Stripe webhook handler
