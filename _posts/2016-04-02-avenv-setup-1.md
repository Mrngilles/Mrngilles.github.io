---
layout: post
title: The development setup for AutoVirtualEnv [Part 1]
description: Setting up of my new AutoVirtualEnv project
modified: 2016-04-02
tags: [python,virtualenv,projects]

---

For some days now, I have been working a bit every day on my new
project, **AutoVirtualEnv**, which you can read about in my
[previous post]({% post_url 2016-03-28-autovirtualenv %}). And I am
quite happy about how things are going.

Today, I am going to show you my starting setup, as I think that
everyone needs to have some infrastructure going before writing even a
single line of code. What I am going to setup today is:

- Creation of a git repository
- The creation of a virtual environment for development, with the
  development tools I want, and the packages required by AutoVirtualEnv
- The creation of a package, distribution ready
- The setup of the test framework
- The initialization of the documentation.

Let's get started !

# Git repository

## Creation of the repository

To ease the process of creating the repository, I like to first create
my repository on [GitLab](https://gitlab.com) (you can also use
[GitHub](https://github.com)). This way, once the repository is
created, I simply have to clone it wherever I want, and it is ready to
get started. To create a repository in [GitLab](https://gitlab.com),
you can follow the
[instructions](http://doc.gitlab.com/ce/gitlab-basics/create-project.html)
on the [official documentation](http://doc.gitlab.com/ce/).

Once you have created your repository, you can just enter your
terminal and enter:

```bash
$ git clone <link_to_your_repository>
```

where you want to clone your repository. In my case, it would be:

```bash
$ git clone https://gitlab.com/Mrngilles/auto-virtualenv
```

Now, all there is to do, is to get started, and a good starting point
is creating common files in your repository

## Common files

The first file to create is the `README.md`. It will give information
about your project to anyone getting to your repository page. It
describes the project, the installation process, dependencies and any
other useful information. However, in our case, it was created with
the repository, so we *just* will have to fill it. For now, it is
filled only with the project description, but I will expand it as soon
as I deem it necessary.

Next, we will include our `LICENSE` file. This file will defines the
way you authorize (or not) the distribution of the project. In my
case, I chose to include a **GNU GPLv3** license, so that the project
can be reused quite easily. To do this, in
[GitLab](https://gitlab.com), there is an `Add License` directly on
your project dashboard. Then, you just have to copy the
[license](https://opensource.org/licenses/GPL-3.0), choose a commit
message, and that's it! Oh, and don't forget to `git pull` from your
local repository.

One other very important file to add is your `.gitignore` file. Do
define this file and update it on a regular basis to avoid cluttering
your git environment with all sort of files you do not want to share,
like build files. As we are starting a python project, a good initial
`.gitignore` file can be found
[here](https://github.com/github/gitignore/blob/master/Python.gitignore). However,
I prefer starting with an empty one and adding elements as I go
along. Still, we will add a few elements to start with:

```
.gitignore


*.egg-info
*__pycache__*
*.pyc
.cache
.eggs
```

Finally, I like to add a file with all the next things to do, which I
will name (creatively) `TODO`.

Now that we have our project started, let's create our python package!

# Python package

To create a package, we will first create a repository, and make it a
*Python package*, meaning we create an `__init__.py` file into it. To
do this,

```bash
$ mkdir avenv
$ touch avenv/__init__.py
```

We then have to create our python `setup.py` script. At the root of
the project, we create the file `setup.py` and insert into it

```python
from setuptools import setup, find_packages
from os import path

here = path.abspath(path.dirname(__file__))

with open(path.join(here, 'README.md'), encoding='utf-8') as f:
    long_description = f.read()

setup(
    name="avenv",
    version="0.0.0",
    description="Configuration based management of virtual environments",
    long_description=long_description,
    url="https://gitlab.com/Mrngilles/auto-virtualenv",
    author="Marin Gilles",
    author_email="mrngilles@gmail.com",
    license="GNU GPLv3",
    classifiers=[
        "Development Status :: 1 - Planning",
        "Environment :: Console",
        "Intended Audience :: Developers",
        ("License :: OSI Approved :: GNU General Public License v3 or "
         "later (GPLv3+)"),
        "Natural Language :: English",
        "Programming Language :: Python :: 3.5"
        "Topic :: Utilities"
    ],
    keywords="deployment installation",
    packages=find_packages(exclude=["tests*", "docs"]),
    install_requires=["pyYAML", "virtualenvwrapper"]
)
```

thus describing our package, and making it distributable. I tried to
make it as full as, possible, but as we will see later, we are going
to need to add elements to it.

# The end word

Of course, we are not done setting up our environment. We just covered
what I consider to be standard python project configuration. In the
[next]({% post_url 2016-04-07-avenv-setup-2 %}) article, we will create our virtual environment for development,
and setup testing with [py.test](http://pytest.org/latest/).

Don't hesitate to [contact]({{ site.url }}/about) me directly if you have any question, want
to participate, or just want to talk!

<!--  LocalWords:  informations
 -->
