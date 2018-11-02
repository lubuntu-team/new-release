This is a checklist for all of the archive opening tasks we should do on our infrastructure when starting a new development release:

 1. Change `update.cfg` in lubuntu-meta and the branding in `calamares-settings-ubuntu` to 19.04.
 1. Run `update-branches.sh` to check out and push new branches for all the repositories listed in `repo-list`.
