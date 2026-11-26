---
name: tarkle-get-started
description: First steps after connecting Tarkle. Use this skill right after the user connects Tarkle, or when they ask what Tarkle can do, which workspaces they can use, or how to get started with their files in Tarkle.
---

# Get started with Tarkle

Help the user check their connection and take a first useful action. Keep it short: one message with what you found and two or three things they can try next.

## 1. Check the connection

1. Call `tarkle_whoami` to see who is signed in. It also gives the plan of the organization they own, or null when they own none.
2. Call `tarkle_list_workspaces` to see the workspaces they can reach, their role in each, and `canShare`.

If either call fails because the user is not signed in, ask them to reconnect Tarkle and sign in with their Tarkle account. If they have no workspace, tell them to create one at https://tarkle.tech first.

## 2. Tell the user what you found

- Their name, and the plan of the organization they own if there is one. A workspace they joined can be on another plan, and `tarkle_whoami` does not say which, so do not state a plan for it.
- Each workspace with their role. Say which ones allow uploads and share links (`canShare` true). Uploading and creating links or file requests only work there.

Do not guess prices, limits or plan features. If an action fails because the workspace's plan does not include it, pass on what Tarkle's answer says.

## 3. Offer a first action

Suggest two or three of these, using the user's own workspace names:

- Find something inside their files: `tarkle_search_files`, then `tarkle_read_file` to read more of a match. It returns about 12,000 characters per call; when it says the text is truncated, read a PDF in page ranges (`fromPage`, `toPage`). For other formats, say that only the first part was read, and offer `tarkle_get_download_link` so the user can open the whole file.
- Ask a question answered from their files, with sources: `tarkle_ask`.
- Save notes or a report as a file: `tarkle_upload_text`.
- Share files by link: `tarkle_create_transfer`.
- Collect files from a client with an upload link: `tarkle_create_file_request`.

## Confirmation

Many tools ask for confirmation first, including creating share links and file requests, deleting files, and changes to members or settings. Their first call changes nothing and describes what will happen. Show that to the user, wait for a clear yes, then call again with the same inputs and the `confirmationCode` from the first answer. Never send a `confirmationCode` the user has not approved.

Other tools act on the first call, for example `tarkle_close_file_request`, which stops a request's link from accepting uploads, and renames, moves and uploads. Before calling a tool that changes something, check its description: if it does not mention a `confirmationCode`, ask the user first yourself.
