# Data Models

## Overview
The application uses PostgreSQL with Drizzle ORM.

## Schema

### courses
- `id`: serial (PK)
- `title`: text
- `image_src`: text

### units
- `id`: serial (PK)
- `title`: text
- `description`: text
- `course_id`: integer (FK -> courses.id)
- `order`: integer

### lessons
- `id`: serial (PK)
- `title`: text
- `unit_id`: integer (FK -> units.id)
- `order`: integer

### challenges
- `id`: serial (PK)
- `lesson_id`: integer (FK -> lessons.id)
- `type`: enum (SELECT, ASSIST)
- `question`: text
- `order`: integer

### challenge_options
- `id`: serial (PK)
- `challenge_id`: integer (FK -> challenges.id)
- `text`: text
- `correct`: boolean
- `image_src`: text
- `audio_src`: text

### challenge_progress
- `id`: serial (PK)
- `user_id`: text
- `challenge_id`: integer (FK -> challenges.id)
- `completed`: boolean

### user_progress
- `user_id`: text (PK)
- `user_name`: text
- `user_image_src`: text
- `active_course_id`: integer (FK -> courses.id)
- `hearts`: integer
- `points`: integer

### user_subscription
- `id`: serial (PK)
- `user_id`: text (Unique)
- `stripe_customer_id`: text (Unique)
- `stripe_subscription_id`: text (Unique)
- `stripe_price_id`: text
- `stripe_current_period_end`: timestamp
