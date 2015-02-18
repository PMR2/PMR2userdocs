.. _cellmlrepositorytutorial:

==========================================================
Tutorial on using CellML with Auckland Physiome Repository
==========================================================

.. sectionauthor:: David Nickerson, Randall Britten, Dougal Cowan

.. _teaching instance: http://teaching.physiomeproject.org

About this tutorial
===================

The Auckland Physiome Repository provides extensive support for CellML
model and related files.  Previously it was called the CellML Model
Repository, this has since been merged completely along with the FieldML
Model Repository into the unified repository.  The underlying software
is :term:`PMR2`, which in turn relies on the distributed version control
system :term:`Git`, which allows the repository to maintain a complete
history of all changes made to every file it contains. This tutorial
demonstrates how to work with the repository using TortoiseGit, which
provides a Windows explorer integrated system for working with Git
repositories.

::

  Brief mention of the equivalent command line versions of the
  TortoiseGit actions will also be mentioned, so that these ideas can
  also be used without a graphical client, and on Linux and similar
  systems. These will be denoted by boxes like this.

This tutorial requires you to have:

- A `Git client <http://git-scm.com/downloads>`_.  Optionally, a GUI
  client such as `TortoiseGit <http://code.google.com/p/tortoisegit/>`_.
- The `OpenCell <http://www.cellml.org/tools/opencell>`_ CellML
  modelling environment.
- A text editor such as `Notepad++ <http://notepad-plus-plus.org/>`_ or
  `gedit <http://projects.gnome.org/gedit/>`_.

Basic concepts
==============

The Auckland Physiome Repository use a certain amount of jargon - some
is specific to the repository software, and some is related to
distributed version control systems (DVCSs). Below are basic
explanations of some of these terms as they apply to the repository.

:term:`Workspace`

  A container (much like a folder or directory on your computer) to hold
  the files that make up a model, as well as any other files such as
  documentation or metadata, etc. In practical terms, each workspace is
  a Git repository.

:term:`Exposure`

  An exposure is a publicly viewable presentation of a particular
  revision of a model. An exposure can present one or many files from
  your workspace, along with documentation and other information about
  your model.

The Git DVCS has a range of terms that are useful to know, and
definitions of these terms can be found in the Git Reference
http://git-scm.com/docs.

.. index::
   single: Auckland Physiome Repository web interface

Working with the repository web interface
=========================================

This part of the tutorial will teach you how to find models in the
Auckland Physiome Repository `<https://models.physiomeproject.org>`_,
how to view a range of information about those models, and how to
download models. The first page in the repository consists of basic
navigation, a link to the main model listing, a search box at the top
right, and a list of model category links as shown below.

.. figure:: images/tut1-mainscreen.png
   :align: center

   The front page of the Auckland Physiome Repository.

Model listings
--------------

Clicking on the main model listing or any of the category listings will
take you to a page displaying a list of exposed models in that category.
Click on electrophysiology for example, and a list of over 100 exposed
models in that category will be displayed, as shown here.

.. figure:: images/tut1-modellistings.png
   :align: center

   A list of models in the electrophysiology category.

Clicking on an item in the list will take you to the exposure page for
that model.

Searching the repository
------------------------

You can search for the model that you wish to work on by entering a
search term in the box at the top right of the page. Many of the models
in the repository are named by the first author and publication date of
the paper, so a good search query might be something like `goldbeter
1991`. A list of the results of your search will probably contain both
workspaces and exposures - you will need to click on the workspace of
the model you wish to work on. Workspaces can be identified by where
they are located, as they will be located inside **Workspaces**.
In the following screenshot, the first two results are workspaces, and
the remainder are exposures.  Note that red links are exposures that are
marked as expired.

.. figure:: images/tut1-searchresults.png
   :align: center

   A search results listing on the Auckland Physiome Repository.

Click on an exposure result to view information about the model and to
get links for downloading or simulating the model. Click on workspaces
to see the contents of the model workspace and the revision history of
the model.

.. _cellmlrepositorytutorial-git:

Working with the repository using Git
=====================================

This part of the tutorial will teach you how to :term:`clone` a
workspace from the model repository using a Git client, create
your own workspace, and then push the cloned workspace into your new
workspace in the repository. We will be using a :term:`fork` of an
existing workspace, which provides you with a personal copy of a
workspace that you can edit and push changes to.

Registering an account and logging in
-------------------------------------

First, navigate to the `teaching instance`_ of the Auckland Physiome
Repository at `<http://teaching.physiomeproject.org/>`_.

