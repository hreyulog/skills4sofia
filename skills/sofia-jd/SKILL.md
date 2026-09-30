---
name: sofia-jd
description: Operate the native HarmonyOS JD app for search and read-only shopping research. Apply when the task names JD/京东 or targets com.jd.hm.mall.
---

# JD on HarmonyOS

Package: `com.jd.hm.mall`.

Use this Skill together with Sofia's phone-operation and failure-recovery rules. This is a read-only workflow unless a later task explicitly obtains approval for a side effect. Never add to cart, order, pay, log in, grant permissions or accept new agreements during research.

## Recognize the page before acting

- A cold JD launch can briefly expose only system/status-bar nodes. Do not call that a broken or empty app. Allow one fresh tree observation for the page to settle.
- On the home page, the search frame has been observed around `TN003_search_frame`, with a separate `TN003_search_btn` search button.
- The dedicated search page exposes its query field as a `TextArea`; it may not advertise `editable=true` even though it is the real text-entry control.
- A search-results page should expose the current query in the top search area before the result list. Verify the query before treating any listing as evidence.

## Search efficiently

1. Open the full JD app returned by app discovery. Do not choose an atom service or browser substitute when the user asked for JD.
2. On home, open the observed search frame.
3. Use one continuous type action on the observed search input: replace the old query and submit in the same phone-tool call when possible. Do not split select-all, typing and submit across multiple rounds; the keyboard/page can change between those actions.
4. After submission, plan directly from the fresh returned observation. Only use one extra observe when the results are still loading.
5. Do not use the legacy JD deep-link shopping adapter as a hidden substitute for the normal app workflow.

## Read result cards from the tree

JD's current HarmonyOS result list exposes strong tree evidence. Prefer `mode: tree` and avoid screenshots unless the tree genuinely lacks the needed result text.

- A product card can expose a clickable parent such as `card_content`.
- Bind title, displayed price, offer label, crossed/original price, sales and rating only when they are descendants of the SAME product-card parent.
- Store/shop text such as `card_shop_name` must be associated with that same card before reporting it.
- Examples of labels that are price conditions rather than unconditional checkout prices include `国补到手价`, `补贴价`, coupons, trade-in and member offers.
- A title containing Mate 80 Pro, refurbished/used wording, a different capacity, or an accessory is not a match for a requested standard Mate 80 SKU.
- Search-list evidence is enough for a read-only comparison. Enter at most one product detail per platform only when the task truly needs detail-level evidence and the page is not blocked by login.

## Screenshot and Sofia PiP

JD screenshots have previously triggered a share panel. Therefore:

- Stay tree-first on JD. Do not request an image merely because the result is visually rich.
- If one image is genuinely required, request it once, inspect it, then return to tree mode.
- Sofia may remain visible as a system PiP/SceneBoard window while JD is the real foreground app. Do not close Sofia's PiP. Do not treat text inside the PiP as JD content.
- If the PiP visually covers a control, prefer its tree node or move JD content with one safe scroll so the target is no longer underneath the PiP. Do not tap through the PiP region.

## Completion

For a normal price lookup, 1–3 clearly matched search-list cards are enough. Report exact visible titles, configuration, displayed price, price condition and seller/channel. Do not keep scrolling merely to find a lower number after enough comparable evidence has been collected.
