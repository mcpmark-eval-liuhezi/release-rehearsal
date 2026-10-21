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
