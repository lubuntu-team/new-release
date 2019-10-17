Two weeks before release day:

 1. Announce internally that any last minute changes should be done as soon as possible.
 1. File the megatask for the upcoming release's blockers.
 1. Go through the release blocker list for this cycle and punt non-RC tasks to next cycle.
 1. Inform the Calamares upstream contact that we plan on doing a release in two weeks. Discuss whether any important patches should be cherry-picked, and get those uploaded as soon as possible. Ask them nicely to ping you in the next two weeks if anything important comes up.
 1. Talk to the Lubuntu Documentation Team about what needs to be wrapped up for next release. Nicely remind them that the release is in two weeks.

A week before release day:

 1. Update the downloads page and the homepage for the new release in a draft, so they can be published on release day.
 1. Do one final check of the [testing checklist](https://phab.lubuntu.me/w/release-team/testing-checklist/) and send out a call for testers.
 1. Start drafting [a blog post](https://phab.lubuntu.me/source/blog/) for the release.
 1. Gather known bugs (possibly automate this) to put on the blog post from:
    1. [bugs associated with the Lubuntu Packages Team](https://bugs.launchpad.net/~lubuntu-packaging);
    1. packages in the Lubuntu packageset which the Lubuntu Packages Team might not have been subscribed to, especially Lubuntu specific ones like `lubuntu-meta` and `lubuntu-artwork`;
    1. known issues from previous release notes; and
    1. [open defects report on the ISO QA tracker](http://iso.qa.ubuntu.com/qatracker/reports/defects/opened) for both the upcoming release as well as previous releases to ensure nothing has been missed. 

After ISOs have been released:

 1. Update the Lubuntu Manual in production (via SSH):
    1. Merge `stable` -> `master`.
    1. Make sure version strings and hashes are updated in the `master` branch.
    1. Rename `stable` to its release number.
    1. Push `master` to `stable` (and to `lts` if applicable; do NOT merge).
    1. Change the version strings in `master` to reflect the new development release.
 1. Publish the blog post and the downloads/homepage drafts.
 1. Post on social media:
    1. [Twitter](https://twitter.com/LubuntuOfficial) or [Mastodon](https://mastodon.technology/@lubuntu) (publishing to one published to the other).
    1. [r/Lubuntu](https://www.reddit.com/r/Lubuntu) and [r/Ubuntu](https://www.reddit.com/r/Ubuntu).
    1. [Facebook page](https://www.facebook.com/Lubuntu.Official.Page/) and [Facebook group](https://www.facebook.com/groups/lubuntu.official/).
    1. IRC topics for #lubuntu, #lubuntu-devel, and #lubuntu-offtopic on freenode.
    1. Announce on the [lubuntu-users](https://lists.ubuntu.com/mailman/listinfo/lubuntu-users) and [lubuntu-devel](https://lists.ubuntu.com/mailman/listinfo/lubuntu-devel) mailing lists.
 1. Scan social media and see if anyone is pointing out any reproducible bugs that we can file.
 1. Edit [the Phab sidebar](https://phab.lubuntu.me/home/menu/configure/global/).

After the codename is announced and `base-files` is uploaded:

 1. File a task about a new wallpaper and slideshow for the upcoming release.
 1. Change `update.cfg` in lubuntu-meta and the branding as well as the desktop file in `calamares-settings-ubuntu`.
 1. Make sure `repo-list` is up-to-date and run `setup-phab` in this repo. The production values can be found in the internal setup document.
 1. Someone with access to GitHub should update the default branches for the mirrored repositories.
 1. Update the CI to enable builds for the new release:
    1. In [ci.conf](https://phab.lubuntu.me/source/ci-metadata/browse/master/ci.conf):
       1. Add the new codename to the `releases` list, and remove old releases if necessary.
       1. Change `default_branch` to the branch you just created above.
       1. Evaluate overrides for the aforementioned variables and season to taste.
    1. Run [jobgenerator](https://ci.lubuntu.me/job/jobgenerator/) and then look over the builds triggered. Did you miss a step?
    1. Add the new release to [the Britney job](https://ci.lubuntu.me/view/mgmt/job/Britney/configure) so builds can migrate.
    1. SSH into the Jenkins container, `su` to the `jenkins` user, go to `~/jobs` and remove old jobs (e.g. from an old release), and in the Jenkins settings, `Reload Configuration from Disk`.
 1. If `lintian` and `devscripts` have not been updated, cherry-pick the `lintian` patch adding the new release as known if there is one, and no-change rebuild `devscripts`.
    1. Lintian needs a patch because all of the Ubuntu releases are hardcoded in `vendors/ubuntu/main/data/changes-file/known-dists`.
    1. `devscripts` needs a no-change rebuild because it gets the value grabbed by `dch -r` on build time. This is in line 47 of `scripts/Makefile`.
 1. Evaluate our packages. What needs to be updated to the latest upstream release? What did we carry over to this release?
