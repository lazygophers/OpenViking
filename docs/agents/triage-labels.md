# Triage Labels

The skills speak in terms of five canonical triage roles. This file maps those roles to the actual strings used in this repo's issue tracker.

| Role | String in our tracker | Meaning                                  |
| ---- | --------------------- | ---------------------------------------- |
| `needs-triage`    | `needs-triage`    | Maintainer needs to evaluate this issue  |
| `needs-info`      | `needs-info`      | Waiting on reporter for more information |
| `ready-for-agent` | `ready-for-agent` | Fully specified, ready for an AFK agent  |
| `ready-for-human` | `ready-for-human` | Requires human implementation            |
| `wontfix`         | `wontfix`         | Will not be actioned                     |

This repo uses the local-markdown tracker, so the string is written as the value of the `Status:` line near the top of the issue file, not applied as a GitHub label.

When a skill mentions a role (e.g. "apply the AFK-ready triage label"), use the corresponding string from the "String in our tracker" column.

Edit that column to match whatever vocabulary you actually use.
