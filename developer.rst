Developer Documentation
=======================

Information about LibreClinca development and contribution workflows. This documentation includes initial proposal for organising development activities.

Version Control
---------------

Git version control system is used for tracking changes in LibreClinica project repositories. Those are hosted publicly via `ReliaTec GmbH GitHub <https://github.com/reliatec-gmbh/>`_ organisation. 

Repository
----------

`LibreClinica <https://github.com/reliatec-gmbh/LibreClinica>`_ (origin) repository was created as a fork from `OpenClinica <https://github.com/OpenClinica/OpenClinica>`_ (upstream) public repository. The idea is to maintain origin repository synchronisable with upstream as long as the upstream public version exists. This requires to define certain naming conventions in order to prevent naming collisions (for versions, branches and tags).

Issue Management
----------------

GitHub integrated issues management should be used to creates tickets before any code contributions. Tickets assigned to milestones that reflect the LibreClinica software versioning scheme.

Main Branches
-------------

Source code organisation is inspired by Vincent Driessen `git branching model <https://nvie.com/posts/a-successful-git-branching-model>`_ that promotes two main branches with an infinite lifetime (lc-master and lc-develop). In addition to above mentioned concept one more master branch exists that allows the syncing with upstream repository.

lc-master
^^^^^^^^^

This branch represents the production ready state of code. No direct commits are permitted to the lc-master. Only merges from supporting branches (release or hotfix) are allowed. Every changes merged back into lc-master repository is considered as new release (that shell be tagged). The initial state of lc-master is cloned from the release branch of upstream repository (3.14).

lc-develop
^^^^^^^^^^

This is a new default branch for origin repository. It tracks development changes for the next software release. This branch should be used for the purpose of continuous integration. Changes to lc-develop are introduced by merges from supporting branches (feature, release or hotfix).

master
^^^^^^

This branch should not be used for development purposes but only for syncing with the upstream repository where development continues independently from LibreClinica.

Supporting Branches
-------------------

Additional temporal branches are created from lc-develop or lc-master in order to introduce changes to the source code.

feature branches
^^^^^^^^^^^^^^^^

===========  ==========  =================
Branch from  Merge into  Naming convention
===========  ==========  =================
lc-develop   lc-develop  anything except master, lc-master, lc-develop, lc-release-\*, lc-hotfix-\*
===========  ==========  =================

.. code-block:: shell
   :caption: Creating a feature branch from lc-develop

   $ git checkout -b myfeature lc-develop


.. code-block:: shell
   :caption: Merging a feature branch on lc-develop

   $ git checkout lc-develop
   $ git merge --no-ff myfeature
   $ git branch -d myfeature
   $ git push origin lc-develop

release branches
^^^^^^^^^^^^^^^^

===========  ========================  =================
Branch from  Merge into                Naming convention
===========  ========================  =================
lc-develop   lc-develop and lc-master  lc-release-\*
===========  ========================  =================

.. code-block:: shell
   :caption: Creating a release branch from lc-develop

   $ git checkout -b lc-release-1.3.0 lc-develop
   $ ./bump-version.sh 1.3.0
   $ git commit -a -m "Bumped version number to 1.3.0"

.. code-block:: shell
   :caption: Merging a release branch on lc-master and tagging

   $ git checkout lc-master
   $ git merge --no-ff lc-release-1.3.0
   $ git tag -a lc-1.3.0

.. code-block:: shell
   :caption: Merging a release branch on lc-develop

   $ git checkout lc-develop
   $ git merge --no-ff lc-release-1.3.0

.. code-block:: shell
   :caption: Removing a temporary release branch

   $ git branch -d lc-release-1.3.0

hotfix branches
^^^^^^^^^^^^^^^

===========  ========================  =================
Branch from  Merge into                Naming convention
===========  ========================  =================
lc-master    lc-develop and lc-master  lc-hotfix-\*
===========  ========================  =================

.. code-block:: shell
   :caption: Creating a hotfix branch from lc-master

   $ git checkout -b lc-hotfix-1.3.1 lc-master
   $ ./bump-version.sh 1.3.1
   $ git commit -a -m "Bumped version number to 1.3.1"

.. code-block:: shell
   :caption: Fix the bug and commit the fix

   $ git commit -m "Fixed severe production problem"

.. code-block:: shell
   :caption: Merging a hotfix branch on lc-master and tagging

   $ git checkout lc-master
   $ git merge --no-ff lc-hotfix-1.3.1
   $ git tag -a lc-1.3.1

.. code-block:: shell
   :caption: Merging a hotfix branch on lc-develop

   $ git checkout lc-develop
   $ git merge --no-ff lc-hotfix-1.3.1


.. note::  The one exception to the rule here is that, when a release branch currently exists, the hotfix changes need to be merged into that release branch, instead of develop.

.. code-block:: shell
   :caption: Removing a temporary hotfix branch

   $ git branch -d lc-hotfix-1.3.1

Tags
----

Tags should be created for released LibreClinica versions.

Release Versioning
------------------

There is a need to start with fresh versioning scheme for LibreClinica (independent from upstream) to allow independent release cycle. Proposed was to use:

* MAJOR.MINOR.PATCH

In order to prevent conflicts with upstream branches proposed to use the "lc-" prefix:

* lc-MAJOR.MINOR.PATCH

these proposal are open to discussion.

Contributions
-------------

Contributions resolving registered tickets are submitted from personal forks of developers as pull requests. (TODO: we will define and transparently document what everything needs to be part of minimal contribution in order to be accepted).

Continuous Integration
----------------------

`Travis CI <https://travis-ci.org/>`_  to automate builds

Testing
-------

There was an idea to automate user interface testing with saucelabs (unit and integration testing is pretty much impossible with current codebase), we may be able to get a free license as open source project.

`Sauce Labs <https://saucelabs.com/open-source>`_  

Documentation
-------------

`reStructuredText <https://en.wikipedia.org/wiki/ReStructuredText>`_ (.rst) lightweight markup language is proposed to be used for the purpose of documentation writing. The LibreClinica documentation source files reside in `LibreClinica-docs <https://github.com/reliatec-gmbh/LibreClinica-docs>`_  repository. This repository contains a webhook to trigger the re-build of static HTML resources that are publicly hosted via `Read the Docs <https://readthedocs.org/>`_ (RTD) utilising RTD Sphinx Theme.
