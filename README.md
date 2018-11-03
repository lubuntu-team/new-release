This is a checklist for all of the archive opening tasks we should do when starting a new development release:

 1. File a task about a new wallpaper and slideshow for the upcoming release.
 1. Change `update.cfg` in lubuntu-meta and the branding as well as the desktop file in `calamares-settings-ubuntu`.
 1. Make sure `repo-list` is up-to-date and run `setup-phab` in this repo. The production values can be found in the internal setup document.
 1. Someone with access to GitHub should update the default branches for the mirrored repositories.
 1. If `lintian` and `devscripts` have not been updated, cherry-pick the `lintian` patch adding the new release as known if there is one, and no-change rebuild `devscripts`.
   1. Lintian needs a patch because all of the Ubuntu releases are hardcoded in `vendors/ubuntu/main/data/changes-file/known-dists`.
   1. `devscripts` needs a no-change rebuild because it gets the value grabbed by `dch -r` on build time. This is in line 47 of `scripts/Makefile`.
 1. File the megatask for the upcoming release blockers.
