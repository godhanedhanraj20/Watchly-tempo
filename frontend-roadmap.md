# Watchly Frontend – First Review & Roadmap

## First-review summary of the screens
The uploaded screens depict a dark-mode, premium-feel watch‑party experience that blends video playback, real‑time chat, and a lightweight room management flow. The UI prioritizes calm feedback states, clear call‑to‑action buttons, and contextual system messages (e.g., reconnecting, permission denied, room full). The product appears to focus on Google Drive streaming with synchronized playback, a host/guest role model, and small, consistent modal patterns for critical actions such as creating rooms, copying links, and logging out.

### Key UI themes observed
- **Dark, cinematic visual language** with soft glows, muted surfaces, and elevated cards.
- **Clear CTA hierarchy** (primary blue actions, secondary neutral, destructive red).
- **Modal‑first flows** for room creation, share links, and confirmations.
- **Stateful feedback** (loading, error, permission denied, reconnecting, sign‑in required).
- **Room‑centric navigation** with persistent header, host status indicator, and participants list.

## Frontend description (what we’re building)
A web application called **Watchly** that lets users sign in with Google, create or join watch rooms, and stream videos from Google Drive in perfect sync with friends. The UI is anchored by a dark theme with high contrast for accessibility, a strong visual focus on the playback area, and real‑time collaboration elements (chat, participants, host controls). The app includes robust system feedback states for sign‑in, room capacity, permissions, reconnection, and playback syncing.

### Core screens/components implied by the designs
1. **Landing / Auth**: single CTA to sign in with Google; short product description and “How it works” link.
2. **Signing-in loading overlay**: minimal spinner with short status text.
3. **Dashboard**: create room, join room, and recent room list with quick actions.
4. **Create room modal**: optional room name input, context hints, confirm/cancel.
5. **Room ready modal**: share link, copy link, open room.
6. **Room player view**: video player, host controls, participant list, chat panel, copy link, leave room.
7. **Room information modal**: share link, capacity, room type, leave room/transfer host.
8. **System feedback collection**: room full, sign‑in required, general error, permission denied, reconnecting, syncing playback.
9. **Logout confirmation modal** with toast feedback.
10. **Mobile layout** with tabs for chat/participants and inline error prompt.

## Frontend roadmap

### Phase 1 – Foundations & UI system (Week 1)
- Establish design tokens for dark theme (colors, elevation, radii, typography, spacing).
- Build a reusable component library: buttons, inputs, cards, modal shell, toast, badges, avatars, tooltips.
- Implement global layout shell (header, page container, overlays).
- Create skeleton loading states and spinners consistent with the visual language.


### Phase 2 – Auth & entry flows (Week 2)
- Build landing page and Google sign‑in CTA.
- Add “Signing you in…” overlay state.
- Wire auth state handling and route guards (signed‑out vs. signed‑in).

### Phase 3 – Room management (Week 3)
- Create dashboard screen (Create Room card, Join Room form, recent rooms list).
- Implement Create Room modal flow and validation.
- Build “Room ready” confirmation modal with link copy success message.

### Phase 4 – Watch room experience (Weeks 4–5)
- Build full watch room layout (player, chat, participant list, host badge, top bar actions).
- Implement chat UI (message bubbles, timestamping, input composer).
- Add host controls/resync UI; display playback sync badges.
- Build Room Information modal (share link, capacity, leave room, transfer host).

### Phase 5 – System feedback & resilience (Week 6)
- Add error/modals: room full, sign‑in required, generic error, permission denied.
- Implement inline banners for reconnecting and sync feedback in the player.
- Add toast notifications (logout success, link copied, errors).

### Phase 6 – Mobile & responsiveness (Week 7)
- Optimize mobile layout with chat/participants tabs.
- Ensure controls and modals are fully usable on small screens.
- Perform accessibility audit for contrast, focus states, keyboard nav.

### Phase 7 – Polish & QA (Week 8)
- Visual polish pass (hover/focus transitions, blur/backdrop, shadows).
- Cross‑browser testing and performance tuning.
- Content review for tone consistency and error messaging.

## Deliverables by milestone
- **M1**: Design system + layout shell + component kit.
- **M2**: Auth flows (landing + sign‑in overlay).
- **M3**: Room creation & dashboard flows.
- **M4**: Full watch room MVP (player + chat + participants + host controls).
- **M5**: Feedback states & resilience coverage.
- **M6**: Mobile responsiveness & accessibility.
- **M7**: Final polish + QA.
