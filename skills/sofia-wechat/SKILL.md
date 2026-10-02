---
name: sofia-wechat
description: Operate HarmonyOS WeChat conversations and Moments drafts with fresh UI evidence and final Send/Publish approval.
---

# WeChat

Use the discovered `com.tencent.wechat` with phone tools. Preparation is Agent work. Final Send/Publish requires the controller approval card. Difficulty navigating is not CAPTCHA and must not request takeover.

## Screens and Sofia's window

Sofia's dot, name, progress and tool counter belong to its floating HUD, never to a WeChat profile or Moments entry. Identify it by current window bounds and role `sofia-overlay`. Never tap a covered control, even by its WeChat node. Drag the observed overlay body to a clear corner, away from close/restore buttons, and keep it visible. Do not guess missing overlay bounds.

Prefer current text nodes even if clickable=false: text often sits inside a clickable parent. For unlabeled controls request mode both, then keep mode both on visual actions until tree text is usable. All coordinates use the latest returned screen, often 720 pixels wide, not the physical display. Do not reuse coordinates after dimensions change. Changing from 720 to 1320 is not proof of a closed dialog.

After two actions show the same page, change strategy: inspect both once and use its actual current node/control. Do not repeat an unchanged coordinate followed by observe. This recovery rule does not impose a per-app call quota.

## Conversations

Find the exact requested contact in the observed chat list or search. Verify the conversation name and read the actual received message before drafting a reply. Never invent message content. If asked only to reply, draft from the visible context. Verify the recipient and exact composer text, then request final Send approval. After approval inspect again and send only that unchanged draft. Verify the sent bubble.

## Moments

Normally use the observed 发现 tab and 朋友圈 entry; these are landmarks, not fixed coordinates. The entry may be an unlabeled image row: inspect both before claiming it is absent. Seeing 视频号/小程序 alone does not prove Moments is disabled. Stop scrolling an unchanged fixed page.

The initial informational sheet says 用朋友圈记录生活 and has 我知道了. Tap its current text node and verify it disappears. This explanation is ordinary navigation, not an approval or CAPTCHA. New privacy terms or permissions still require the owner.

The feed has a profile header and top-right camera. Short-tapping the observed camera opens 拍摄 / 从手机相册选择; long-press is a text-only composition route. Use the requested route and fresh coordinates.

For a web image, download a real observed URL into a file_id. Sofia storage is not system Gallery. Use harmony_native_file_share with that file_id and inspect actual share/save destinations. Choose the requested WeChat/Moments destination if available. If saving to Gallery is required, verify the save before opening the photo picker. Never substitute another existing image or claim that a download is already in Gallery. Report the specific image-import blocker if that integration is unavailable.

Select the requested photo, finish the observed selection confirmation and write the caption. Verify the actual composer, photo(s), text and visibility. Request harmony_request_approval alone immediately before final 发表/发布. A sheet, picker or share menu is not a ready publishing draft. After approval inspect again, publish only the unchanged approved draft and verify the new post.

## Human verification

Only a currently observed CAPTCHA/verification-code challenge may use takeover with reason captcha and exact observation evidence. Saved-session continuation follows phone-operation rules. Passwords, new terms, biometric checks and permission grants require the owner directly. Publishing approval never authorizes those steps.
