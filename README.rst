# Task # 4: 

This problem crops up because when they are loaded with the script `gen_latex_symbols.py`, some of the entries are writted with a capital `\U` rather than the lowercase `\u` that python seems to accept.

This can be fixed manually with a find and replace, but some of them are being rendered incorrectly, e.g. `\scrl` should be mathematical script small l: `𝓁` but instead comes out as `ᵌ1` in GitBash.

I've changed `gen_latex_symbols.py` to run a find/replace on `\U -> \u` in the value part of the string, but the issue with the misrendered symbols still needs to be addressed.

# Task # 3:
Continuing efforts towards: https://github.com/ipython/ipython/issues/12861

We already Removed the check that LaTeX commands must be valid Python identifiers.
This allowed users to input glyphs like the root symbol with \sqrt.

When merged with #Task #1, this creates a new problem: not all commands in latex_symbols.jl can be parsed correctly.

(Note: On e938d046f3ec81120a86763900a9be86a7dc5f81 on NixOS Linux in a VirtualEnv with no other special setup, the below error could not be reproduced. Why might it only occur intermittently?)

```
> python3 -m IPython
Traceback (most recent call last):
  File "/usr/lib/python3.8/runpy.py", line 185, in _run_module_as_main
    mod_name, mod_spec, code = _get_module_details(mod_name, _Error)
  File "/usr/lib/python3.8/runpy.py", line 144, in _get_module_details
    return _get_module_details(pkg_main_name, error)
  File "/usr/lib/python3.8/runpy.py", line 111, in _get_module_details
    __import__(pkg_name)
  File "/home/david/Downloads/ipython/IPython/__init__.py", line 56, in <module>
    from .terminal.embed import embed
  File "/home/david/Downloads/ipython/IPython/terminal/embed.py", line 16, in <module>
    from IPython.terminal.interactiveshell import TerminalInteractiveShell
  File "/home/david/Downloads/ipython/IPython/terminal/interactiveshell.py", line 47, in <module>
    from .debugger import TerminalPdb, Pdb
  File "/home/david/Downloads/ipython/IPython/terminal/debugger.py", line 7, in <module>
    from IPython.core.completer import IPCompleter
  File "/home/david/Downloads/ipython/IPython/core/completer.py", line 133, in <module>
    from IPython.core.latex_symbols import latex_symbols, reverse_latex_symbol
  File "/home/david/Downloads/ipython/IPython/core/latex_symbols.py", line 1662
    "\\scrl" : "\U1d4c1",
               ^
SyntaxError: (unicode error) 'unicodeescape' codec can't decode bytes in position 0-6: truncated \UXXXXXXXX escape
```
You can type LaTeX Unicode commands as desired if the offending lines
are deleted from `IPython/core/latex_symbols.py`.




# Task # 1 - https://github.com/ipython/ipython/issues/12861

accidentalrebel: Made a pull request. https://github.com/code-relay-io/ipython/pull/1

# Task # 2 - Double check if newly generated `latex_symbols.py` is complete and are working in IPython.

# Task # 2

Investigate why tools/gen_latex_symbols.py fails to decode \U1d4c1 mathematical script small l in latex_symbols.jl

Remember your job is to make *incremental* progress, break the task into smaller tasks, or finish something in 15 minutes, then pass it along to the next contributor. 
No responsibility, only fun.

Add your next task to the readme.md. When you're done add your next task to the top of this readme and make a pull request to this repo.

Email with questions

.. image:: https://codecov.io/github/ipython/ipython/coverage.svg?branch=master
    :target: https://codecov.io/github/ipython/ipython?branch=master

.. image:: https://img.shields.io/pypi/v/IPython.svg
    :target: https://pypi.python.org/pypi/ipython

.. image:: https://img.shields.io/travis/ipython/ipython.svg
    :target: https://travis-ci.org/ipython/ipython

.. image:: https://www.codetriage.com/ipython/ipython/badges/users.svg
    :target: https://www.codetriage.com/ipython/ipython/

.. image:: https://raster.shields.io/badge/Follows-NEP29-brightgreen.png
    :target: https://numpy.org/neps/nep-0029-deprecation_policy.html


===========================================
 IPython: Productive Interactive Computing
===========================================

Overview
========

Welcome to IPython.  Our full documentation is available on `ipython.readthedocs.io
<https://ipython.readthedocs.io/en/stable/>`_ and contains information on how to install, use, and
contribute to the project.
IPython (Interactive Python) is a command shell for interactive computing in multiple programming languages, originally developed for the Python programming language, that offers introspection, rich media, shell syntax, tab completion, and history.

