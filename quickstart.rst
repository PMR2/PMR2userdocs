Quickstart guides
=================

Here we are creating some quickstart guides for some common tasks. If you have a task that you think would benefit from such a guide, please `let us know <https://models.physiomeproject.org/about/contact>`_.

.. contents::

Uploading a model to the repository
-----------------------------------

While it is desirable to use some kind of version control system to manage the development of any work performed on a computer, it is often the case that a user has a model, in CellML for example, that they simply wish to upload to the model repository. It is hoped that soon tools such as `OpenCOR <http://opencor.ws/>`_ will natively support such a task, but for now users are currently required to learn a bit of :term:`Git` in order to upload such models themselves. An alternative is to simply `contact us <https://models.physiomeproject.org/about/contact>`_ with your model and we will upload it for you, but this will loose any direct association or connection with the original author of the model. We therefore highly recommend that the following process is followed at this time.

   #. create a :term:`workspace`
   
      More detail is available at :ref:`creatingNewWorkspace`. Note the :ref:`teaching instance <teachingInstanceFirstMention>` that is available for testing things out if required.
   
   #. use a :term:`git` client to :term:`clone` the workspace to your local machine
   
      To ensure an accurate record of your contributions is maintained, please see :ref:`gitUserNameConf`. A detailed description of cloning a workspace is available here: :ref:`tut1cloningworkspace`.
   
   #. add your model and any other data to the workspace (such as a brief documentation page in HTML or reStructuredText and any images used in the documentation)
   
      See :ref:`tut1CommitChanges` for details on adding the files to the cloned workspace on your local machine.
   
   #. push the changes back to the repository
   
      Details available here: :ref:`tut1PushingChanges`.
   
   #. [optional] share the workspace with any collaborators
   
      Your workspace will currently be private and only visible to yourself when you are logged in to the repository. If you would like to share the workspace with your collaborators while still keeping the work private, you are able to do so: :ref:`sharingWorkspaces`.
   
   #. [optional] create an :term:`exposure`
   
      If you have some documenation for your workspace or would like to easily link to a specific revision of your workspace, you are able to :ref:`create an exposure <tut1CreateExposure>` for the workspace. Like the workspace, this will initially be private to yourself and the users you choose to share it with. For CellML models, see extra information here: :ref:`exposing-cellml`.
   
   #. submit the workspace for "publication" - this will make the workspace publicly available
   
      In order to make your workspace publicly available, you need to submit it for publication. The publication process simply allows the repository administrators to quickly check the workspace for material that should not be distributed in the repository (once a workspace is published, it will be available *forever*). The process is the same as that described here: :ref:`submitting_exposure`.
   
   #. [optional] submit the exposure for publication (again, this makes it public)
   
      Once the workspace is published, you are able to submit any exposure(s) you might want public for publication.
