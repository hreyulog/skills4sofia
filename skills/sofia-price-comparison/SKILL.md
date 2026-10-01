---
name: sofia-price-comparison
description: Compare products across requested shopping apps using exact SKU evidence, price conditions and bounded work per platform. Apply only to shopping comparison tasks.
---

# Price comparison

Apply only if the user requested shopping research or a comparison. Follow the phone-operation and failure-recovery Skills. Do not perform purchases, add to cart or solve challenges. Existing saved-login restoration follows the bounded rule below.

When an app-specific Skill such as `sofia-jd` or `sofia-taobao` is loaded, use that Skill's page-recognition and evidence strategy instead of applying one generic screenshot/tree assumption to every platform.

## Saved login and blockers

The owner permits reuse of an existing saved login for shopping research. A login banner alone does not prove research is blocked: read whether results and controls remain available first.

- If a login page offers an observed existing-account/session continuation or saved-login action that needs no password entry, verification code, biometric confirmation, new agreement, permission or new account linkage, attempt that restoration ONCE. Use only the account already shown; never guess an account or retrieve credentials. A prefilled phone number alone is not a saved authenticated session.
- Verify the returned observation: login UI must disappear and the requested app/search must be visible. A click acknowledgement alone is not successful login. If a stale action was skipped, do not repeat it as a login attempt.
- If restoration still shows login, needs human input, or no eligible saved-login control exists, record the blocker and move to the next requested platform immediately. Do not tap around the login page, Back and resubmit the search, or try a different login method.
- CAPTCHA, risk verification, payment and new consent remain human steps. For a multi-platform comparison finish independent platforms before asking for manual help, rather than pausing the whole task at the first blocker.

## Task ledger and progress

Before starting phone actions, keep a short ledger of every requested platform: NOT_STARTED, EVIDENCE_COLLECTED or BLOCKED, plus the exact SKU and observed price conditions. Discover the installed apps once with one inventory call and reuse their bundles. Load core/task Skills and each platform Skill once; reads are cached.

There is NO fixed per-app phone-call quota. Continue as many necessary, evidence-producing steps as the task needs. Move on when a platform has useful evidence or a real blocker, rather than stopping because of an arbitrary call count. Distinguish actual progress from repeatedly trying an unchanged control. Cover ALL requested platforms before refining one platform further. After each platform, emit a short visible progress note with its observed evidence or blocker before opening the next app; this preserves the ledger when old tool context is compacted. Batch independent Skill reads in one round.

After each returned observation, decide whether it changed the task state. Two attempts on the same unchanged control end that interaction. One fresh visual observation may identify a different, actually observed route; if that route also fails, mark the app blocked. Do not alternate tap/observe/tap/observe. Never repeat a query that is already correct just because result cards are custom-rendered.

## Scope and search

- Keep the requested platform list, model, RAM/storage, condition and other specified attributes. Do not replace Standard with Pro, Pro Max, refurbished or a different capacity. If the user left an essential attribute ambiguous, ask briefly.
- Discover the requested apps once, then reuse those discovered bundles while moving across platforms. Read what actually opened. Search the exact requested model and capacity. If an old search already matches, inspect the visible listings without claiming a fresh submission.
- Named shopping platforms use their phone apps by default. Use websites only when the user explicitly selected web access for this task or conversation. A missing app, connection problem, login or CAPTCHA never authorizes an automatic switch to a website.
- Work through platforms independently. For login, apply the saved-login rule once. For CAPTCHA or unresolved login, record that blocker and continue with the next platform. Do not wait, refresh or reopen a blocked platform hoping it disappears.

## Evidence and limits

- Examine up to three plausible listings. Prefer a verified match over endless browsing. Default to one result-page scroll per platform; a second is justified only when a confirmed result page contains no plausible exact match. Use at most one product-detail attempt per platform and only when a critical field cannot be resolved from search-list evidence. A platform Skill may impose a tighter image budget; follow the tighter limit.
- Record platform, exact visible product title, RAM/storage, seller, displayed price, offer label and verification level. Tie these fields to the SAME visible product row or product-card parent. A query heading, generic title, nearby advertisement or unrelated row does not prove the SKU. If the tree cannot associate fields, use the app Skill's bounded visual fallback or mark that listing unverified.
- Never reconstruct a missing SKU attribute from a truncated title, nearby card, page-level shop banner or earlier listing. Missing capacity/model/seller stays unknown unless it is visible in the same card/evidence object.
- Prefer organic listings over cards explicitly labelled as ads. Ads may be reported separately when useful, but do not silently rank an ad against organic results as though the evidence class were identical.
- Separate ordinary displayed prices from coupons, trade-in, member prices and regional subsidies. Do not subtract discounts yourself or call a conditional offer an unconditional checkout price. A “from” price or unspecified SKU is not a confirmed match.
- Prices visible in search results can be reported as search-list prices. Do not call them verified checkout prices. Never invent missing product links, seller names or specifications.
- A sparse/empty result tree is not permission to scroll blindly. Follow the platform Skill's single visual/recovery path first; if it still yields no meaningful product evidence, preserve the blocker and leave that platform.
- There is no per-platform call limit. Finish when a useful match or a clear blocker is established. Take additional necessary steps when they resolve missing evidence; do not repeat unchanged actions just to keep working.

## Final report

Return a concise Chinese table for every requested platform: matching listing and seller, displayed price and conditions, evidence level, blocker if any. Mark unavailable or unverified data explicitly. Name a cheapest result only among genuinely comparable verified rows and keep any subsidy conditions visible. If a platform or SKU could not be verified, report partial completion, not a complete three-platform comparison. Respect Sofia's outcome marker contract.