**IPython versions and Python Support**

Starting with IPython 7.10, IPython follows `NEP 29 <https://numpy.org/neps/nep-0029-deprecation_policy.html>`_

**IPython 7.17+** requires Python version 3.7 and above.

**IPython 7.10+** requires Python version 3.6 and above.

**IPython 7.0** requires Python version 3.5 and above.

**IPython 6.x** requires Python version 3.3 and above.

**IPython 5.x LTS** is the compatible release for Python 2.7.
If you require Python 2 support, you **must** use IPython 5.x LTS. Please
update your project configurations and requirements as necessary.


The Notebook, Qt console and a number of other pieces are now parts of *Jupyter*.
See the `Jupyter installation docs <https://jupyter.readthedocs.io/en/latest/install.html>`__
if you want to use these.

Main features of IPython
========================
Comprehensive object introspection.

Input history, persistent across sessions.

Caching of output results during a session with automatically generated references.

Extensible tab completion, with support by default for completion of python variables and keywords, filenames and function keywords.

Extensible system of ‘magic’ commands for controlling the environment and performing many tasks related to IPython or the operating system.

A rich configuration system with easy switching between different setups (simpler than changing $PYTHONSTARTUP environment variables every time).

Session logging and reloading.

Extensible syntax processing for special purpose situations.

Access to the system shell with user-extensible alias system.

Easily embeddable in other Python programs and GUIs.

Integrated access to the pdb debugger and the Python profiler.


Development and Instant running
===============================

You can find the latest version of the development documentation on `readthedocs
<https://ipython.readthedocs.io/en/latest/>`_.

You can run IPython from this directory without even installing it system-wide
by typing at the terminal::

   $ python -m IPython

Or see the `development installation docs
<https://ipython.readthedocs.io/en/latest/install/install.html#installing-the-development-version>`_
for the latest revision on read the docs.

Documentation and installation instructions for older version of IPython can be
found on the `IPython website <https://ipython.org/documentation.html>`_



IPython requires Python version 3 or above
==========================================

Starting with version 6.0, IPython does not support Python 2.7, 3.0, 3.1, or
3.2.

For a version compatible with Python 2.7, please install the 5.x LTS Long Term
Support version.

If you are encountering this error message you are likely trying to install or
use IPython from source. You need to checkout the remote 5.x branch. If you are
using git the following should work::

  $ git fetch origin
  $ git checkout 5.x

If you encounter this error message with a regular install of IPython, then you
likely need to update your package manager, for example if you are using `pip`
check the version of pip with::

  $ pip --version

You will need to update pip to the version 9.0.1 or greater. If you are not using
pip, please inquiry with the maintainers of the package for your package
manager.

For more information see one of our blog posts:

    https://blog.jupyter.org/release-of-ipython-5-0-8ce60b8d2e8e

As well as the following Pull-Request for discussion:

    https://github.com/ipython/ipython/pull/9900

This error does also occur if you are invoking ``setup.py`` directly – which you
should not – or are using ``easy_install`` If this is the case, use ``pip
install .`` instead of ``setup.py install`` , and ``pip install -e .`` instead
of ``setup.py develop`` If you are depending on IPython as a dependency you may
also want to have a conditional dependency on IPython depending on the Python
version::

    install_req = ['ipython']
    if sys.version_info[0] < 3 and 'bdist_wheel' not in sys.argv:
        install_req.remove('ipython')
        install_req.append('ipython<6')

    setup(
        ...
        install_requires=install_req
    )

Alternatives to IPython
=======================

IPython may not be to your taste; if that's the case there might be similar
project that you might want to use:

- the classic Python REPL.
- `bpython <https://bpython-interpreter.org/>`_
- `mypython <https://www.asmeurer.com/mypython/>`_
- `ptpython and ptipython <https://pypi.org/project/ptpython/>`
- `xonsh <https://xon.sh/>`

Ignoring commits with git blame.ignoreRevsFile
==============================================

As of git 2.23, it is possible to make formatting changes without breaking
``git blame``. See the `git documentation
<https://git-scm.com/docs/git-config#Documentation/git-config.txt-blameignoreRevsFile>`_
for more details.

To use this feature you must:

- Install git >= 2.23
- Configure your local git repo by running:
   - POSIX: ``tools\configure-git-blame-ignore-revs.sh``
   - Windows:  ``tools\configure-git-blame-ignore-revs.bat``
