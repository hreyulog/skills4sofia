---
name: sofia-pinduoduo
description: Search and read product evidence in the installed HarmonyOS Pinduoduo app. Apply for 拼多多/Pinduoduo or com.xunmeng.pinduoduo.hos.
---

# Pinduoduo shopping research

Discovered package: `com.xunmeng.pinduoduo.hos`. Discover the installed app; do not assume an ability or use an invented deep link. Follow phone-operation, failure-recovery and price-comparison Skills. No cart, order or payment actions during research.

Open -> observed search field/action -> observed editable input with replace+submit -> inspect product results -> at most one scroll -> finish. Home has previously exposed `搜索你要的商品`; that is a recognition hint, not a fixed node ID or coordinate. Use fresh observations to identify the real input. Do not confuse 拼小圈, camera/image search or recommendations with text search. Never retry the same unchanged control more than twice.

Verify the actual query before reporting product evidence. Prefer tree text when it associates title, configuration, price conditions and seller within ONE card. If a confirmed result page contains custom/opaque cards, request `both` once and read the real image; do not swipe an unconfirmed sparse screen. One second image after the single result scroll is permitted if it yields needed evidence. Missing or hidden SKU fields stay unverified.

## Saved login and blockers

The owner permits reuse of an existing saved login for shopping research. A login banner alone does not prove research is blocked: read whether results and controls remain available first.

- If a login page offers an observed existing-account/session continuation or saved-login action that needs no password entry, verification code, biometric confirmation, new agreement, permission or new account linkage, attempt that restoration ONCE. Use only the account already shown; never guess an account or retrieve credentials. A prefilled phone number alone is not a saved authenticated session.
- Verify the returned observation: login UI must disappear and the requested app/search must be visible. A click acknowledgement alone is not successful login. If a stale action was skipped, do not repeat it as a login attempt.
- If restoration still shows login, needs human input, or no eligible saved-login control exists, record the blocker and move to the next requested platform immediately. Do not tap around the login page, Back and resubmit the search, or try a different login method.
- CAPTCHA, risk verification, payment and new consent remain human steps. For a multi-platform comparison finish independent platforms before asking for manual help, rather than pausing the whole task at the first blocker.

## Completion

There is no per-app call quota; continue necessary steps while actual task progress is visible. Search-list evidence is sufficient. Distinguish 百亿补贴, coupons, group-buy and new-user offers from ordinary prices; do not compute an assumed checkout price. Stop at useful exact evidence or a clear blocker. Preserve this result in the task ledger and return a Chinese comparison covering every requested platform, including partial/blocked entries.
