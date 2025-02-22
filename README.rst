=============
**HeuDiConv**
=============

`a heuristic-centric DICOM converter`

.. image:: https://img.shields.io/badge/docker-nipy/heudiconv:latest-brightgreen.svg?logo=docker&style=flat
  :target: https://hub.docker.com/r/nipy/heudiconv/tags/
  :alt: Our Docker image

.. image:: https://travis-ci.org/nipy/heudiconv.svg?branch=master
  :target: https://travis-ci.org/nipy/heudiconv
  :alt: TravisCI

.. image:: https://codecov.io/gh/nipy/heudiconv/branch/master/graph/badge.svg
  :target: https://codecov.io/gh/nipy/heudiconv
  :alt: CodeCoverage

.. image:: https://readthedocs.org/projects/heudiconv/badge/?version=latest
  :target: http://heudiconv.readthedocs.io/en/latest/?badge=latest
  :alt: Readthedocs

.. image:: https://zenodo.org/badge/DOI/10.5281/zenodo.1012598.svg
  :target: https://doi.org/10.5281/zenodo.1012598
  :alt: Zenodo (latest)

.. image:: https://repology.org/badge/version-for-repo/debian_unstable/heudiconv.svg?header=Debian%20Unstable
   :target: https://repology.org/project/heudiconv/versions
   :alt: Debian Unstable

.. image:: https://repology.org/badge/version-for-repo/gentoo_ovl_science/python:heudiconv.svg?header=Gentoo%20%28%3A%3Ascience%29
   :target: https://repology.org/project/python:heudiconv/versions
   :alt: Gentoo (::science)

.. image:: https://repology.org/badge/version-for-repo/pypi/python:heudiconv.svg?header=PyPI
   :target: https://repology.org/project/python:heudiconv/versions
   :alt: PyPI

About
-----

``heudiconv`` is a flexible DICOM converter for organizing brain imaging data
into structured directory layouts.

- It allows flexible directory layouts and naming schemes through customizable heuristics implementations.
- It only converts the necessary DICOMs and ignores everything else in a directory.
- You can keep links to DICOM files in the participant layout.
- Using `dcm2niix <https://github.com/rordenlab/dcm2niix/>`_ under the hood, it's fast.
- It can track the provenance of the conversion from DICOM to NIfTI in W3C PROV format.
- It provides assistance in converting to `BIDS <http://bids.neuroimaging.io/>`_.
- It integrates with `DataLad <https://www.datalad.org/>`_ to place converted and original data under git/git-annex
  version control while automatically annotating files with sensitive information (e.g., non-defaced anatomicals, etc).

Installation
------------

See our `installation page <https://heudiconv.readthedocs.io/en/latest/installation.html>`_ 
on heudiconv.readthedocs.io .

HOWTO 101
---------

In a nutshell -- ``heudiconv`` operates using a heuristic which, given metadata from DICOMs, would decide how to name
resultant (from conversion using `dcm2niix`_) files. Heuristic `convertall <https://github
.com/nipy/heudiconv/blob/master/heudiconv/heuristics/convertall.py>`_ could actually be used with no real
heuristic and by simply establish your own conversion mapping through editing produced mapping files.
In most use-cases of retrospective study data conversion, you would need to create your custom heuristic following
`existing heuristics as examples <https://github.com/nipy/heudiconv/tree/master/heudiconv/heuristics>`_ and/or
referring to `"Heuristic" section <https://heudiconv.readthedocs.io/en/latest/heuristics.html>`_ in the documentation.
**Note** that `ReproIn heuristic <https://github.com/nipy/heudiconv/blob/master/heudiconv/heuristics/reproin.py>`_ is
generic and powerful enough to be adopted virtually for *any* study: For prospective studies, you would just need
to name your sequences following the `ReproIn convention <https://github.com/nipy/heudiconv/blob/master/heudiconv/heuristics/reproin.py#L26>`_, and for
retrospective conversions, you often would be able to create a new versatile heuristic by simply providing
remappings into ReproIn as shown in `this issue (documentation is coming) <https://github.com/ReproNim/reproin/issues/18#issuecomment-834598084>`_.

Having decided on a heuristic, you could use the command line::

    heudiconv -f HEURISTIC-FILE-OR-NAME -o OUTPUT-PATH --files INPUT-PATHs

with various additional options (see ``heudiconv --help`` or
`"Usage" in documentation <https://heudiconv.readthedocs.io/en/latest/usage.html>`__) to tune its behavior to
convert your data.

For detailed examples and guides, please check out `ReproIn conversion invocation examples <https://github.com/ReproNim/reproin/#conversion>`_
and the `user tutorials <https://heudiconv.readthedocs.io/en/latest/tutorials.html>`_ in the documentation.


How to cite
-----------

Please use `Zenodo record <https://doi.org/10.5281/zenodo.1012598>`_ for
your specific version of HeuDiConv.  We also support gathering
all relevant citations via `DueCredit <http://duecredit.org>`_.


How to contribute
-----------------

HeuDiConv sources are managed with Git on `GitHub <https://github.com/nipy/heudiconv/>`_.
Please file issues and suggest changes via Pull Requests.

HeuDiConv requires installation of `dcm2niix`_ and optionally `DataLad`_.

For development, you will need a non-shallow clone (so there is a
recent released tag) of the aforementioned repository. Once you have cloned the repository,
you can then install all the necessary development requirements using ``pip install -r
dev-requirements.txt``.  Testing is done using `pytest
<https://docs.pytest.org/>`_.  Releases are packaged using Intuit
auto.  Workflow for releases and preparation of Docker images is in
``.github/workflows/release.yml``.
