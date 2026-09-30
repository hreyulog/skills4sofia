---
name: sofia-taobao
description: Operate the native HarmonyOS Taobao app for search and read-only shopping research. Apply when the task names Taobao/淘宝 or targets com.taobao.taobao4hmos.
---

# Taobao on HarmonyOS

Package: `com.taobao.taobao4hmos`. Main ability observed: `Taobao_mainAbility`.

Use this Skill together with Sofia's phone-operation and failure-recovery rules. Never add to cart, order, pay, log in, grant permissions or accept new agreements during research.

## Page structure

Taobao exposes different amounts of semantic UI on different pages. Do not use one blanket rule for the whole app.

### Home

The current home page exposes a useful tree:

- category tabs and recommendation cards are readable;
- a search area is visible near `searchBoxPos0`;
- the right-side search action exposes visible text `搜索`.

Use tree mode here. A recommendation visible on home is not a substitute for running the user's requested search.

### Search input page

The dedicated search page currently exposes:

- `TextInput` with id/key `input`;
- a visible right-side `搜索` action;
- search-history chips such as prior Mate 80 queries.

Use the actual TextInput. Replace the old query rather than appending to a previous one. Submit through the observed search action or the phone tool's combined replace+submit path. Verify the query shown on the results header.

If submission lands on a platform risk/safety verification page (for example a route containing `punish`, `安全校验`, `验证`, slider/CAPTCHA or equivalent risk-control wording), stop automated Taobao interaction immediately. Do not drag the slider, retry the search, refresh repeatedly, request images to solve the challenge, or navigate around it. Leave the verification page intact for the human.

When this happens, tell the user exactly what is needed: complete the Taobao verification manually on the executor phone, then ask Sofia to continue. For a multi-platform task, preserve evidence already collected from other apps and continue those independent platforms before returning a PARTIAL result. For a Taobao-only task, return BLOCKED with that single next action. If a later user turn asks to continue after manual verification, reopen/observe Taobao first; if the verification page is gone and the requested query/results are visible, resume from that state instead of starting the search over.

### Search results

The results page is different: the query header remains readable, but the product grid can collapse into `Custom` nodes under containers such as `srp_waterflow_0`, with no title or price text in the UI tree.

When that happens:

1. Confirm from tree that the requested query is active and the result grid exists.
2. Request `mode: both` once for the stable first result screen.
3. Use the image to bind title, configuration, displayed price, subsidy/coupon label and shop to the SAME visible product card.
4. Keep the card geometry from the tree as a consistency check; do not mix fields from adjacent columns/cards.
5. If a second screen is necessary, do one result-page scroll, use the fresh observation, and request at most one additional image. Do not screenshot every step.

If a future Taobao version exposes full result text in tree again, prefer tree and skip the screenshot. The rule is evidence-driven, not permanently screenshot-first.

## Price evidence

- Distinguish `补贴后`, `百亿补贴`, trade-in, coupon and other conditional prices from ordinary displayed price.
- Do not infer a seller or official status from visual branding alone when the shop name is not readable.
- A `需激活`, used/refurbished, Pro or different-capacity listing is not interchangeable with a requested new standard model.
- Search-list evidence is acceptable for comparison when clearly labelled as such. Do not enter product detail only to make the report look stronger if the list already answers the task.

## Sofia PiP and overlays

Sofia may stay visible in a system PiP while Taobao is foreground.

- Keep Sofia's PiP; do not close it as part of the Taobao workflow.
- Ignore Sofia/SceneBoard text when interpreting a Taobao screenshot.
- If the PiP covers part of a product card, do not guess the hidden text. Prefer another fully visible card or move the result content once so the card becomes unobstructed.
- Clipboard/share/promotion overlays are separate windows. Dismiss an ordinary popup once if safe; login, CAPTCHA, privacy or permission choices belong to the user.

## Human verification handoff

Taobao may show a platform risk-control page with a slider, `punish` route, `安全校验`, `验证`, CAPTCHA or similar wording. Treat this as a human-only verification step.

1. Do not automate, drag or solve the slider/challenge.
2. Do not refresh, reopen Taobao, restart the search or repeatedly screenshot the challenge page.
3. Leave Taobao on the verification page and keep Sofia's PiP visible.
4. Tell the user: `淘宝需要人工验证，请在执行手机上完成滑块验证，完成后对 Sofia 说“继续”。`
5. Preserve any evidence already collected from JD or other apps.
6. On the later `继续` turn, observe Taobao before taking any action. If the verification page is gone and the requested query/results are visible, resume from that exact state. Do not submit the same search again unless the query is missing or wrong.
7. If the verification page is still present, remain blocked and repeat only the manual-action request; do not attempt the challenge yourself.

For a Taobao-only task, this is a blocker until the human finishes verification. For a multi-platform comparison, finish other independent platforms first, then report Taobao as waiting for manual verification rather than fabricating or substituting web results.

## Completion

For a normal search or comparison, two or three clearly readable matching cards are sufficient. Prefer verified card consistency over more scrolling.
