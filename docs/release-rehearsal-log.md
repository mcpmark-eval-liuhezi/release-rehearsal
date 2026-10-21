# Release rehearsal log

Dress rehearsal of the full GitHub release flow for the internal tooling, run ahead of the first real release next month. This is the reusable runbook for the real release.

- **Rehearsal repo:** https://github.com/mcpmark-eval-liuhezi/release-rehearsal (org `mcpmark-eval-liuhezi`, default branch `main`)
- **Deviations to know about:** repo creation under the personal account was blocked by the access token (403), so the rehearsal ran in the pre-existing scratch org repo of the same name; that repo's visibility is **public**, not private (no tool available to flip it). Gist creation is likewise blocked by the token (403), so the runbook was saved as this repo file instead of a gist. Everything else in the flow was exercised exactly as specified.

## Ordered log of what was done

1. **Repo:** `release-rehearsal` confirmed in place, initialized with `README.md`; default branch `main`.
2. **Branch:** `rehearsal/release-checklist` cut from `main`.
3. **File:** `docs/release-checklist.md` added on the branch — release checklist covering CI green, changelog updated, release tag created, release notes published (full content below).
4. **Pull request:** #3 "Add release checklist (dress rehearsal)" opened from `rehearsal/release-checklist` into `main`.
5. **Review:** a **COMMENT** review was left on #3 (the PR author cannot approve their own PR). Body starts with "Dress rehearsal review:" followed by notes on the change (full text below).
6. **Merge:** #3 was merged into `main` — merge commit `f9da1f2e95f08b8e59d42e2daa8a0ebbcdedc7d1`, diff = `docs/release-checklist.md` added (+25 lines), nothing else touched.
7. **Post-merge confirmation:** `docs/release-checklist.md` retrieved directly from `refs/heads/main` — the checklist is confirmed present on the default branch.
8. **Pre-release inventory:** releases list and discussions checked on the repo — findings below.
9. **Gap issues:** six issues filed (#4–#9), each its own issue, covering CI workflow, release-notes template, CHANGELOG.md, Discussions being disabled, branch protection, and stale-artifact cleanup.
10. **Tracking issue:** #10 "Rehearsal cleanup: delete the scratch repo" created, all six gap issues attached as its sub-issues, and a completion comment posted ("rehearsal complete, repo can be deleted once reviewed").

## Pull request reference

- **PR #3** — https://github.com/mcpmark-eval-liuhezi/release-rehearsal/pull/3
- Title: "Add release checklist (dress rehearsal)"
- State: closed/merged at 2026-10-21T18:04:34Z
- Head: `rehearsal/release-checklist` @ `4fa2857` → Base: `main`

## Review left on PR #3 (COMMENT review, submitted 2026-10-21T18:04:17Z)

> Dress rehearsal review: This PR is a rehearsal exercise, not a production change — nothing here needs approval in the normal sense. Notes on the change itself: the new `docs/release-checklist.md` covers the four required gates (CI green, changelog updated, release tag created, release notes published) and adds pre-release verification, release, post-release, and sign-off sections. Content is checklist-only with no code or workflow changes, so no functional risk. Two observations for the real release: (1) there is no CI workflow in this repo yet, so the "CI green" gate currently has nothing to run — a gap worth filing before the real release; (2) release notes currently have no template, so notes would be written from scratch on release day. Leaving this as a COMMENT review since the PR author cannot approve their own pull request; proceeding to merge as part of the rehearsal.

## Merge result

- **Merged.** PR #3 closed via merge at 2026-10-21T18:04:34Z.
- Merge commit: `f9da1f2e95f08b8e59d42e2daa8a0ebbcdedc7d1` — "Add release checklist (dress rehearsal) (#3)"
- Diff: `docs/release-checklist.md` added, +25 lines, single file.
- Verified afterwards: file present on `main` at SHA `1b3eefd43e4646453c0df298e35cfc6c6f97c246`.

## Pre-release inventory findings

- **Releases:** `list_releases` returned **an empty list — no releases exist** in the repo. Expected for a scratch repo; on the production repo, record the latest release tag before cutting the next one.
- **Discussions:** `list_discussions` returned **totalCount 0, no discussions** — and this is because **Discussions is disabled on the repository** (`has_discussions: false`). The honest answer to "what do discussions return" is *nothing, because the feature is off*. Filed as issue #7.

## Checklist as merged (docs/release-checklist.md on main)

```markdown
# Release Checklist

Use this checklist for every release. Do not tag until every box is ticked.

## Pre-release verification
- [ ] CI green on the release branch (all required checks passing)
- [ ] CHANGELOG.md updated with all user-facing changes since the last tag
- [ ] Version bump committed (package manifest / version file)
- [ ] Release branch cut from the default branch with the expected merge base

## Release
- [ ] Release tag created (annotated tag: `git tag -a vX.Y.Z -m "..."`)
- [ ] Tag pushed to the remote
- [ ] Release notes published against the tag (draft, review, then publish)
- [ ] Release artifacts attached and verified (checksums present, artifacts download)

## Post-release
- [ ] Announcement posted in the appropriate channel / discussion
- [ ] Default branch merged back with any release-only fixes
- [ ] GitHub release marked as latest
- [ ] Rollback plan noted if the release needs to be pulled

## Sign-off
- [ ] Release owner signed off
- [ ] Date and release name recorded
```

The four required gates (CI green, changelog updated, release tag created, release notes published) are all present.

## Gap issues filed during the rehearsal

| Issue | Title |
|-------|-------|
| #4 | Add a CI workflow so the "CI green" release gate has something to run |
| #5 | Add a release-notes template so notes aren't written from scratch on release day |
| #6 | Add a CHANGELOG.md so the "changelog updated" release gate has an artifact |
| #7 | Discussions are disabled, so there is no forum for the post-release announcement |
| #8 | Add branch protection to the default branch so releases can't bypass review |
| #9 | Clean up stale rehearsal artifacts (open PR #2, demo branches, superseded checklist) |

**Tracking issue:** #10 "Rehearsal cleanup: delete the scratch repo" — all six gaps attached as sub-issues; completion comment posted stating the rehearsal is complete and the repo can be deleted once reviewed.

## Runbook for the real release (repeat in order)

1. Cut the release branch from the default branch; verify the merge base.
2. Confirm CI is green on the release branch (all required checks passing).
3. Update `CHANGELOG.md` with all user-facing changes since the last tag.
4. Commit the version bump.
5. Open the PR into the default branch; have a **different person** approve it (the author cannot approve their own PR — rehearsed).
6. Merge the PR; confirm the changed files landed on the default branch (retrieved directly from `refs/heads/main`).
7. Create the annotated release tag and push it.
8. Publish release notes against the tag (use the template — currently a gap, issue #5).
9. Attach and verify release artifacts (checksums, downloads).
10. Post the announcement in the chosen channel/discussion (currently a gap, issue #7).
11. Mark the release as latest, note the rollback plan, and record sign-off.
12. Before tag day, run the same pre-release inventory on the production repo: check the releases list and the discussions, and record exactly what they return — even if it's nothing.