.. include:: teaching-instance-warning.rst

In order to make changes to models in the CellML repository, you must
first register for an account.  Your account will
have the appropriate access privileges so that you can push any changes
you have made to a model back into the repository.

To register an account, access the *Log in* link and access the
*registration form* from there. Enter your desired username and
password. After completing the email validation step, you can now log in
to the repository.

.. note::

   This username and password are also the credentials you use to
   interact with the repository via Git.

Once logged in to the repository, you will notice that there is a new
link in the navigation bar, My Workspaces. This is where all the
workspaces you create later on will be listed. The Log in link is also
replaced by your username and a Log out link.

Git username configuration
--------------------------

.. important::
   **Username setup for Git**

   Since you are about to make changes, your name and email address must
   be recorded as part of the workspace revision history. When commit
   your changes using Git, they exist independently from the Auckland
   Physiome Repository.  This means that you have to set-up your
   username for the Git client software, even though you have registered
   a username on Auckland Physiome Repository.

   You only need to do this once.

**Steps for TortoiseGit:**

- From the right-click menu in Windows Explorer (which is accessible by
  right-clicking anywhere on the file selection area) you can select the
  Settings by :menuselection:`TortoiseGit --> Settings`.
- On the settings screen, under the Git section, enter your details into
  the respective sections.

**Steps for command line:**

  The configurations are saved in the ``.gitconfig`` file in the user's
  home directory, and the recommended way to do so is::

  $ git config --global user.name "<Your Name>"
  $ git config --global user.email "<Your Email address>"

.. _tut1forkingaworkspace:

Forking an existing workspace
-----------------------------

.. important::

   It is essential to use a Git client to obtain models from the
   repository for editing. The Git client is not only able to keep
   track of all the changes you make (allowing you to back-track if you
   make any errors), but using a Git client is the only way to add
   any changes you have made back into the repository.

For this tutorial we will :term:`fork` an existing workspace. This
creates new workspace owned by you, containing a copy of all the files
in the workspace you forked including their complete history. This is
equivalent to cloning the workspace, creating a new workspace for
yourself, and then pushing the contents of the cloned workspace into
your new workspace.

Forking a workspace can be done using the Physiome Model Repository web
interface. The first step is to find the workspace you wish to fork. We
will use the Beeler, Reuter 1977 :term:`workspace` which can be found
at:
`<http://teaching.physiomeproject.org/workspace/beeler_reuter_1977>`_.

Now click on the :guilabel:`fork` option in the toolbar, as shown below.

.. figure:: images/fork1.png
   :align: center

You will be asked to confirm the *fork* action by clicking the
:guilabel:`Fork` button. You will then be shown the page for your forked
workspace.

.. _tut1cloningworkspace:

Cloning your forked workspace
-----------------------------

In order to make changes to your workspace, you have to :term:`clone` it
to your own computer. In order to do this, copy the URI for git
clone/pull/push as shown below:

.. figure:: images/tut1-cloneurl.png
   :align: center

   Copying the URI for cloning your workspace.

In Windows explorer, navigate the folder where you want to create the
clone of the workspace. Then use the right-click menu and select
:menuselection:`Git Clone...` as shown below:

.. figure:: images/tut1-tortoisegitclone.png
   :align: center

Paste the copied URL into the *Source:* area and then click the *Clone*
button. This will create a folder called ``beeler_reuter_1977_tut`` that
contains all the files and history of your forked workspace. The folder
will be created inside the folder in which you instigated the clone
command.

**Command line equivalent** ::

   git clone [URI]

You will need to enter your username and password to clone the
workspace, as the fork will be set to *private* when it is created.

The repository will be cloned within the current directory of your
command line window.

Making changes to workspace contents
------------------------------------

Your cloned workspace is now ready for you to edit the model file and
make a commit each time you want to save the changes you have made. As
an example, open the model file in your text editor and remove the
paragraph which describes validation errors from the documentation
section, as shown below:

.. figure:: images/tut1-editcellmlfile.png
   :align: center

Save the file. If you are using TortoiseGit, you will notice that the
icon overlay has changed to a red exclamation mark. This indicates that
the file now has uncommitted changes.

Committing changes
------------------

If you are using TortoiseGit, bring up the shell menu for the altered
file and select :menuselection:`TortoiseGit --> Git Commit`. A window will
appear showing details of the changes you are about to commit, and
prompting for a commit message. Every time you commit changes, you
should enter a useful commit message with information about what changes
have been made. In this instance, something like "Removed the paragraph
about validation errors from the documentation" is appropriate.

