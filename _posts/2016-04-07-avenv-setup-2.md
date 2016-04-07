---
layout: post
title: The development setup for AutoVirtualEnv [Part 2]
description: Setting up of my new AutoVirtualEnv project, part. 2
modified: 2016-04-02
tags: [python,virtualenv,projects,testing]

---

In the [previous article]({{ post_url }}avenv-setup-1 ), we set up
our git repository for the AutoVirutalEnv project, and created the
package. Today, we will create our development virtual environment, install the
packages we want, and put our test system up. Let's get started!

# Setting up the virtual environment

## Creating the environment

To create our virtual environment, we will obviously be using
[virtualenv](https://virtualenv.pypa.io/), but we will be using it
through
[virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/),
allowing easier management of our environment, but also an easy way to get back
to work on our project. In the following, I am assuming you already have
installed them, but if you have not, I will let you follow the official guides
for
[installing virtualenv](https://virtualenv.pypa.io/en/latest/installation.html)
and
[installing virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/en/latest/install.html).
My advise would be to install them through `pip`, for easier management.

Once you have both of them installed, let's go to our project directory

```bash
$ cd <my/project/directory>
```

and create the virtual environment

```bash
$ mkvirtualenv -p python3.5 -a . avenv
```

Here, we want to create a new virtual environment (`mkvirtualenv`), for which
the python interpreter is python 3.5 (`-p python3.5`), for which the project
path is the current directory (`-a .`), and with the name of `avenv`. I choose
python 3.5 because it is the last stable python version, and there should be
only a few elements that are not compatible with previous python 3 versions. I
am aware that this is probably not the best option, but it is the one I
chose. One very important option is the project path option. By setting this,
it allows a *warp* to the project directory as soon as the virtual environment
is activated, from anywhere. For example, you can be in any directory, if you
type

```bash
$ workon avenv
```

You will activate your virtual environment, and `cd` into
`/my/project/directory` (if you are already using this feature, you probably
already love it. If not, you will once you have tried it!)

Now, we just activate your environment, with the `workon avenv` command we saw
before, and can install our development tools and requirements.

## Installing tools and requirements

For the configuration files, I decided I would be using
[YAML](http://www.yaml.org/) files, thus I need to install
[pyYAML](http://pyyaml.org/). Also, we will obviously need
[virtualenv](https://virtualenv.pypa.io/) and
[virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/), as
we will be wrapping them over. We possibly have to install other packages
later, but this will do as requirement packages for now. To install them, after
we entered our virtual environment, we type

```bash
(avenv) $ pip install pyyaml virtualenv virtualenvwrapper
```

PyYAML needed other dependencies that we installed prior to entering this
command. If you want to install the package, be sure to install those
dependencies.

Then we will install utilities packages. One of the best is
[IPython](https://ipython.org/), which is an alternative python interpreter,
but much better. We also want the debugger which is
[IPython](https://ipython.org/) enabled,
[Ipdb](https://pypi.python.org/pypi/ipdb). It is an alternative to the standard
python debugger, but with welcomed improvements, like tab completion, syntax
highlighting or better tracebacks. To install those two, just type

```bash
(avenv) $ pip install ipython ipdb
```

Finally, we will install our test package, [Pytest](http://pytest.org/). With
that, we will add coverage to our tests, using the
[pytest-cov](https://pypi.python.org/pypi/pytest-cov/), which adds a
[Pytest](http://pytest.org/) option to add coverage to our tests. This package
sits on top of the [coverage](https://coverage.readthedocs.org/), which is the
most popular coverage testing tool for python. To install those,

```bash
(avenv) $ pip install py.test pytest-cov
```

And for eye-candy, I also like to install
[pytest-sugar](https://pypi.python.org/pypi/pytest-sugar/)

```bash
(avenv) $ pip install pytest-sugar
```

Now that we are done with installing all the tools necessary, let us configure
[Pytest](http://pytest.org/) to test only our package tests and run coverage
testing each time. This is going to be a small package, with not that much
tests, so running coverage each time should not pose too much delay, which is
very important if you want people to keep running you tests.

# Testing setup
## [Pytest](http://pytest.org/) configuration

Let us first tell [Pytest](http://pytest.org/) to run **only** our tests, not
all tests found in the current directory (and subdirectories). This is useful
if you install your virtual environment files directly in you project
folder. To do this, create a new file in your project root, called `pytest.ini`,
and in it, write, assuming your test repository is `/my/project/directory/tests`

```ini
[pytest]
testpaths = tests
```

Then, we will add the covering to our tests. For this, we need to declare
[pytest-sugar](https://pypi.python.org/pypi/pytest-sugar/) as a plugin, and run
covering when running the tests. To do this, just edit again your `pytest.ini`
to have it contain

```ini
[pytest]
testpaths = tests
pytest_plugins = pytest-coverage
addopts = --cov=avenv
```

with `avenv` the relative path to the directory containing your sources. The
configuration file I just wrote is exactly the one that I am using in the
development of `AutoVirtualEnv`, and you can find it in the
[official repository](https://gitlab.com/Mrngilles/auto-virtualenv).

With all of this in place, we can write our tests in the `tests` folder, then
just run

```bash
$ py.test
```
[Pytest](http://pytest.org/) will discover all of our tests, and run them
automatically (and [pytest-sugar](https://pypi.python.org/pypi/pytest-sugar/)
will give the tests and awesome look). It will also run
[coverage](https://coverage.readthedocs.org/) and give us a report on the
coverage of our code. Awesome, right?

## Install our package locally

However, there is one last bit that needs to be taken care of. Indeed, to be
able to call our package from our test suite, we need to install our package in
the virtual environment. This is really easy to do, but the first time I setup
a test suite, I banged my head on this problem a lot. So to install your
package, in *editable mode* in `pip`, go to your project root directory, and
type

```bash
(avenv) $ pip install -e .
```

This command will read the information from the `setup.py` file, and create
every necessary file to package your sources, in *editable mode*, meaning you
will still be able to change your sources and the changes will be taken into
account in the `pip` package that was just created.

## Seamless py.test integration

Although we are using [Pytest](http://pytest.org/) for testing, python has a
built-in testing support. And when creating your package, you can define a
custom way to run your tests in `setup.py`, or keep the default
behavior. Then, to run tests with the default scheme, you need to run

```bash
$ python setup.py test
```

We want this command to run our [Pytest](http://pytest.org/) tests. By
following the
[instructions](http://pytest.org/latest/goodpractices.html#integrating-with-setuptools-python-setup-py-test-pytest-runner)
from the official web site, we just need to add, to our `setup.py`

```python
setup(
#...
setup_requires=["pytest-runner", ...],
tests_require=["pytest", ...],
#...
)
```

and create an alias in `setup.cfg`

```ini
[aliases]
test=pytest
```

With those two small modifications, the standard python testing command will
work. Just that easy !

# The end word

Now that our project is set up, we can start working on our code (finally
!). This took some time, but will help us save much more on the long run. Now,
we need to define the architecture of our project, but this will have to wait
for an other day.

Don't hesitate to [contact]({{ site.url }}/about) me directly if you have any question, want
to participate, or just want to talk!
