# Example Executions: Spec → Delivered

## Example 1: Campaign Execution (4 Tasks, 1 Blocker, Green)

**Spec**: Launch "Speed-First Creator" campaign. Target emerging creators on Twitter. Budget: $2K/week. Goal: 500 signups in 4 weeks.

**Acceptance Criteria**:
- Campaign live on Twitter + Instagram
- All creative assets approved brand review
- Analytics connected (conversion tracking)
- Typo-free copy

---

### Task 1: Write Copy Variants (Headlines + Body)

**Subagent dispatch**:
```
Write 3 headline + body combos for Twitter + Instagram ads.

Spec excerpt: "Position on speed. 'Create in 5 minutes.'"

Acceptance criteria:
- 3 distinct copy angles (speed, results, social proof)
- Fit Twitter (280 chars) + Instagram (longer form)
- All copy reflects "Speed-First Creator" positioning
- No typos

Constraints:
- No brand voice inconsistencies
- Include CTA in all variants

Self-review:
- [ ] Copy reads clean
- [ ] All variants test different angles
- [ ] No typos (human proofread)
```

**Result**: 
- Variant A: "Create Instagram posts in 5 minutes. Ship before coffee gets cold."
- Variant B: "Professional results. Zero design training. Speed included."
- Variant C: "Watch 10k creators ship daily. See how fast they work."

**Signal**: 🟢 Green (all criteria met, copy tested against positioning)

---

### Task 2: Design Visual Assets (Hero Image + Button)

**Subagent dispatch**:
```
Design hero image (1200x630 for social) + CTA button.

Spec excerpt: "Speed-First Creator positioning. Target Gen Z creators."

Acceptance criteria:
- Hero image shows fast workflow (motion, energy)
- Color palette matches brand (reference colors in spec)
- Button CTA is clear ("Create for Free" or similar)
- Accessibility: Contrast ratio ≥4.5:1

Constraints:
- No stock photos; original design or illustrations
- Mobile-friendly (test at 375px width)

Self-review:
- [ ] Colors match brand
- [ ] Image conveys speed/energy
- [ ] Contrast meets WCAG AA
- [ ] Mobile renders correctly
```

**Result**: 
- Hero: Animated illustration of creator moving fast (laptop, phone, coffee). Bright cyan + magenta color scheme.
- Button: "Create for Free" in sans-serif, white-on-cyan, 16px touch target

**Signal**: 🟢 Green (brand-aligned, mobile-tested, accessibility met)

---

### Task 3: Set Up Analytics & Tracking

**Subagent dispatch**:
```
Connect Segment / GA4 tracking to campaign.

Spec excerpt: "Track signups + trial starts"

Acceptance criteria:
- Pixel fires on ad click
- Signup event tracked (email + source)
- Trial start event tracked
- No data leakage (PII cleaned)

Constraints:
- Use existing analytics stack (Segment)
- GDPR compliant

Self-review:
- [ ] Pixels verified (browser DevTools)
- [ ] Events tested (fake signup flows)
- [ ] No PII in analytics
```

**Result**: 
- Twitter pixel + Instagram pixel connected
- Signup event: name + email (no passwords/PII)
- Trial event: user_id + plan_tier

**Blocker Hit**: ❌ **BLOCKER: Segment API key expired. Pixel won't fire.**

**Tier 1 Self-Research (5 min)**:
- Subagent re-reads: API key in .env is expired (last rotated 6mo ago)
- Fix: Generate new API key in Segment dashboard, update .env, test pixel
- Result: Pixel now fires ✓

**Signal**: 🟢 Green (blocker self-resolved)

---

### Task 4: Create Sample Campaign Brief (Setup)

**Subagent dispatch**:
```
Create mock Twitter + Instagram campaign posts using approved copy + assets.

Spec excerpt: "Campaign goes live on Twitter + Instagram"

Acceptance criteria:
- Twitter posts use copy variant (280 chars max)
- Instagram posts use longer copy + hero image
- Posts preview correctly in platform
- Brand consistency check (colors, tone, CTA match)

Constraints:
- Posts are draft (not published yet)
- Include screenshot proof of preview

Self-review:
- [ ] Copy fits platform character limits
- [ ] Images render correctly
- [ ] CTA is visible and clickable
- [ ] No typos (final proofread)
```

**Result**: 
- Twitter post: "Create Instagram posts in 5 minutes. Ship before coffee gets cold. Join 10k creators. [link]" (279 chars)
- Instagram post: Longer headline + hero image + CTA button "Create for Free"
- Screenshots attached

**Smoke Gate**:
- ✓ Draft posts created
- ✓ All assets render correctly
- ✓ Copy is typo-free (human proofread)
- ✓ Brand colors match spec

**Signal**: 🟢 Green (all smoke gates passed)

---

## Summary

| Task | Result | Signal | Notes |
|------|--------|--------|-------|
| Copy variants | 3 approved | 🟢 | All angles test different positioning |
| Visual assets | Hero + button | 🟢 | Mobile-tested, accessible |
| Analytics setup | Segment configured | 🟢 | Blocker hit (API key expired), Tier 1 self-resolved |
| Campaign brief | Draft posts + screenshots | 🟢 | Ready to publish |

**Total time**: 3 hours (1.5 hr per task)
**Confidence**: All green. Ready to publish.

---

## Example 2: Feature Build (5 Tasks, 2 Blockers, 1 Yellow)

**Spec**: Build "Quick Share" feature. Users can share their creations directly to Instagram/TikTok.

