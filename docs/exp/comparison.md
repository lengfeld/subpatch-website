# Comparison to other tools

Subpatch is not the first tool that tries to solve the multi repository
problem. Other tools are

* [git-submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules)
* [repo](https://gerrit.googlesource.com/git-repo/+/HEAD/README.md)
* [kas](https://kas.readthedocs.io/en/latest/)
* [west](https://docs.zephyrproject.org/latest/develop/west/index.html)
* [git-subtree](https://git.kernel.org/cgit/git/git.git/tree/contrib/subtree/git-subtree.txt)

This page will compare these tools with subpatch.


## Technical comparison

The following table compares the architecture of the tools

|                | subpatch | repo | git submodule | west    | kas     | subtree |
|--------------- |----------|------|---------------|---------|---------|---------|
| config format  | git-cfg  | xml  | git-cfg       | ???     | yaml    | none    |
| superproject   | any(1)   | none | git           | git     | git     | git     |
| subprojects    | any(1)   | git  | git           | git     | git     | git     |

Explanations of the rows:

* *config format*: The format of the config file that is used to track the
  information about the subprojects.
* *superproject*: This is the type of cvs that is the top level repository and
  also (often) tracks the configuration of subprojects. The repo tool is special here:
  It tracks the subprojects in a manifest file in a separate git
  repository, the so called *manifest repository*. But this repository is not
  part of the directory hierarchy when the project is checked out. It does not
  sit at the top level of the superproject.
* *subprojects*: This is the type of cvs that is support as a subproject. For all
  other tools, except subpatch, only other git repositories are supported.

Legend:

* `git-cfg` stands for the [git config format](https://git-scm.com/docs/git-config)
  used in `.git/config`, `~/.gitconfig` and `.gitmodules`.
* `(1)`: subpatch does not support all other cvs as super- and subprojects for
  now. Still work in progress.