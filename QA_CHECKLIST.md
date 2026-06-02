# Daily Toolkit - Pre-Launch QA Checklist

> **Status Legend**: ⬜ Not Tested | ✅ Pass | ❌ Fail | 🔄 Blocked  
> **Test Date**: ___/___/______  
> **Tester**: _________________  

---

## 1. Installation & Onboarding

| # | Test Case | Steps | Expected Result | Status | Notes |
|---|-----------|-------|-----------------|--------|-------|
| 1.1 | Fresh Install | 1. Go to Shopify App Store  <br>2. Click "Add app"  <br>3. Complete OAuth flow | App installs successfully, redirects to app admin | ⬜ | |
| 1.2 | OAuth Scopes | Check scope approval screen | Only required scopes shown (no excessive permissions) | ⬜ | Current: `read_products`, `write_products`, `read_themes`, `write_themes` |
| 1.3 | Post-Install Redirect | Complete OAuth | Redirects to `/app` with welcome screen | ⬜ | |
| 1.4 | Reinstall After Uninstall | 1. Uninstall app  <br>2. Reinstall within 24h | OAuth completes, no session conflicts | ⬜ | |

---

## 2. Uninstall & Data Cleanup (GDPR)

| # | Test Case | Steps | Expected Result | Status | Notes |
|---|-----------|-------|-----------------|--------|-------|
| 2.1 | Uninstall Webhook | 1. Create bundle/timer settings  <br>2. Uninstall app from Shopify admin  <br>3. Check Supabase DB | All shop data deleted from: <br>- `tool_settings` <br>- `bundle_configs` | ⬜ | Check logs for `[Uninstall] Data cleanup completed` |
| 2.2 | Metafield Cleanup | After uninstall | App metafields removed from store (verify with GraphQL) | ⬜ | Query: `app.metafields.daily-toolkit.*` |
| 2.3 | Reinstall After Cleanup | Reinstall app after 5+ min | Fresh state (no old settings) | ⬜ | |

---

## 3. Theme Compatibility - Dawn Theme

**Store URL**: _________________  
**Theme**: Dawn v___._.__

### 3.1 Countdown Timer
| # | Test Case | Steps | Expected Result | Status | Notes |
|---|-----------|-------|-----------------|--------|-------|
| 3.1.1 | Enable Timer | 1. Go to Countdown Timer tool  <br>2. Enable toggle  <br>3. Set end date | Timer appears on storefront product pages | ⬜ | |
| 3.1.2 | Timer Accuracy | Check storefront display | Countdown shows correct days/hours/mins/secs | ⬜ | |
| 3.1.3 | Expiry Behavior | Wait for timer to reach 0 | Timer shows "Expired" message or hides per settings | ⬜ | |
| 3.1.4 | Style Presets | Apply different presets | Each preset renders correctly (colors, layout) | ⬜ | Test at least 3 presets |
| 3.1.5 | Mobile View | View on mobile device | Timer responsive and readable | ⬜ | |

### 3.2 Bundle Offers
| # | Test Case | Steps | Expected Result | Status | Notes |
|---|-----------|-------|-----------------|--------|-------|
| 3.2.1 | Create Bundle | 1. Create quantity break bundle  <br>2. Enable global toggle  <br>3. Set target products | Bundle widget appears on product pages | ⬜ | |
| 3.2.2 | Bundle Selection | Click different quantity options | Visual selection updates, price recalculates | ⬜ | |
| 3.2.3 | Add to Cart | Click "Add to cart" | Correct quantity/price added to cart | ⬜ | |
| 3.2.4 | Toggle Off | Disable global toggle | Bundle widget disappears from storefront | ⬜ | Sync should be instant |
| 3.2.5 | Multiple Bundles | Create 3+ bundles | Only enabled bundles show, no conflicts | ⬜ | |