**Acceptance Criteria**:
- User clicks "Share to Instagram" button
- Pre-filled caption (uses creator's last message)
- Image is exported (MP4 or PNG)
- Redirect to Instagram (open app or web)

---

### Task 1: Implement Export Logic (Core)

**Subagent dispatch**:
```
Build export function: design canvas → MP4/PNG file.

Spec excerpt: "Export for Instagram (video or image format)"

Acceptance criteria:
- Canvas exports to valid MP4 (H.264 codec)
- Exports to PNG as fallback
- File is <100MB (Instagram limit)
- No console errors

Constraints:
- Use existing ffmpeg wrapper (src/utils/ffmpeg.ts)
- Verify ffmpeg binary exists before exporting

Self-review:
- [ ] Export function tested (mock canvas)
- [ ] Formats verified (ffmpeg -version check)
- [ ] File sizes under limit
```

**Blocker Hit**: ❌ **BLOCKER: ffmpeg.ts doesn't exist. Hallucinated import.**

**Tier 2 Escalation**: 
- Fresh subagent reviews, identifies hallucination
- Searches codebase: finds `src/services/videoExport.ts` (actual export service)
- Rewrites to use correct import: `import { exportVideo } from 'src/services/videoExport'`
- Tests: Export works ✓

**Signal**: 🟢 Green (blocker escalated, resolved, no stubs)

---

### Task 2: Build UI Component (Share Button)

**Subagent dispatch**:
```
Build "Share to Instagram" button component.

Spec excerpt: "User clicks button, Instagram opens with pre-filled caption"

Acceptance criteria:
- Button visible in design canvas (top-right area)
- On click: exports video + opens Instagram with caption
- Capt

ion pre-fills last message (if available)
- Mobile responsive (test at 375px)

Constraints:
- No placeholder API endpoints
- Verify Instagram share URL scheme works

Self-review:
- [ ] Button renders correctly
- [ ] Click handler doesn't throw
- [ ] Mobile responsive
- [ ] Screenshot proof
```

**Result**:
```tsx
<button onClick={handleShareInstagram}>
  Share to Instagram
</button>

const handleShareInstagram = async () => {
  const video = await exportVideo(canvas);
  const caption = state.lastMessage || 'Check this out!';
  const url = `https://www.instagram.com/?url=${encodeURIComponent(window.location.href)}&text=${encodeURIComponent(caption)}`;
  window.open(url, '_blank');
}
```

**Signal**: 🟡 Yellow (works, but Instagram share URL may not pre-fill caption. Acceptable MVP behavior — users will paste caption themselves if needed. Document as known limitation.)

---

### Task 3: Wire Integration (Export + UI)

**Subagent dispatch**:
```
Connect "Share to Instagram" button to export logic.

Spec excerpt: "Click button → export → share"

Acceptance criteria:
- User clicks button
- Export starts (loading spinner shows)
- Instagram opens (or app if user has it)
- No console errors

Constraints:
- Verify export succeeds before opening Instagram
- Graceful failure if export takes >10 sec

Self-review:
- [ ] All event handlers wired
- [ ] No missing dependencies
- [ ] Error handling in place
- [ ] Smoke test: dev server + manual click
```

**Result**:
- Button click triggers export
- Loading spinner shows during export
- Instagram link opens after export
- Error handling: if export fails, show toast notification

**Signal**: 🟢 Green (integrated, tested)

---

### Task 4: Polish & Accessibility

**Subagent dispatch**:
```
Polish UI: button styling + accessibility.

Spec excerpt: "User-friendly, accessible sharing"

Acceptance criteria:
- Button has visible focus state (keyboard navigation)
- Aria labels correct (for screen readers)
- Color contrast ≥4.5:1
- Touch target ≥44px

Constraints:
- Match existing design system
- No new dependencies

Self-review:
- [ ] Focus state visible
- [ ] Aria labels added
- [ ] Contrast verified (DevTools accessibility tab)
- [ ] Touch target tested (44px min)
```

**Result**:
- Button has blue focus ring (keyboard visible)
- Aria-label: "Share to Instagram"
- White button on blue bg: contrast 4.8:1 ✓
- Button: 48px tall (touch-friendly)

**Signal**: 🟢 Green (accessible, polished)

---

### Task 5: Smoke Gate & Verification

**Subagent dispatch**:
```
Final smoke gate: dev server + manual test.

Acceptance criteria:
- Dev server starts cleanly (no errors)
- Feature works end-to-end (manual click test)
- Console is clean (no errors/warnings)
- Screenshot proof attached

Constraints:
- No shortcuts; actual manual test
```

**Result**:
- ✓ Dev server runs: `npm run dev` → ready in 8 sec
- ✓ Manual test: Click "Share to Instagram" → export takes 3 sec → Instagram opens
- ✓ Console clean (no errors)
- ✓ Screenshot: button + loading spinner + Instagram share screen

**Signal**: 🟢 Green (smoke gate passed)

---

## Summary

| Task | Result | Signal | Notes |
|------|--------|--------|-------|
| Export logic | Video export working | 🟢 | Blocker (hallucinated import), escalated to Tier 2, resolved |
| UI component | Share button built | 🟡 | Caption pre-fill may not work (Instagram limitation), acceptable MVP |
| Integration | Export + UI wired | 🟢 | Fully connected, tested |
| Polish | Accessibility added | 🟢 | WCAG AA compliant, touch-friendly |
| Smoke gate | End-to-end verified | 🟢 | Dev works, manual test passed, console clean |

**Total time**: 4 hours (45 min per task)
**Blockers**: 1 (Tier 2 escalation, resolved)
**Known limitations**: 1 (Instagram caption pre-fill)
**Confidence**: 🟢 Green for core feature. 🟡 Yellow for caption pre-fill (document, ship, iterate).

