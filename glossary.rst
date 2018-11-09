.. _glossary:

========
Glossary
========

.. _Git Beginner's Guide: http://backlogtool.com/git-guide/en/

.. glossary::
   :sorted:


   Checkout
      Switch branches or restore working tree files.
      
   Clone
      The term used with distributed version control systems (DVCS) to describe the process for making complete copy of another repository, usually hosted at a different site. This is done in order to have a local copy of a repository to work in.

   Embedded workspace
   Embedded workspaces
      Essentially workspace or workspaces that are nested inside another one through mechanisms offered by distributed version control systems.  In :term:`Git` it will be through the use of Git submodules.

   Exposure
   Exposures
      A publicly available page that provides access to and information about a specific revision of a workspace. Exposures are used to publish the contents of workspaces at points in time where the model(s) contained are considered to be useful.

      Exposures are created by the PMR software, and offer views appropriate to the type of model being exposed. CellML files for example are presented with options such as code generation and mathematics display, whereas FieldML models might offer a 3D view of the mesh.

   Fork
      A copy of the workspace which includes all the original version history, but is owned by the user who created the fork.

   Synchronize
      Used to pull the contents or changes from other repositories into a workspace via a URI.  The remote repository have to be of the same DVCS protocol of the corresponding workspace..

   Workspace
   Workspaces
      A `Git` repository hosted on the Physiome Model Repository. This is essentially a folder or directory in which files are stored, with the added feature of being version controlled by the distributed version control system called `Git`_.

   Git
      `Git <http://git-scm.com/>`_ is a distributed version control system currently used by the Physiome Model Repository software to maintain a history of changes to files in :term:`workspaces`. See a tour of the `Git Beginner's Guide`_ for some good introductory material.

   PMR
      An instance of :term:`PMR2` known as the Physiome Model Repository. The official URL of PMR is https://models.physiomeproject.org. A :term:`teaching instance` is also available for testing and teaching purposes.
      
   PMR2
      The software that powers the Auckland Physiome Repository.

   Push
   Pushing
      The term used with distibuted version control systems for the action of pushing changes from one clone of the repository into another. With PMR, this usually implies pushing from a workspace clone on your local machine back to the workspace in the model repository, but could be into any other clone of the workspace. See a tour of the `Git Beginner's Guide`_ for some good introductory material.

   Pull
   Pulling
      The term used with distributed version control systems for the action of pulling changes from one clone of the repository into another. With PMR, this usually implies pulling from a workspace in the model repository into a clone of the workspace on your local machine.

   Python
      Python is a programming language that lets you work more quickly and integrate your systems more effectively. See `<http://python.org>`_ for all the details.

   Teaching instance
      An instance of :term:`PMR2` that allows users to explore and test the functionality of PMR2 without making permanent :term:`workspaces` or :term:`exposures`. The teaching instance is regularly cleared of content and re-populated from :term:`PMR`. It is also used for testing the latest PMR2 features prior to their deployment on PMR, so the user interface may not always exactly match that of PMR.
