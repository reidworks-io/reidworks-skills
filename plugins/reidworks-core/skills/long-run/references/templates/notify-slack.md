<!-- Paste this block as the {{notification-block}} in orchestrator-prompt.md
     if the user wants per-cycle Slack DMs. Requires the Slack MCP server
     (mcp__claude_ai_Slack__*) to be configured in this session.

     IMPORTANT — headless-mode trap (see SKILL.md Known traps #4):
     `claude -p` running non-interactively often ships with a narrower
     default toolset; deferred MCP tools (including Slack) may not be
     auto-loaded. If the orchestrator runs via launchd / cron / a remote
     routine, test the Slack path from a non-interactive Claude session
     (`claude -p "use the Slack MCP to send a test message"`) BEFORE
     kickoff. If the tool isn't pre-loaded, either prepend a ToolSearch
     step to this block or treat DIGEST.md as the only heartbeat and
     drop the Slack step entirely. Running the orchestrator via /loop
     in an interactive session avoids this trap. -->

7. **Slack the user with the cycle outcome.** Use
   `mcp__claude_ai_Slack__slack_send_message` to DM `{{user-email}}`.
   One message per cycle, every cycle — including `no work available`
   and STOP-file exits. Format:
   - **First line:** `<milestone-id> <outcome>` where outcome is one of
     `merged`, `blocked`, `contract-violation`, `no work`, `stopped`.
     For `no work` and `stopped`, omit the milestone-id.
   - **Gate line** (when a milestone ran): `gates: test <ok|FAIL>,
     typecheck <ok|FAIL>, lint <ok|FAIL>, build <ok|FAIL>` and the
     Playwright smoke line for app milestones.
   - **Diagnosis or PR line:** for `merged`, the PR URL. For `blocked` /
     `contract-violation`, a one-sentence diagnosis +
     `see .agents/BLOCKED.md`.
   - **Resolve the DM channel each cycle:** call `slack_search_users`
     with `{{user-email}}` if you don't already have the user ID in
     this session, then send the DM. If Slack send fails (auth,
     rate-limit, anything): log the failure to `DIGEST.md` and
     continue — never block the cycle on Slack delivery.