### 3.3 Offer Bar
| # | Test Case | Steps | Expected Result | Status | Notes |
|---|-----------|-------|-----------------|--------|-------|
| 3.3.1 | Enable Bar | Create announcement bar with CTA | Bar appears at top of all pages | ⬜ | |
| 3.3.2 | Sticky Behavior | Scroll down page | Bar remains fixed at top (if sticky enabled) | ⬜ | |
| 3.3.3 | CTA Click | Click CTA button | Navigates to correct URL (new tab if configured) | ⬜ | |
| 3.3.4 | Rotating Messages | Enable rotating messages | Messages cycle automatically | ⬜ | |
| 3.3.5 | Mobile View | View on mobile | Bar responsive, text readable | ⬜ | |

### 3.4 Popup Builder
| # | Test Case | Steps | Expected Result | Status | Notes |
|---|-----------|-------|-----------------|--------|-------|
| 3.4.1 | Time Trigger | Set 5-second delay | Popup appears after 5 seconds | ⬜ | |
| 3.4.2 | Exit Intent | Move cursor to close tab | Popup appears before leaving | ⬜ | Test on desktop only |
| 3.4.3 | Close Button | Click X | Popup closes, doesn't reappear (session cookie) | ⬜ | |
| 3.4.4 | CTA Navigation | Click popup CTA | Opens correct URL | ⬜ | |
| 3.4.5 | Image Upload | Upload custom image | Image displays correctly in popup | ⬜ | |

### 3.5 Trust Badges
| # | Test Case | Steps | Expected Result | Status | Notes |
|---|-----------|-------|-----------------|--------|-------|
| 3.5.1 | Enable Badges | Select 3 badges, enable | Badges appear on product pages | ⬜ | |
| 3.5.2 | Custom Text | Edit badge text | Custom text displays correctly | ⬜ | |
| 3.5.3 | Icon Selection | Change badge icons | New icons render correctly | ⬜ | |

---

## 4. Theme Compatibility - Non-Dawn Theme

**Test Theme**: _________________ (e.g., Impulse, Prestige, Warehouse)

| # | Test Case | Tool | Expected Result | Status | Notes |
|---|-----------|------|-----------------|--------|-------|
| 4.1 | Bundle Display | Bundle Offers | Renders without layout breaks | ⬜ | |
| 4.2 | Timer Display | Countdown Timer | Styling doesn't conflict with theme | ⬜ | |
| 4.3 | Offer Bar | Offer Bar | Positioning works (top/bottom) | ⬜ | |
| 4.4 | Popup | Popup Builder | Z-index correct (above theme elements) | ⬜ | |

---

## 5. Admin Panel Functionality

| # | Test Case | Steps | Expected Result | Status | Notes |
|---|-----------|-------|-----------------|--------|-------|
| 5.1 | Navigation | Click between tools | Smooth navigation, no 404s | ⬜ | |
| 5.2 | Save Settings | Edit and save any tool | "Saved" confirmation appears | ⬜ | |
| 5.3 | Discard Changes | Make edits → click Discard | Changes reverted to saved state | ⬜ | |
| 5.4 | Preview Panel | Edit settings | Preview updates in real-time | ⬜ | |
| 5.5 | Mobile Admin | Access on mobile device | Admin usable (may have limitations) | ⬜ | |

---

## 6. Data Sync & Webhooks

| # | Test Case | Steps | Expected Result | Status | Notes |
|---|-----------|-------|-----------------|--------|-------|
| 6.1 | Metafield Sync | 1. Save bundle settings  <br>2. Check Shopify GraphQL | Metafields updated with correct JSON | ⬜ | Query: `{ app { metafields { edges { node { namespace key value } } } } }` |
| 6.2 | Shop Uninstall Webhook | Uninstall app | Webhook received (check logs) | ⬜ | Log entry: `Received app/uninstalled webhook` |
| 6.3 | Scopes Update Webhook | Modify app scopes | Session scope updated in DB | ⬜ | |
| 6.4 | Health Check | Visit `/health` | Returns 200 with DB status | ⬜ | Should show: `{"status":"healthy","checks":{"supabase":true}}` |

