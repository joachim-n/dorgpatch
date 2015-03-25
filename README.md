# dorgpatch
Drush shell script to create patches for drupal.org issues.

Requires the following setup:

 - You are on a git feature branch for your issue.
 - The branch name is of the format '1234-description-of-issue' where 1234
   is the drupal.org issue number.
 - The feature branch is rebased to the major development branch you want to
   diff against.
 - All your work is committed.

Optional, to also create a 'tests-only' patch:
 - Your changes to tests are all on a branch whose name is of the format
   '1234-tests'. This should be merged into your feature branch.

Pass a parameter to give a comment number for the issue. Alternatively, the
script can query drupal.org's API to get the number for the next comment on
the issue.

## Example

Suppose:
  - You are in sites/all/modules/contrib/flag.
  - You are on branch '1234-fix-everything', which branches off 8.x-4.x.
  - There is also a branch '1234-tests', which branches off 8.x-4.x
  - The most recent comment on www.drupal.org/node/1234 is #5.

Then this script will create the following patch files, diffing from 8.x-4.x:
  - 2457403-6.flag.fix-everything.patch
  - 2457403-6.flag.fix-everything-tests-only.patch
