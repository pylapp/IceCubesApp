# Developer reminder about the fork

- [Certificates, profiles and identifiers](#certificates-profiles-and-identifiers)
- [Developer Certificate of Origin](#developer-certificate-of-origin)
- [Commits configuration](#commit-configuration)
- [Submit work](#submit-work)
- [Examples](#examples)

## Certificates, profiles and identifiers

- Create, if not done yet, a new app identifier
- Change the bundle indentifier in Xcode
- Create and download the suitable provisioning profile matching the computer and the devices in uses and also the capabilities
- Plug the developer team in Xcode
- If too difficult to update profiles, use autimatic signing

## Developer Certificate of Origin

Apply DCO in each commit with **-s** option

## Commit configuration

Check values for *user.name*, *user.email* and *user.signingKey*

Try as best as possible to apply [conventional commits rules](https://www.conventionalcommits.org/en/v1.0.0/).
Keep in mind to have  commits well prefixed, and with the issue number between parenthesis at the end, and also if needed the pull request issue number.
If commits embed contributions for other people, do not forget to [add them as co-authors](https://docs.github.com/fr/pull-requests/committing-changes-to-your-project/creating-and-editing-commits/creating-a-commit-with-multiple-authors).

Commit message should be prefixed by keywords [you can find in the specification](https://www.conventionalcommits.org/en/v1.0.0/#specification):
- fix:
- feat:
- build:
- chore:
- ci:
- docs:
- style:
- refactor:
- perf:
- test:

Can add also ! aftter the keyword to say a breaking change occur, and also add a scope between parenthesis like:
- feat!: breaking change because..
- feat(API)!: breaking change in the API because..
- feat: add something in the API...

For example, given a commit to fix the issue n°42, the commit should be like:

```text
fix: title of your commit (#42)

Some details about the fix you propose

Co-authored-by: First author firstname and lastname <first author email>
Co-authored-by: Second author firstname and lastname <second author email>

Signed-off-by: First author firstname and lastname <first author email>
Signed-off-by: Second author firstname and lastname <second author email>
```

## Submit work

1. Synchronize the fork (supposed created in GitHub and cloned)

```shell
# Check if upstream is added
git remote -v
# If not
git remote add upstream git@github.com:Dimillian/IceCubesApp.git

# Synchronize main branches (no develop branch spotted in upstream today)
git checkout main
git rebase upstream/main
```

2. Align the local _develop_ branch keeping local modifications for builds

```shell
git chekcout develop
git rebase main

# Should have in top of history the commits:
# - Apply my own Apple Developer configuration for debuging purposes / 8f45356a4a987e2cd5d720b8dc23c270b55b2c7e / Thu Sep 26 11:18:59 2024 +0200
# - Update local XCConfig file / ebe378bb0358f91e72e533c30eb3cebef5a1f749 / Thu Sep 26 11:38:13 2024 +0200
# - Just add a reminder about contributions for upstream
```

3. Reproduce the bug, check is issue already exists

4. Create workding branch from _develop_

```shell
git checkout -b working-branch develop
```

5. Do the evolutions, squash if needed

6. If ok, create the issue and the associated branch from main (synced with upstream)

```shell
git checkout -b xxxx-some-description-of-evolution main # Replace xxxx by issue number and improve name of course
```

7. Apply changes with cherry picks so as to have only useful evolutions in the branch to submit

```shell
# In xxxx-some-description-of-evolution of course
git cherry-pick commit-hash # Use the suitable commit hashes
```

8. Then push the branch and create the pull request

## Examples

Example of commit: https://github.com/pylapp/IceCubesApp/commit/bab41187ceeeda6422373dab8cbced330a3b3dd2

If you look at this repository, you main find in branches:
- *main*: synced with *upstream/main*
- *develop*: rebased from *main* with some local configuration commits, nver pushed to upstream, only in fork
- *fix/l10n/french-wordings*: a working branch to test, improve or fix things, created from *develop* with local changed
- *2200-improve-french-localizables*: created from synced *main*, thus *upstream/main* with useful commits cherry-picked, submitted for pull request, referencing the upstream issue
