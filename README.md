# Tarkle MCP server

<img src="assets/logo.png" alt="Tarkle" width="64" height="64">

Tarkle is AI-powered storage for business files. Teams keep their working files there: product specs, client briefs, contracts, brand assets, exports, reports and project handoffs. The Tarkle MCP server lets an AI assistant find, read and deliver those files: search inside them, answer questions with the file and page of each source, upload files with SHA-256 checks, edit PDF and Office files, send share links and request files from clients.

- Server: `https://mcp.tarkle.tech/mcp` (Streamable HTTP)
- Sign-in: OAuth 2.1 with your own Tarkle account (dynamic client registration, PKCE). No API key.
- Website: https://tarkle.tech
- Docs: https://tarkle.tech/docs/mcp

This repository holds the Gemini CLI extension and the client setup. The server itself is hosted by Tarkle; there is nothing to install or run.

## What you can do

- **Find any file.** Search the words inside PDFs, Word files and text across a workspace, then read the passage you need into your session. Recordings are read as timestamped transcripts.
- **Get answers from your files.** Ask a question and get an answer written from your files, with the file and page of each source.
- **Work with documents.** Convert files, run OCR, redact, compress, and merge, split or reorder PDF pages. Every edit is saved as a new file.
- **Keep files in order.** Upload, rename, move and copy files, rename and move folders, add tags and descriptions, and restore an earlier version (Pro). Files you remove go to the recovery bin and can be restored.
- **Deliver files.** Send a build, an export or a report with a share link, list the links you already sent, put a file in a client's portal, or ask a client for missing files with an upload link.
- **Set up a workspace.** Create a workspace in the region you choose, change its settings, logo and address, connect a custom domain, and manage invitations and contacts.
- **See what happened.** Read the activity log: who viewed, downloaded, moved or shared a file, and when. Check storage and AI credits left.

The assistant acts as you, within your role in each workspace. It asks before it creates a public link or file request, moves files to the bin, or changes workspace settings, members, invitations, domains or portal access. A workspace owner can turn off groups of actions for AI agents and hide folders from them.

## Install

### Gemini CLI

```bash
gemini extensions install https://github.com/tarkleHQ/tarkle-mcp-server
```

Start Gemini CLI and ask "List my Tarkle workspaces". A browser tab opens on the first tool call: sign in to Tarkle and approve the connection. If the sign-in does not finish, run `/mcp auth tarkle`.

### Claude Code

```bash
claude mcp add --transport http tarkle https://mcp.tarkle.tech/mcp
```

### Cursor

Add to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "tarkle": { "url": "https://mcp.tarkle.tech/mcp" }
  }
}
```

### VS Code

Add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "tarkle": { "type": "http", "url": "https://mcp.tarkle.tech/mcp" }
  }
}
```

### Kiro

Install the Tarkle power: https://github.com/tarkleHQ/tarkle-for-kiro

### Any other MCP client

Add a remote (Streamable HTTP) MCP server with the URL `https://mcp.tarkle.tech/mcp`. The client opens the Tarkle sign-in on first use. More clients: https://tarkle.tech/docs/mcp.

## Tools

The table lists the 102 tools of the Tarkle MCP server. Your assistant gets the tools the hosted server offers at the time: ask it to list the Tarkle tools to see them. Which ones a person can use depends on their role in each workspace and on what the workspace owner allows AI agents to do.

