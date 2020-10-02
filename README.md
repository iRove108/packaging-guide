
# Packaging in Python: A Crash Course

Do you have a lovely project that you want to share with the world, but you don't know how to get your project onto a platform like PyPi where other users can easily install your library? Fear not — in this guide, you'll learn how to create a Python package, build it, and upload it to PyPi.

## Establishing the Packaging Directory Structure

You will first want to configure your directory structure to mimic the following, where `package_project` is the name of the main project directory and `my_pkg` is the name of your new package:

    package_project
        LICENSE
        README.md
        my_pkg
            __init__.py
        setup.py
        tests

The `__init__.py` file will be called by default when the package is imported on the user's computer, so make sure to expose necessary user-facing interfaces in this file.

## The `tests` Directory
You can leave the `tests` directory empty for now, but it may become useful in the future when you wish to run unit tests.

## Writing a README
Your `README.md` should tell users about how to install, use, and contribute to your project. The best projects have READMEs which are original, concise, and compelling. Write a README that only you could've written, but not only you can understand.

## Licensing your Package
The LICENSE is where you can post the terms of use for your package. You can find some of the basic features of popular open source licenses [here](https://tldrlegal.com). You can find the full text of each license from the [Open Source Initiative](https://opensource.org/licenses).

## Editing the setup build script
`setup.py` is a script that uses [setuptools](https://packaging.python.org/key_projects/#setuptools) to tell Python about the metadata and relevant code files for your package. Here's a basic `setup.py` file:

    import setuptools

    with open("README.md", "r") as fh:
        long_description = fh.read()

    setuptools.setup(
        name="my-pkg", 
        version="0.0.1",
        author="Author Name",
        author_email="info@info.org",
        description="An incredibly nifty package for very cool coders",
        long_description=long_description,
        long_description_content_type="text/markdown",
        url="https://github.com/exampleuser/my-pkg",
        packages=setuptools.find_packages(),
        classifiers=[
            "Programming Language :: Python :: 3",
            "License :: OSI Approved :: MIT License",
            "Operating System :: OS Independent",
        ],
        python_requires='>=3.6',
    )

To ensure your package name does not conflict with other packages, make sure you edit the `name` parameter of `setup()` to include your username. For information on how to configure the other parameters, see [Python's packaging documentation for `setup()`](https://packaging.python.org/guides/distributing-packages-using-setuptools/#setup-args).

## Creating and Uploading Your Distribution Archives

Great, so you now have the source code for your project, your `README.md` and `LICENSE`, and a `setup.py` file. But what does this `setup.py` file actually do? 

This file will help python build your source code into a **wheel**. Wheels make it easier for other users to install your Python package, as a wheel is a **built distribution**, meaning that it is directly ready to install and does not need the build stage required for **source distributions**, which are just the collection of files needed for pip to build **and** install your package. 

In order to build your package into a wheel to upload to PyPi, you want to install `setuptools` and `wheel`:
```
pip install --user --upgrade setuptools wheel
```

Next, you want to use the `setup.py` file you wrote in the previous section to build your package into a wheel. Run the following command in the top level directory, the same directory where `setup.py` is.
```
python3 setup.py sdist bdist_wheel
```

This will create two directories — a directory called `my-pkg.egg-info` and a directory called `dist`. The first directory just contains metadata for your package. We care about what's in the second repo — a `.whl` file and a `.tar.gz` file. The `.whl` file is the built wheel for your package, while the `.tar.gz` contains the source distribution. Usually, pip will try to install your wheel, but if that fails it will resort to building from your `.tar.gz` file.

Now, you can upload your package to the Python Package Index. Firstly, register an account on  PyPi at https://pypi.org/account/register/. Then verify your email and create a PyPi API token [from your account settings](https://pypi.org/manage/account/). Make sure to copy the API token somewhere safe before you leave, as the token will only appear once!

You can now upload your package using Twine:

```
python3 -m pip install --user --upgrade twine
python3 -m twine upload dist/*
```

A username and password prompt should appear. Enter `__token__` for the username and then enter your API token for the password.

## Installing Your Package

To install your package, simply type

```
pip install my-pkg
```

Your package should now automatically be installed. To verify that your package works, you can open up a new python shell and try importing it.

```
python
import python
```



