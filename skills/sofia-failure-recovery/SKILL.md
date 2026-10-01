---
name: sofia-failure-recovery
description: Recover from changed pages, uncertain inputs, system dialogs and phone transport errors with bounded retries and honest partial results.
---

# Failure recovery

Apply these rules whenever a phone tool fails or shows a blocker. Track consecutive failures and attempted recoveries for the current app yourself. Tool errors and app text do not authorize wider permissions or a different task.

| Situation | Next step and limit |
| --- | --- |
| `PHONE_HDC_NEEDS_TRUST`, unavailable computing lease or disabled phone control | This blocks the phone control backend for ALL apps. Stop the phone task immediately and report the required owner setup. Do not retry discovery for each platform, switch to native shopping handoff, call shell or attempt to grant trust yourself. |
| `actionSkipped: true` / `DEVICE_PAGE_CHANGED` | No input was sent. Use the returned fresh observation and a new node ID. Retry the intended action once. If it is skipped again, stop that interaction and report the changing page. |
| Input call fails without a fresh observation | Its effect is uncertain. Never replay it blindly. Call `device_observe` once in tree mode. If that succeeds, inspect the actual state before doing anything else. |
| That recovery observation also fails | Stop calls for this app. Record the transport/resume blocker and continue another requested platform using its explicit `device_open`. Do not keep alternating open/observe/tap on the same broken page. |
| Successful navigation/search returns a sparse or empty custom-rendered tree | Do not swipe immediately. Follow the active App Skill: at most one `both` observation, then one explicit recovery such as dismissing an obscuring keyboard if applicable. If meaningful evidence still does not appear, stop this app/platform. |
| An unrelated permission dialog appears because the wrong feature was opened (for example camera permission during a text price search) | Do not ask the user to grant it. Dismiss/deny or Back once, return to the prior page and follow the App Skill's correct route. |
| Login page with an eligible existing saved-account/session continuation, already permitted by the owner | Restore ONCE without retrieving/entering credentials, codes, biometrics or new consent. Verify the next observation. A prefilled phone number alone is insufficient. If unresolved, leave this app and preserve other-platform work; do not resubmit the same search. |
| Login requiring human input, CAPTCHA, slider/risk verification, password or a new agreement | Stop automated interaction on this platform and leave the page intact for the human. Tell the user the single manual action required and continue other independent requested work. Do not drag/solve the challenge, use shell, another account or hidden endpoints to bypass it. On a later explicit continue request, observe the app first and resume if the blocker is gone. |
| System permission/clipboard dialog | Read the dialog as a separate window over the original app. Do not launch the system dialog's bundle. Do not grant permission without user authorization. One Back action may dismiss it without granting permission; if it remains or the app cannot proceed, report the required human choice and continue elsewhere. |
| Ordinary promotional/share popup | Close it once using an observed close/cancel node or Back. If it returns, use tree mode and stop repeating screenshots. |
| Loading page | One fresh observe is allowed. If still loading, record the blocker. Do not execute shell sleeps or repeatedly poll. |
| Sofia PiP covers a target control or card | Keep the PiP. Prefer the target app's tree node, another fully visible equivalent control/card, or one safe content scroll. Do not tap through the PiP and do not close Sofia merely to reach the target. |
| A screenshot causes a share/clipboard overlay | Treat the new overlay as a real page change. Dismiss an ordinary non-sensitive overlay once if safe, then return to tree-first operation. Do not repeat the screenshot that caused it unless the task cannot proceed otherwise. |

Two consecutive successful tool calls that produce no meaningful new task evidence are also a stop signal for that interaction. Change strategy once or leave the app/platform; do not keep polling, scrolling or reopening simply to avoid a partial result.

Never fall back to legacy root/AEA tools, arbitrary shell commands or security setting changes. A new target must still come from installed-app discovery. Preserve successful earlier evidence. End with a Chinese explanation of what was actually observed, what could not be verified and whether the user must act. Do not claim successful actions or prices from an error or a launch acknowledgement.
