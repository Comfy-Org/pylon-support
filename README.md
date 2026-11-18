# pylon-support

A Claude Code skill for working Comfy support tickets in Pylon, one ticket at a time, with a person approving every reply and every action.

## What it does

- Presents each ticket with its account, payments, tracking status, sourced facts and a draft reply.
- Sends, closes and assigns only on the owner's go for that ticket.
- Prepares refund, credit and deletion dialogs when asked, stopped one click short.
- Includes a read-only queue watcher that reports what changed, in tables.

## What it needs

| Needs | Used for | Required |
|---|---|---|
| Claude Code, with scheduled prompts and sub-agents | Running the skill; the watcher | Yes |
| Pylon connector | Reading tickets, sending replies, closing, assigning, the watcher | Yes |
| Claude in Chrome | Opening the ticket, Comfy Admin and Stripe pages; filling dialogs | Yes |
| Comfy Admin access | Account, plan, credits, recent jobs | Yes |
| Stripe connector and a Stripe dashboard login | Charges, refunds and subscription state | For billing tickets |
| Linear connector | Whether a bug is already tracked | For bug tickets |
| Datadog connector | How widespread a fault is and since when | For bug tickets |
| Slack connector | Searching earlier discussion (read-only) | Optional |
| Comfy Cloud connector | Whether a model, node or template is on Cloud | Optional |
| Web access | Docs, the Registry API, public GitHub | Optional |

## What it does in your browser

- Every tab it opens goes in Claude's own tab group. It does not open, move or close tabs in your windows.
- For each ticket it opens the Pylon ticket, the customer's Comfy Admin page, the workspace page, and the Stripe customer page when billing is involved.
- It types the customer's email into the Comfy Admin search, and runs a read-only script in a Pylon view tab to read ticket order.
- It may open cloud.comfy.org to read the build or reproduce a fault.
- It fills a refund, credit or deletion dialog only when you ask, and never presses the final button unless you tell it to for that ticket.
- It closes a ticket's tabs after the reply is sent or the ticket is closed.

## Install

```sh
git clone https://github.com/Comfy-Org/pylon-support ~/.claude/skills/support
cd ~/.claude/skills/support
cp config.example.md config.md
```

Fill in `config.md`, add your team's files (below), then start with `/support`.

## Update

```sh
git -C ~/.claude/skills/support pull --ff-only
```

Your `config.md` and team files are not in the repo, so an update does not touch them. The skill also checks at the start of each session whether it is out of date and offers to update.

## Changing the skill

Propose a change as a pull request for a maintainer to review and merge. The skill offers one whenever it changes a file tracked in this repo. It opens one only on your go, and merges one only when you tell it to for that pull request.

## Files

| File | Purpose |
|---|---|
| `SKILL.md` | The per-ticket procedure. |
| `config.example.md` | Template for ids, links, preferences and shorthand. |
| `references/watcher.md` | The queue watcher. |
| `references/view-order.md` | Reading ticket order from a Pylon view. |

Team files are not in this repo. Get them from your team and put them in `references/`:

| File | Purpose |
|---|---|
| `refunds.md` | Refunds, credit changes, subscription cancels. |
| `deletions.md` | Account deletion requests. |
| `house-answers.md` | Agreed answers for recurring questions. |
| `local-rules.md` | Any other rules internal to the team. |

Without a team file, the skill prepares no action of that kind and says the file is missing.
