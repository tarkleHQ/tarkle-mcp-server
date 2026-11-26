---
name: tarkle-get-started
description: First steps after connecting Tarkle. Use this skill right after the user connects Tarkle, or when they ask what Tarkle can do, which workspaces they can use, or how to get started with their files in Tarkle.
---

# Get started with Tarkle

Help the user check their connection and take a first useful action. Keep it short: one message with what you found and two or three things they can try next.

## 1. Check the connection

1. Call `tarkle_whoami` to see who is signed in and their plan.
2. Call `tarkle_list_workspaces` to see the workspaces they can reach, their role in each, and `canShare`.

If either call fails because the user is not signed in, ask them to reconnect Tarkle and sign in with their Tarkle account. If they have no workspace, tell them to create one at https://tarkle.tech first.

## 2. Tell the user what you found

- Their name and plan.
- Each workspace with their role. Say which ones allow uploads and share links (`canShare` true). Uploading and creating links or file requests only work there.

Do not guess prices, limits or plan features. If the user asks, read https://tarkle.tech/pricing.md and say that you used it.

## 3. Offer a first action

Suggest two or three of these, using the user's own workspace names:

- Find something inside their files: `tarkle_search_files`, then `tarkle_read_file` for the full text.
- Ask a question answered from their files, with sources: `tarkle_ask`.
- Save notes or a report as a file: `tarkle_upload_text`.
- Share files by link: `tarkle_create_transfer`.
- Collect files from a client with an upload link: `tarkle_create_file_request`.

## Confirmation

Share links, file requests, deletions and other changes that affect people or settings ask for confirmation first. The first call changes nothing and describes what will happen. Show that to the user, wait for a clear yes, then call again with the same inputs and the `confirmationCode` from the first answer. Never send a `confirmationCode` the user has not approved.
