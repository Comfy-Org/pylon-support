# Settings

Copy this file to `config.md` and fill it in. `config.md` is not tracked.

## Shared by the team

| Setting | Value |
|---|---|
| Pylon ticket link | `https://app.usepylon.com/support/issues/views/<view id>?issueNumber=N` |
| Pylon view link | `https://app.usepylon.com/support/issues/views/<view id>` |
| Comfy Admin user search | `<admin user search URL>` |
| Comfy Admin workspace page | `<admin workspace URL pattern>` |
| Stripe customer page | `https://dashboard.stripe.com/<stripe account id>/customers/<customer id>` |
| Stripe payment page | `https://dashboard.stripe.com/<stripe account id>/payments/<payment id>` |
| Stripe account id | `<acct_...>` |
| Bug channel | `<#channel>` (`<channel id>`) |
| Skill update channel | `<#channel>` (`<channel id>`) |
| Team, for watcher reports | `<name>` `<Pylon user id>` · `<name>` `<Pylon user id>` |

## Per person

| Setting | Value |
|---|---|
| Owner | `<your name>` |
| Owner's Pylon user id | `<Pylon user id>` |
| Pylon view id | `<view id>` |
| Watcher state folder | `<full path of a folder the watcher may write to>` |
| Word that lets the agent press the final Delete account button | `<a word you would not type by accident>` |

## Preferences

Defaults are shown. The skill updates this table when the owner asks for something to be done a particular way.

| Preference | Value |
|---|---|
| Fill refund, credit and deletion dialogs | Only when asked |
| Where tabs open | Claude's own tab group |
| Watcher report style | Tables, as in `references/watcher.md` |

## Shorthand

What the owner types and what it means. Edit to match how you talk.

| The owner types | Meaning |
|---|---|
| "ok", "ok send", "ok for N", "ok for both" | Send that draft on that ticket (or those two). |
| "no, just send" | Send the draft as it stands. |
| "redraft …" | Apply the change and show the whole draft again. |
| "next", "move on" | Present the next ticket. |
| "closed, move on" | They closed it themselves; close its tabs and go to the next. |
| "close it, assign to me" / "close with no reply, don't assign to me" | Close as worded (SKILL.md section 8). |
| "assign yourself N" / "assign yourself unassigned" | Assign those tickets to the owner (SKILL.md section 2). |
