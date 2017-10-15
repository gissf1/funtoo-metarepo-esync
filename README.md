# funtoo-metarepo-esync
esync tool to be used with Funtoo's meta-repos.  Allows proper metarepo syncs and persisting user's preferred branch settings.

This was fundamentally based on the script from http://forums.funtoo.org/topic/1180-how-to-change-branch-of-kits-from-meta-repo/ where @cafaia shows how to sync a repo.

This tool (shell + gawk) does syncs on each metarepo section, allows selection of a desired branch, and persists those branch selections across syncs.  This is provided in hopes that it can be useful to others until ego/epro does this internally.

Github page is here: https://github.com/gissf1/funtoo-metarepo-esync/

It currently requires you to call set for each metarepo's desired branch for it to do a pull on that branch.  It reports some errors and warnings, and should not destroy any data, but as usual, there are no warranties of any kind and you are using this at your own risk.

It uses a hidden file to store the preferences at /var/git/.metarepo_selections and creates a backup before updating.

Sample usage and output:
```bash
# esync
usage: esync [help|sync|show [meta-repo]|set {meta-repo} {branch}]
   sync  Syncs all meta-repos on the appropriate branches
   show  Shows branches for meta-repo (all meta-repos by default)
         Legend:  "[checked-out]", "{selected}", or "available"
   set   Selects the desired branch for the specified meta-repo
   help  Shows this help/usage text

# esync show
core-hw-kit     [master]
core-kit        [1.0-prime] master
desktop-kit     [master]
dev-kit         [master]
editors-kit     [master]
games-kit       [master]
gnome-kit       [3.20-prime] master
java-kit        [master]
kde-kit         [5.10-prime] master
media-kit       [1.0-prime] master
net-kit         [master]
nokit           [master]
perl-kit        [5.24-prime] master
php-kit         [master]
python-kit      [3.4-prime] master
science-kit     [master]
security-kit    1.0-prime [master]
text-kit        [master]
xorg-kit        1.17-prime [master]

# esync set security-kit 1.0-prime

# esync show security-kit
security-kit    [1.0-prime] master

# esync sync
Already up-to-date.
Submodule path 'kits/xorg-kit': checked out '4427e37462e2260c52e3e3e35139e43948d72392'
I: meta-repo 'core-hw-kit' is already on branch 'master'
Already up-to-date.
I: meta-repo 'core-hw-kit' successfully updated branch 'master'
I: meta-repo 'core-kit' is already on branch '1.0-prime'
I: meta-repo 'core-hw-kit' is already on branch 'master'
Already up-to-date.
I: meta-repo 'core-hw-kit' successfully updated branch 'master'
I: meta-repo 'core-kit' is already on branch '1.0-prime'
Already up-to-date.
I: meta-repo 'core-kit' successfully updated branch '1.0-prime'
I: meta-repo 'desktop-kit' is already on branch 'master'
Already up-to-date.
I: meta-repo 'desktop-kit' successfully updated branch 'master'
I: meta-repo 'dev-kit' is already on branch 'master'
Already up-to-date.
I: meta-repo 'dev-kit' successfully updated branch 'master'
I: meta-repo 'editors-kit' is already on branch 'master'
Already up-to-date.
I: meta-repo 'editors-kit' successfully updated branch 'master'
I: meta-repo 'games-kit' is already on branch 'master'
Already up-to-date.
I: meta-repo 'games-kit' successfully updated branch 'master'
I: meta-repo 'gnome-kit' is already on branch '3.20-prime'
Already up-to-date.
I: meta-repo 'gnome-kit' successfully updated branch '3.20-prime'
I: meta-repo 'java-kit' is already on branch 'master'
Already up-to-date.
I: meta-repo 'java-kit' successfully updated branch 'master'
I: meta-repo 'kde-kit' is already on branch '5.10-prime'
Already up-to-date.
I: meta-repo 'kde-kit' successfully updated branch '5.10-prime'
I: meta-repo 'media-kit' is already on branch '1.0-prime'
Already up-to-date.
Already up-to-date.
I: meta-repo 'media-kit' successfully updated branch '1.0-prime'
I: meta-repo 'net-kit' is already on branch 'master'
Already up-to-date.
I: meta-repo 'net-kit' successfully updated branch 'master'
I: meta-repo 'nokit' is already on branch 'master'
Already up-to-date.
I: meta-repo 'nokit' successfully updated branch 'master'
I: meta-repo 'perl-kit' is already on branch '5.24-prime'
remote: Counting objects: 69, done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 69 (delta 48), reused 69 (delta 48), pack-reused 0
Unpacking objects: 100% (69/69), done.
From https://github.com/funtoo/perl-kit
   b2caa470..d15410f1  master     -> origin/master
Already up-to-date.
I: meta-repo 'perl-kit' successfully updated branch '5.24-prime'
I: meta-repo 'php-kit' is already on branch 'master'
Already up-to-date.
I: meta-repo 'php-kit' successfully updated branch 'master'
I: meta-repo 'python-kit' is already on branch '3.4-prime'
remote: Counting objects: 13, done.
remote: Compressing objects: 100% (8/8), done.
remote: Total 13 (delta 5), reused 13 (delta 5), pack-reused 0
Unpacking objects: 100% (13/13), done.
From https://github.com/funtoo/python-kit
   871713c8..2e003333  master     -> origin/master
Already up-to-date.
I: meta-repo 'python-kit' successfully updated branch '3.4-prime'
I: meta-repo 'science-kit' is already on branch 'master'
Already up-to-date.
I: meta-repo 'science-kit' successfully updated branch 'master'
I: meta-repo 'security-kit' is already on branch '1.0-prime'
Already up-to-date.
I: meta-repo 'security-kit' successfully updated branch '1.0-prime'
I: meta-repo 'text-kit' is already on branch 'master'
Already up-to-date.
I: meta-repo 'text-kit' successfully updated branch 'master'
Previous HEAD position was 4427e37... updates
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
I: meta-repo 'xorg-kit' is now on branch 'master'
Already up-to-date.
I: meta-repo 'xorg-kit' successfully updated branch 'master'

# esync show security-kit
security-kit    [1.0-prime] master
```
