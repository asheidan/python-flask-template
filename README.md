# Template for getting started with Flask and Python

The easiest way of using Flask (and/or other libraries) in a Python project is
to create something called a /virtual environment/ (virtualenv usually for
short). This is really just a folder to which python and all dependencies are
copied. This isolates it from the system-wide installation of python and allows
you to have different libraries for different project.

The 2 largest downsides are:
1. You have to use the python-binary that's in the virtualenv (the folder) when
   you are running and testing.
2. You can't really move the virtualenv once it is created. But it is easy to
   automate the creation of the virtualenv. So don't move it, delete the old
   one and create a new one instead.


## Getting started

To get started there are a few steps:

1. Create the virtualenv
2. Install dependencies into the virtualenv
3. Test your setup to make sure it works


### Create the virtualenv

I suggest keeping your virtualenv in the project folder since this make a lot
of things easier. But it might be worth knowing that some tools keeps your
virtualenv in a special hidden folder, so all of your virtualenvs are in the
same place.

The name `venv` is very common for virtualenvs that are kept in the project
folder, so common in fact so VSCode will usually automatically detect
virtualenvs if they have that name.

So go to your project folder:
```sh
cd ~/awesome-project
```

Create the virtualenv named venv:
```sh
virtualenv venv
```
This will use the default python installed on your systewm. Check the
documentation for `virtualenv` if you need to use a specific version of python.

All of this of course is dependent on virtualenv (and python) being installed already.


#### Installing virtualenv

Installing virtualenv can be done in way too many ways, I will just list one way for Fedora and one for MacOS.


##### Fedora

Use the system package manager. That will ensure that all other dependencies are installed as well:

```sh
sudo dnf install python3-virtualenv
```


##### MacOS

You probably want to use Homebrew, unless you already know how to install it (but then why are you reading this).

```sh
brew install virtualenv
```


### Install dependencies

Using the same versions for everybody working on a project is something every
project involving more than a single person has to deal with. Every system that
works and, more importantly, are used are good.

With virtualenvs and pip (the dependency manager that usually are automatically
installed as part of your python install) the easiest way to do this is a
`requirements.txt` file. Keep this as well in your project folder.

In `requirements.txt` it is possible to specify exakt versions as well as just
"please install this library, I don't care about the versions".

So start with just specify which libraries you need, one on each line.
Something like this:
```txt
Flask
psocopg2-binary
```

If you want to specify version numbers you can use many ways, but I suggest:
* `==` -- this exact version, nothing else
* `~=` -- this version or "bugfixes to this version"

This would mean that your `requirements.txt` would look like this:
```txt
Flask==2.0.2
psycopg2-binary==2.9.3
```

To install these into your virtualenv you use the pip that's in your virtualenv:
```sh
./venv/bin/pip install -r requirements.txt
```

Examine the output from this to make sure that this doesn't result in any errors. You can also make sure that your dependencies are installed into your virtualenv by starting the python in your virtualenv and try to import the dependency:
```sh
./venv/bin/python -c 'import flask'
./venv/bin/python -c 'import psycopg2'
```
Neither of these should give you any errors, they might not even give you any output.

### Test run your app

If you have gotten this far you should be able to run your flask-app by running the following in your project folder:
```sh
./venv/bin/python app.py
```
Given that your app is actually in `app.py`.
