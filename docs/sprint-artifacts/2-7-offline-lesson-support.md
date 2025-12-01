# Story 2.7: Offline Lesson Support

Status: drafted
Jira Issue: DC-9

## Story

As a user,
I want to complete my next lesson even if I lose internet connection,
so that I can learn on the go without interruption.

## Acceptance Criteria

1. Service Worker caches the *active* lesson's data and assets (audio/images) when the user is on the Learn page.
2. User can start and complete the lesson while offline.
3. Lesson completion result is queued and synced when connection is restored.

## Tasks / Subtasks

- [ ] Configure Serwist for Service Worker generation
  - [ ] Install `@serwist/next` and `@serwist/precaching`
  - [ ] Create `app/sw.ts` configuration
  - [ ] Update `next.config.mjs` to use Serwist
  - [ ] Add `manifest.json` to `public/` and link in `app/layout.tsx`
- [ ] Implement Offline Caching Strategy
  - [ ] Configure runtime caching for API routes (`/api/lessons/*`, `/api/courses/*`)
  - [ ] Configure caching for static assets (images, audio)
  - [ ] Ensure `user_progress` is cached
- [ ] Refactor Lesson Data Fetching for Offline Support
  - [ ] Verify `useQuery` is used for fetching lesson data
  - [ ] Ensure `staleTime` and `gcTime` are configured to allow offline access
- [ ] Implement Offline Mutation Queue
  - [ ] Use `persistQueryClient` from TanStack Query
  - [ ] Configure `createSyncStoragePersister` (using `idb-keyval` or `localStorage`)
  - [ ] Wrap `lesson-completion` mutation to support offline queuing
- [ ] UI Indicators
  - [ ] Add "Offline Mode" indicator in the UI when disconnected
  - [ ] Show toast notification when connection is restored and sync happens

## Dev Notes

- **Architecture Pattern**: Offline-First using Serwist + TanStack Query (ADR-001).
- **Constraint**: Server Actions cannot be easily cached for offline use. Ensure data fetching uses API endpoints compatible with TanStack Query caching.
- **Testing**: Use Playwright to simulate offline mode and verify sync.
- **Library**: `serwist` is the replacement for `next-pwa`.

### Project Structure Notes

- `app/sw.ts`: Service Worker configuration.
- `public/manifest.json`: PWA manifest.
- `lib/query-client.ts`: TanStack Query client configuration (needs persistence setup).

### References

- [Source: docs/architecture.md#ADR-001-Offline-First-Architecture]
- [Source: docs/epics.md#Story-2.7-Offline-Lesson-Support]

## Dev Agent Record

### Context Reference

<!-- Path(s) to story context XML will be added here by context workflow -->

### Agent Model Used

Gemini 3 Pro (Preview)

### Debug Log References

### Completion Notes List

### File List
