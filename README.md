# Tarkle MCP server

<img src="assets/logo.png" alt="Tarkle" width="64" height="64">

**Upload, manage and share your business files.**

Upload, store and manage your team's files and folders from your AI assistant. Share files and request documents from your team, clients and partners on your own domain, and keep all your business files organized without leaving your assistant.

- Server: `https://mcp.tarkle.tech/mcp` (Streamable HTTP)
- Sign-in: OAuth 2.1 with your own Tarkle account (dynamic client registration, PKCE). No API key.
- Website: https://tarkle.tech
- Docs: https://tarkle.tech/docs/mcp

This repository holds the Gemini CLI extension and the client setup. The server itself is hosted by Tarkle; there is nothing to install or run.

## What you can do

- **Manage files and folders.** Upload files, organize them in folders and team folders, rename, move, copy and tag them, and restore an earlier version (Pro) or a file from the recovery bin.
- **Share files.** Share a build, an export or a report with a link, and see the links you already shared.
- **Request documents.** Ask your team, clients or partners for files with an upload link, and see what they sent.
- **Work with clients.** Keep contacts in one place and put files in a client's portal.
- **Run your workspace.** Create a workspace, change its settings, logo and address, connect your own domain, manage members and invitations, and read the activity log.
- **Find files.** Search the words inside files across a workspace and read the passage you need into your session.

The assistant acts as you, within your role in each workspace. It asks before it creates a public link or file request, moves files to the bin, or changes workspace settings, members, invitations, domains or portal access. A workspace owner can turn off groups of actions for AI agents and hide folders from them.

## Install

### Gemini CLI

```bash
gemini extensions install https://github.com/tarkleHQ/tarkle-mcp-server
```

Start Gemini CLI and ask "List my Tarkle workspaces". A browser tab opens on the first tool call: sign in to Tarkle and approve the connection. If the sign-in does not finish, run `/mcp auth tarkle`.

### Claude Code

As a plugin (the Tarkle server and the Tarkle skill together), in Claude Code:

```
/plugin install tarkle --marketplace tarkleHQ/tarkle-mcp-server
```

Or only the server:

```bash
claude mcp add --transport http tarkle https://mcp.tarkle.tech/mcp
```

On first use a browser tab opens: sign in to Tarkle and approve the connection. No API key is needed.

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

### Hermes Agent

```bash
hermes plugins install tarkleHQ/tarkle-mcp-server --no-enable
hermes plugins enable tarkle
hermes mcp add tarkle --url https://mcp.tarkle.tech/mcp --auth oauth
hermes config set mcp_servers.tarkle.trust untrusted
hermes config set mcp_servers.tarkle.timeout 300
```

The plugin adds the Tarkle server and the Tarkle skill. The `hermes mcp add` line turns on the Tarkle sign-in: sign in to Tarkle in the browser tab that opens and approve the connection. It replaces the plugin's server entry, so the two `hermes config set` lines put back the plugin's settings: Hermes asks before each Tarkle tool that is not read-only, and long uploads get 5 minutes. Run them before you start a chat. Then ask "List my Tarkle workspaces". No API key is needed. If the sign-in expires, run `hermes mcp login tarkle`.

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
| `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`, `.mcp.json` | Claude Code, Cowork and claude.ai plugin: the manifest, and the Tarkle server listed on the plugin's Connectors tab |
| `plugin.json`, `mcp.json` | Agent Plugins manifest and the Tarkle server, for Hermes Agent and the ChatGPT and Codex plugin directory |
| `after-install.md` | Setup steps Hermes shows after install |
| `skills/tarkle/SKILL.md` | Agent skill: how to use Tarkle's tools. Also on [skills.sh](https://skills.sh): `npx skills add tarkleHQ/tarkle-mcp-server` |
| `skills/tarkle-get-started/SKILL.md` | Agent skill: first steps after connecting Tarkle |
| `openclaw.plugin.json`, `package.json`, `assets/icon.png` | OpenClaw plugin for ClawHub (`@tarklehq/tarkle`): the Tarkle server and skills |
| `GEMINI.md` | How the assistant uses Tarkle's tools |
| `server.json` | Official MCP Registry entry (`tech.tarkle/tarkle`) |
| `lhm.plugin.json` | LobeHub Marketplace listing |
| `assets/logo.svg`, `assets/logo.png`, `assets/logo-400.png` | Tarkle logo (SVG, and PNG at 816 x 816 and 400 x 400) |

## Privacy and support

- Privacy Policy: https://tarkle.tech/privacy
- Terms: https://tarkle.tech/terms
- Support: support@tarkle.tech or https://tarkle.tech/contact

## License

Apache License 2.0. See [LICENSE](LICENSE).