Click on the Commit button at the far left of the toolbar. The icon
overlay for the file will now change to a green tick, indicating that
changes to the file have been committed.

.. figure:: images/tut1-commitchanges.png
   :align: center

**Command line equivalent** ::

   git commit -m "Removed the paragraph about validation errors from the documentation"

Pushing changes to the repository
---------------------------------

Your cloned workspace on your local machine now has a small history of
changes which you wish to *push* into the repository.

Right click on your workspace folder in Windows explorer, and select
:menuselection:`TortoiseGit --> Git Synchronize` from the shell menu. This
will bring up a window from which you can manage changes to the
workspace in the repository. Click on the Push button in the toolbar,
and enter your username and password when prompted.

.. figure:: images/tut1-pushchanges.png
   :align: center

**Command line equivalent** ::

   git push

Now navigate to your workspace and click on the history toolbar button.
This will show entries under the Most recent changes, complete with the
commit messages you entered for each commit, as shown below:

.. figure:: images/tut1-newhistoryentry.png
   :align: center

Create an exposure
==================

As explained earlier, an :term:`exposure` aims to bring a particular
revision to the attention of users who are browsing and searching the
repository.

There are two ways of making an exposure - creating a new exposure from
scratch, or "Rolling over" an exposure. Rolling over is used when a
workspace already has an existing exposure, and the updates to the
workspace have not fundamentally changed the structure of the workspace.
This means that all the information used in making the previous exposure
is still valid for making a new exposure of a more recent revision of
the workspace. Strictly speaking, an exposure can be rolled over to an
older revision as well, but this is not the usual usage.

As you are working in a forked repository, you will need to create a new
exposure from scratch. To learn how to create exposures, please refer to
:ref:`exposing-cellml`.

.. _migrating-from-teaching-to-live-repo:

Migrating content to the main repository
========================================

As noted above, the `teaching instance`_ used in this tutorial is not
suitable for permanent storage of your work. One of the advantages of
using a distributed version control system to manage :term:`workspaces`
is that it is straightforward to move the entire workspace, including
the full history and provenance record, from one location to another.
PMR2 also provides a feature that exports exposures so that they can
then be imported into another PMR2 instance.

For example: if you would like to move your work in your workspace on
the teaching instance into a *new* workspace on the Auckland Physiome
Repository (or from one PMR2 instance to another), you should follow
these steps:

1. Ensure that you have pushed all your commits to the source instance;

#. :ref:`Create the new workspace <creatingNewWorkspace>` in the
   destination repository;

#. Navigate to the workspace created and choose the
   :guilabel:`synchronize` action from the workspace toolbar, as shown
   below.

.. figure:: images/synchronize-form.png
   :align: center

4. Fill in the URI of your workspace on the source instance (*e.g.,*
   `<http://models.physiomeproject.org/w/andre/cortassa-ECME-2006>`_)

#. Click the :guilabel:`Synchronize` button.

.. _exposurewizardimportexport:

In a similar manner, you are able to copy :term:`exposures` you might
have made on the teaching instance over to the main repository, or from
the main to the teaching instance if you want to test things out. Follow
these steps to migrate an :term:`exposure` from one repository to
another.

1. Navigate to the exposure you would like to migrate in the source
   repository.

#. Choose the :guilabel:`wizard` item from the toolbar as shown below.

.. figure:: images/exposure-wizard-highlight-export.png
   :align: center

3. In the destination repository, navigate to the desired revision of
   the (published) workspace and choose the :guilabel:`Create exposure`
   action as described in the directions for :ref:`creating an exposure
   from scratch <createExposureChooseRevision>`

#. Rather than building a new exposure, choose the :guilabel:`Exposure
   Import via URI` tab in the exposure creation wizard, as shown below.

.. figure:: images/exposure-wizard-import-from-uri.png
   :align: center

5. Copy and paste the URI from the source exposure wizard, highlighted
   above, into the :guilabel:`Exposure Export URI` field in the exposure
   creation wizard shown above.

#. Click the :guilabel:`Add` button. This will take you back to the
   standard :ref:`exposure build page <buildingTheExposure>`, but now
   with all the fields pre-populated from the source exposure.

#. Navigate to the bottom of the page and click the :guilabel:`Build`
   button to actually build the exposure pages. You are free to
   reconfigure the exposure if desired, some :ref:`help is available
   <buildingTheExposure>` for this if needed.
