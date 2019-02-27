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

Branches
--------

master
^^^^^^

This branch should not be used for development purposes but only for syncing with the upstream repository.

lc-master
^^^^^^^^^

This is a new default branch for origin repository. It's starting state is cloned from the release branch of upstream repository. (TODO: need to decide whether we start from upstream 3.14 or lesser).

Tags
----

Tags should be created for released LibreClinica versions (not branches).

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
