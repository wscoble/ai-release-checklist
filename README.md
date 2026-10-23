# AI Code Release Checklist

The minimum gate I want before code goes to production, whether a person wrote it or a coding agent did. It's 18 checks. Most teams already do some of them. The ones that get skipped are usually the ones that hurt later.

Copy it into a PR description, a release ticket, or a wiki page and tick through it. There's also a nicer one-page PDF version on Gumroad if you'd rather print it or pin it in a channel: [AI Code Release Checklist (free)](https://scottscoble.gumroad.com/l/ai-release-checklist).

## Spec and scope
- [ ] The change links to a written spec or ticket that has acceptance criteria.
- [ ] Every acceptance criterion is checkable: it names an observable result and how to check it.
- [ ] A named human owns this release. Not "the team" and not "the agent".

## Code and review
- [ ] Every PR in the release was approved by a human reviewer. Agent-written PRs were also checked for invented APIs or packages, tests edited to pass, and swallowed errors.
- [ ] No secrets, tokens, or credentials in the diff or the branch history.
- [ ] No test was disabled, skipped, deleted, or loosened without a linked reason.

## Tests and verification
- [ ] CI is green on the exact commit being released, and that commit SHA is recorded.
- [ ] Tests for new behavior fail without the change.
- [ ] Each acceptance criterion was demonstrated, and the evidence is linked.

## Data and migrations
- [ ] Schema changes are backward compatible with the code currently in production (expand, then contract).
- [ ] A current backup exists, and a restore from that backup system was tested in the last 90 days.

## Security and dependencies
- [ ] Every new package exists, is the one you meant, and is pinned in the lockfile.
- [ ] New endpoints and actions require the right permission, and a test proves an unauthorized user is denied.

## Observability
- [ ] Alerts exist for the failure modes that matter, go to an on-call human, and have fired at least once in testing.

## Rollout and rollback
- [ ] The rollback method is written down: the exact command or button, who can run it, and how long it takes.
- [ ] Rollback for this kind of change was rehearsed in the last 90 days, and the time was recorded.
- [ ] Rollback triggers are set in advance: thresholds that mean "roll back now, no debate".

## After release
- [ ] Acceptance criteria are re-checked in production within 30 minutes of release.

## Using it with a coding agent

[`AGENTS.md`](AGENTS.md) in this repo is a short set of rules that asks the agent to work from the spec, stay in scope, run your real checks, and finish with a Gate Report that covers the parts of this list it can actually see. Copy it into your repo root and fill in the CONFIGURE lines with your own commands. Codex, Cursor, and other tools that follow the AGENTS.md convention will pick it up.

If you want the matching `CLAUDE.md`, a Cursor rule, and the Gate Report template as a zip, that's the free Agent Gate Pack: https://scottscoble.gumroad.com/l/agent-gate-pack

The agent can't tick the whole list for you. Ownership, backups, alerts, and rollback rehearsal live outside the diff, and a human has to answer for them.

## The full kit

This is 18 of the 48 checks in **Ship-Ready: Release Gates for AI-Written Code**. The kit adds a checkable spec template, the full release checklist, a 25-point review for AI-written pull requests, a rollback rehearsal guide, a blameless postmortem template, and the complete agent files. One version, team use included: https://scottscoble.gumroad.com/l/ship-ready

## Contributing

Issues are welcome if a check is unclear or you think one is missing. I keep the list short on purpose, so not every good idea will make it in.

## License

[CC BY 4.0](LICENSE). Use it, adapt it, put it in your company wiki. Please credit "AI Code Release Checklist by Scott Scoble (Greybeard Holdings LLC)" with a link back to this repo.