| Area | Tools |
| --- | --- |
| Account and workspaces | `tarkle_whoami`, `tarkle_list_workspaces`, `tarkle_get_usage`, `tarkle_list_regions`, `tarkle_create_workspace`, `tarkle_check_workspace_url`, `tarkle_set_workspace_url`, `tarkle_get_workspace_settings`, `tarkle_update_workspace_settings`, `tarkle_set_workspace_logo`, `tarkle_connect_workspace_domain`, `tarkle_check_workspace_domain`, `tarkle_remove_workspace_domain`, `tarkle_get_organization`, `tarkle_update_organization`, `tarkle_set_organization_logo` |
| Find and read | `tarkle_list_files`, `tarkle_list_folders`, `tarkle_search_files`, `tarkle_read_file`, `tarkle_get_download_link`, `tarkle_get_activity`, `tarkle_get_received_emails` |
| Answers and data | `tarkle_ask`, `tarkle_extract_data`, `tarkle_get_extraction`, `tarkle_split_document` |
| Add files | `tarkle_upload_text`, `tarkle_upload_file`, `tarkle_upload_from_url`, `tarkle_start_upload`, `tarkle_get_upload_parts`, `tarkle_get_upload_status`, `tarkle_get_upload_page` |
| Documents | `tarkle_create_document`, `tarkle_fill_template`, `tarkle_edit_office_file`, `tarkle_edit_pdf`, `tarkle_convert_file` |
| Organize | `tarkle_create_folder`, `tarkle_rename_file`, `tarkle_move_file`, `tarkle_copy_file`, `tarkle_rename_folder`, `tarkle_move_folder`, `tarkle_list_versions`, `tarkle_restore_version`, `tarkle_delete_files`, `tarkle_list_bin`, `tarkle_restore_from_bin` |
| Tags and descriptions | `tarkle_update_details`, `tarkle_list_tags`, `tarkle_rename_tag`, `tarkle_delete_tag` |
| Share links and galleries | `tarkle_create_transfer`, `tarkle_list_transfers`, `tarkle_update_transfer`, `tarkle_deliver_transfer_to_contacts`, `tarkle_create_gallery`, `tarkle_get_gallery_status` |
| File requests | `tarkle_create_file_request`, `tarkle_list_file_requests`, `tarkle_get_file_request_submissions`, `tarkle_close_file_request`, `tarkle_reopen_file_request`, `tarkle_delete_file_request` |
| Contacts and client portal | `tarkle_list_contacts`, `tarkle_create_contact`, `tarkle_update_contact`, `tarkle_add_contact_to_organization`, `tarkle_set_portal_access`, `tarkle_resend_portal_invite`, `tarkle_set_portal_storage_limit` |
| People and teams | `tarkle_list_members`, `tarkle_list_roles`, `tarkle_invite_member`, `tarkle_change_member_role`, `tarkle_remove_member`, `tarkle_list_invitations`, `tarkle_resend_invitation`, `tarkle_cancel_invitation`, `tarkle_list_team_folders`, `tarkle_create_team_folder`, `tarkle_add_member_to_team_folder`, `tarkle_remove_member_from_team_folder`, `tarkle_set_team_folder_budget` |
| Brand pages | `tarkle_list_brands`, `tarkle_get_brand`, `tarkle_create_brand`, `tarkle_update_brand`, `tarkle_import_brand_file`, `tarkle_lookup_brand_domain`, `tarkle_connect_brand_domain`, `tarkle_check_brand_domain`, `tarkle_disconnect_brand_domain` |
| Webhooks | `tarkle_list_webhooks`, `tarkle_create_webhook`, `tarkle_update_webhook`, `tarkle_delete_webhook`, `tarkle_test_webhook`, `tarkle_get_webhook_deliveries` |
| Feedback to Tarkle | `tarkle_report_feedback` |

## Safety

- Every call runs as the signed-in person, within their role in each workspace (owner, admin, member or viewer).
- Tools that create a public link or file request, move files to the bin, or change workspace settings, members, invitations, domains or portal access ask for confirmation first: the first call returns a preview and a code, and nothing happens until the call is repeated with the person's approval.
- A workspace owner can turn off groups of actions for AI agents and hide folders from them (Settings > AI agents).
- File names and contents are returned marked as data, never as instructions.
- Deleted files go to the recovery bin and can be restored.

## Contents

| Path | What it is |
| --- | --- |
| `gemini-extension.json` | Gemini CLI extension manifest: the Tarkle server |
| `GEMINI.md` | How the assistant uses Tarkle's tools |
| `assets/logo.svg`, `assets/logo.png` | Tarkle logo (SVG, and PNG at 816 x 816) |

## Privacy and support

- Privacy Policy: https://tarkle.tech/privacy
- Terms: https://tarkle.tech/terms
- Support: support@tarkle.tech or https://tarkle.tech/contact

## License

Apache License 2.0. See [LICENSE](LICENSE).