---

## 7. Error Handling & Edge Cases

| # | Test Case | Steps | Expected Result | Status | Notes |
|---|-----------|-------|-----------------|--------|-------|
| 7.1 | Invalid Date | Set countdown to past date | Graceful error message | ⬜ | |
| 7.2 | Empty Bundle | Save bundle with no products | Validation error or empty state | ⬜ | |
| 7.3 | Long Text | Enter 500+ char headline | UI handles overflow gracefully | ⬜ | |
| 7.4 | Special Characters | Use emoji, HTML tags in text | Properly escaped, no XSS | ⬜ | Test: `<script>alert('xss')</script>` |
| 7.5 | Network Offline | Disconnect wifi → save | Appropriate error message | ⬜ | |
| 7.6 | Session Expiry | Leave admin idle 30min | Re-auth prompt or auto-refresh | ⬜ | |

---

## 8. Performance & Security

| # | Test Case | Steps | Expected Result | Status | Notes |
|---|-----------|-------|-----------------|--------|-------|
| 8.1 | Storefront Load Time | Measure page load with tools | < 200ms added to TTFB | ⬜ | Use Lighthouse |
| 8.2 | No Console Errors | Check browser console | No JS errors from app scripts | ⬜ | |
| 8.3 | CSP Compliance | Check for inline scripts | No CSP violations reported | ⬜ | |
| 8.4 | HTTPS Only | Attempt HTTP request | Redirects to HTTPS | ⬜ | |
| 8.5 | Admin API Rate Limits | Rapid save operations | No 429 errors, graceful handling | ⬜ | |

---

## 9. Multi-Store/Merchant Scenarios

| # | Test Case | Steps | Expected Result | Status | Notes |
|---|-----------|-------|-----------------|--------|-------|
| 9.1 | Data Isolation | Check DB: two shops' data | No cross-contamination of settings | ⬜ | Query: `SELECT shop_domain, COUNT(*) FROM tool_settings GROUP BY shop_domain` |
| 9.2 | Concurrent Edits | Two admins edit same tool | Last write wins (expected behavior) | ⬜ | |

---

## 10. Accessibility (WCAG 2.1 AA)

| # | Test Case | Steps | Expected Result | Status | Notes |
|---|-----------|-------|-----------------|--------|-------|
| 10.1 | Keyboard Navigation | Tab through all interactive elements | All buttons/links focusable | ⬜ | |
| 10.2 | Screen Reader | Use NVDA/VoiceOver | Labels announced correctly | ⬜ | |
| 10.3 | Color Contrast | Check with contrast checker | All text ≥ 4.5:1 ratio | ⬜ | |
| 10.4 | Focus Indicators | Tab through storefront widgets | Visible focus rings | ⬜ | |

---

## Sign-Off

| Role | Name | Date | Signature |
|------|------|------|-----------|
| QA Tester | | | |
| Tech Lead Review | | | |
| Product Owner | | | |

---

## Post-Launch Monitoring Checklist

Set up these monitors before launch:

- [ ] Error tracking (Sentry/Rollbar) configured
- [ ] Uptime monitoring for `/health` endpoint
- [ ] Shopify webhook delivery monitoring
- [ ] Daily DB backup verification
- [ ] App store reviews alert

---

## Quick Reference: Test Store URLs

| Store | Theme | URL | Notes |
|-------|-------|-----|-------|
| Test Store 1 | Dawn | | |
| Test Store 2 | Non-Dawn | | |
| Production | | | DO NOT TEST ON PROD |

---

## Known Issues / Blockers

| Issue | Severity | Ticket | Status |
|-------|----------|--------|--------|
| | | | |

---

## Revision History

| Date | Version | Changes | Author |
|------|---------|---------|--------|
| 2025-01-XX | 1.0 | Initial checklist | |
