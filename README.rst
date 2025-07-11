#######
WARNING
#######
This repository is no longer kept up to date.

###############
Plugin Template
###############
This repository serves as a template that can be used to quickly get a plugin published to PyPI as well as establish a consistent development environment with the rest of Moe.

By following the instructions of this template repository, you will setup a plugin that has the following features:

#. Automatic release process initiated by a manual trigger.

   * Changelog generation as well as releasing to PyPI and github are all initiated by running the ``Create Release PR`` github action. Once run, it will create a pull request for the new release which will allow you to edit the generated changelog prior to rebasing the PR onto the main branch. Once rebased into main, the ``Release`` github action will automatically run, publishing your new release.

   .. important::
       The automatic changelog generation is dependent on you adhering to the specific commit conventions of Moe.

#. Plugin documentation hosted on `Read the Docs <https://readthedocs.org/>`_.

   * As well as creating a consistent documentation interface with the rest of Moe, the main benefit of this is to use the auto-documentation feature of Sphinx for any API functions your plugin may provide.

#. Project and dependency management using `Poetry <https://python-poetry.org/>`_.
#. A CI suite that will run tests, lint your code, and build the documentation of any PR.

Instructions
============
#. Create a new repository from this template repository.

   * Name your repository ``moe_{plugin name}``. This will be the name of your package on PyPI as well.

#. Edit ``pyproject.toml``.

   * Edit any information in the ``tool.poetry`` and ``tool.poetry.plugins."moe.plugins"`` sections.

#. Edit github scripts and files.

   * ``.github/ISSUE TEMPLATE`` contains default issue templates that Moe uses. At a minimum, you need to change the url in ``config.yml`` to link to your repository's discussions.

     * You must also enable 'Discussions' in your repository settings in order for the referenced link to work.

   * Edit the ``SLUG`` constant in ``.github/scripts/prep_release.py`` to be your repository.

#. Setup documentation on `Read the Docs <https://readthedocs.org/>`_.

   .. note::
       This step is optional if you are not providing any new API functions with your plugin. In that case, you may remove the ``docs`` directory as well as the ``.readthedocs.yml`` file.

   * Edit ``docs/conf.py`` project information.

   * `Import your repository into Read the Docs <https://readthedocs.org/dashboard/import/?>`_.

     * This is the site used to host your documentation.

   * Configure your project to build docs on pull requests.

     * Readthedocs project -> Admin -> Settings

       * Check the box in the settings to build pull requests.

   * Edit the ``project-slug`` in ``.github/workflows/preview_docs.yml`` to be your readthedocs project slug.

#. Edit plugin information.

   * Edit the repository "About" section on github

     * Ensure to add your documentation link to the ``Website`` section.

   * Edit ``README.rst``

   * Edit ``docs/index.rst``

#. Setup PyPI publishing.

   * In your PyPI account, add the `release.yml` github action as a `trusted publisher <https://docs.pypi.org/trusted-publishers/adding-a-publisher/>`_.

#. Edit repository "About" information.

   * Ensure to add your documentation link to the ``Website`` section.

#. Optional: Setup code coverage reports in pull requests.

   * `Connect the repository with Codecov <https://docs.codecov.com/docs/github-2-getting-a-codecov-account-and-uploading-coverage>`_.

   * Add the ``CODECOV_TOKEN`` secret to the repository.

#. Once finished, commit your changes and create a ``v0.1.0`` tag. Then, push your changes with the new tag.

Contributing
============
If you find any steps missing, confusing, outdated, etc, please don't hesitate to create an issue, discussion, or PR. I'd like this repository to be a central truth for any shared project files such as linter settings, CI scripts, test helper functions, and anything else contained here.
