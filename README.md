# dorgpatch
Drush shell script to create patches for drupal.org issues.

** This has been superseded by Dorgflow: https://github.com/joachim-n/dorgflow **

Requires the following setup:

 - You are on a git feature branch for your issue.
 - The branch name is of the format '1234-description-of-issue' where 1234
   is the drupal.org issue number.
 - The feature branch is rebased to the major development branch you want to
   diff against.
 - All your work is committed and the git working directory is clean.

Optional, to also create a 'tests-only' patch:
 - Your changes to tests are all on a branch whose name is of the format
   '1234-tests'. This should be merged into your feature branch.

Optional, to support also creating an interdiff file, one of:
 - The most recent patch corresponds to a commit on the feature branch whose
   subject is of the format 'patch 42', where 42 is the number of the comment
   the patch was posted on. (You may of course have any number of commits
   between this commit and the tip of the feature branch.)
 - The most recent patch file is in the current folder, and the filename
   contains both the issue number and the number of the comment it was posted
   on.

The following optional parameters may be passed. If omitted, they will be
prompted for.
 - comment_number: The index number for the comment the patch will be posted
   on. One of:
   - a numeric value for the comment number for the issue.
   - '?' to query drupal.org's API to get the number for the next comment
      on the issue.
   - 'x' to not add a comment number to the patch.

## Example

Suppose:
  - You are in sites/all/modules/contrib/flag.
  - You are on branch '1234-fix-everything', which branches off 8.x-4.x.
  - There is also a branch '1234-tests', which branches off 8.x-4.x
  - The most recent comment on www.drupal.org/node/1234 is #5.
  - There was an earlier patch at comment #2, which you based your work on,
    committing it to your feature branch with the commit message 'patch 2'.

Then this script will create the following patch files, diffing from 8.x-4.x:
  - 1234-6.flag.fix-everything.patch
  - 1234-6.flag.fix-everything-tests-only.patch
  - 1234-2-6.flag.fix-everything.interdiff.txt
