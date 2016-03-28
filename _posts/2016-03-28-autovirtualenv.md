---
layout: post
title: AutoVirtualEnv development
description: "The beginning of a new way to manage Python Virtual Environments"
modified: 2016-03-24
tags: [virtualenv, python]

---

I wanted to start working on my simulation library as soon as I finished the
introductory post, and I did. However, I noticed that there is no easy way to
get some python source code, and in one command, install a python virtual
environment with all the project dependencies, development tools and testing
tools. Also, if you're using virtualenvwrapper, although you have completion in
your command line interface, you quite often don't want to type the name of the
environment you will be working on for a project. Of course, you could be using
something like autoenv, or an equivalent, but you usually will not add the
.autoenv file to your repository, and will not share it with others. Then, how
to improve all of this.

## What will I do then ?

So I had the idea of creating a new package that would ease all of this. Using
**AutoVirtualEnv**, you will be able, in a single command to:
- Create multiple environments based on a configuration file
- Have environments defined as *development* or *test*, installing your
  favorite tools in a given virtualenv
- Choose the python version for an environment
- Create environment based on others, with only minor modifications
- Share the development and test environment in your project, directly from
  your project repository
- And maybe more, as I think about other functionalities

I will implement this project before my simulation library. Indeed, I think
this is an easier project, from which I can learn a lot, and learn not only
python but also all the related tools.

My plan is to wrap around the
[virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/en/latest/) and
[virtualenv](https://virtualenv.pypa.io/en/latest/) libraries. The developers
of those two libraries have already done an amazing work and their projects are
well supported. I use them every time I need to work on some python, and
absolutely love them. I also plan to have a support for conda environments,
once I have a first version released. Conda is a tool developed by
[Enthought](https://www.enthought.com/), mixing the capabilities of
[virtualenv](https://virtualenv.pypa.io/en/latest/),
[virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/en/latest/) and
[pip](https://pypi.python.org/pypi/pip/). However, unlike
[pip](https://pypi.python.org/pypi/pip/), it can also install non python
libraries, making the installation of libraries like
[mayavi](http://code.enthought.com/projects/mayavi/), or
[pyQt](https://riverbankcomputing.com/software/pyqt/intro) really simple.

I will developing the library for python 3 first, and might think about
porting it back in the future. I understand that a lot of people still use
python 2, and that it is still distributed on many Linux distributions by
default, but python 3 is full of new things, and will probably still be here
once python 2 disappears.

I will describe the structure of the project, and what I tried and do right
from the very beginning in the next post. In the mean time, let me tell you
which tools I am going to use.

## Tools

### [Pytest](http://pytest.org/latest/)

[Pytest](http://pytest.org/latest/) is an amazing testing library. What I like
most about it (compared to [nose](https://nose.readthedocs.org/en/latest/)), is
the way the results are displayed, on a file by file summary, with total tests
percentage bar, and with well separated error and failure reports. It also
integrates quite easily with coverage and has a lot of nice plugins (I like to
use Pytest-sugar to improve even more the looks of the results).

### [Sphinx](http://www.sphinx-doc.org/en/stable/)

I would be lynched if I did not use this library for the project
documentation. It is the most widely used documentation package in python, and
is very easy to use. You just have to write .rst files, write properly your
docstrings, and creating the documentation is as easy as `make html`, or "make
latexpdf", or even `make man`, outputting your documentation in the desired
format. The rst format also allows you to write your documentation as ipython
notebooks and export them. For more information, look at my post on
[Packtpub](https://www.packtpub.com/books/content/using-jupyter-write-documentation).

### [Tox](https://tox.readthedocs.org/en/latest/)

[Tox](https://tox.readthedocs.org/en/latest/) is a tool to automate the testing
on multiple python environments, with different configurations. It creates
temporary virtual environments for testing, allowing to have it run the same
tests on python from version 2.6 to 3.5, run tests with different options, and
about every single combination you can imagine with a single command,
`tox`. Although the first run may be slow, because Tox must create all
environments and install all dependencies, it will be much faster (and more
importantly simpler for you) from the second time on.

### [Git](https://git-scm.com/)

I guess this was pretty obvious, but I think that it is one of the most
important tools during development. It allows to track your work, share it,
allow others to contribute, gives you a backup in the worst case... However,
even though a lot of open-source projects are hosted on
[GitHub](https://github.com/), I will be hosting this one on
[GitLab](https://gitlab.com/). First, because I like the open-source model
better, but also, I think they have made a pretty amazing work in developing
their project. I am also thinking about self-hosting, and I would be able to
get it running on my machine (and for free !). You can find the repository
[here](https://gitlab.com/Mrngilles/auto-virtualenv). Keep in mind that at the
time I am writing this article, the project is still in its infancy.

## The end word

I am really glad to be working on such a project. I will do my best to explain
as clearly as possible my development train of thoughts, and will try to
develop using the best possible methods I can find, read about and apply. I am
planning on releasing a first version within 3 months (If I'm not overloaded
with my day job). Don't hesitate to contact me directly if you have any
question, want to participate, or just want to talk!
