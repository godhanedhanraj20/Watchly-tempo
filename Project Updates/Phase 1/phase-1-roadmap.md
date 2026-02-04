# Phase 1 – Foundations & UI System (Week 1)

## Detailed timeline & tasks
**Day 1 – Design tokens + theme setup**
- Define the dark theme palette (primary, neutral, error, success, warning) with contrast targets.
- Set elevation and shadow styles for cards, modals, and overlays.
- Establish typography scale and spacing scale.
- Document tokens in a shared theme file (CSS variables or design system config).

**Day 2 – Core primitives**
- Build foundational components: `Button`, `Input`, `Card`, `Badge`, `Avatar`.
- Define sizing variants, disabled states, and focus states for accessibility.
- Validate hover/active states against the dark theme.

**Day 3 – Overlay patterns**
- Implement `Modal` shell with backdrop and focus lock.
- Implement `Toast` system with placement and auto‑dismiss.
- Create `Tooltip` pattern for helper text.

**Day 4 – Layout system**
- Create the global layout shell (header, page container, content area).
- Define layout utilities for consistent spacing and alignment.
- Add sample layout compositions to validate component spacing.

**Day 5 – Loading & skeletons**
- Build spinner + skeleton loaders for cards and forms.
- Ensure motion is subtle and consistent with the visual language.
- Review overall visual coherence and compile a baseline UI kit snapshot.

## Phase 1 checklist
- [ ] Finalize dark theme color tokens with WCAG‑aligned contrast ratios.
- [ ] Define typography scale and spacing scale in design tokens.
- [ ] Implement `Button` with primary/secondary/destructive variants.
- [ ] Implement `Input` with label, hint, and error states.
- [ ] Implement `Card`, `Badge`, and `Avatar` components.
- [ ] Create `Modal` shell with backdrop and focus management.
- [ ] Add `Toast` system with success/error variants.
- [ ] Implement `Tooltip` component for inline guidance.
- [ ] Build layout shell (header + content container).
- [ ] Create skeleton loaders and spinner animations.
- [ ] Document usage examples for each component.

## Phase 1 deliverables
- Design token file (colors, typography, radii, spacing, elevation).
- Reusable component library foundation.
- Layout shell ready for page composition.
- Loading states and skeleton components.
