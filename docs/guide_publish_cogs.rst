.. Publishing cogs for V3

Publishing cogs for Red V3
==========================

Users of Red install 3rd-party cogs using Downloader cog. To make your cog available
to install for others, you will have to create a git repository
and publish it on git repository hosting (for example `GitHub <https://github.com>`_)

Repository Template
-------------------

We have standardized what a repository's structure should look like to better assist
our Downloader system and provide essential information to the Red portal.

The main repository should contain at a minimum:

 - :ref:`An info.json file <info-json-format>`
 - One folder for each cog package in the repository

   - refer to :doc:`/guide_cog_creation` for information on how to create a valid cog package
   - you should also put :ref:`info.json file <info-json-format>` inside each cog folder

We also recommend adding a license and README file with general information about the repository.

For a simple example of what this might look like when finished,
take a look at `our example template <https://github.com/Cog-Creators/Applications>`_.

.. _info-json-format:

Info.json format
----------------

The optional info.json file may exist inside every package folder in the repo, 
as well as in the root of the repo. The following sections describe the valid 
keys within an info file (and maybe how the Downloader cog uses them).

Keys common to both repo and cog info.json (case sensitive)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- ``author`` (list of strings) - list of names of authors of the cog or repo.

- ``description`` (string) - A long description of the cog or repo. For cogs, this 
  is displayed when a user executes ``[p]cog info``.

- ``install_msg`` (string) - The message that gets displayed when a cog 
  is installed or a repo is added
  
  .. tip:: You can use the ``[p]`` key in your string to use the prefix
      used for installing.

- ``short`` (string) - A short description of the cog or repo. For cogs, this info 
  is displayed when a user executes ``[p]cog list``

Keys specific to the cog info.json (case sensitive)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- ``min_bot_version`` (string) - Min version number of Red in the format ``MAJOR.MINOR.MICRO``

- ``max_bot_version`` (string) - Max version number of Red in the format ``MAJOR.MINOR.MICRO``,
  if ``min_bot_version`` is newer than ``max_bot_version``, ``max_bot_version`` will be ignored

- ``min_python_version`` (list of integers) - Min version number of Python
  in the format ``[MAJOR, MINOR, PATCH]``

- ``hidden`` (bool) - Determines if a cog is visible in the cog list for a repo.

- ``disabled`` (bool) - Determines if a cog is available for install.

- ``required_cogs`` (map of cogname to repo URL) - A map of required cogs that this cog depends on.
  Downloader will not deal with this functionality but it may be useful for other cogs.

- ``requirements`` (list of strings) - list of required libraries that are
  passed to pip on cog install. ``SHARED_LIBRARIES`` do NOT go in this
  list.

- ``tags`` (list of strings) - A list of strings that are related to the
  functionality of the cog. Used to aid in searching.

- ``type`` (string) - Optional, defaults to ``COG``. Must be either ``COG`` or
  ``SHARED_LIBRARY``. If ``SHARED_LIBRARY`` then ``hidden`` will be ``True``.

.. warning::
    Shared libraries are deprecated since version 3.2 and are marked for removal in version 3.4.

