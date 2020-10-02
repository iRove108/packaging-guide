# Establishing the Packaging Directory Structure

You will first want to configure your directory structure to mimic the following, where `package_project` is the name of the main project directory and `my_pkg` is the name of your new package:

    package_project
        LICENSE
        README.md
        my_pkg
            __init__.py
        setup.py
        tests

The `__init__.py` file will be called by default when the package is imported on the user's computer, so make sure to expose necessary user-facing interfaces in this file.

# The `tests` Directory
You can leave the `tests` directory empty for now, but it may become useful in the future when you wish to run unit tests.

# Writing a README
Your `README.md` should tell users about how to install, use, and contribute to your project. The best projects have READMEs which are original, concise, and compelling. Write a README that only you could've written but not only you can understand.

# Licensing your Package
The LICENSE is where you can post the terms of use for your package. You can find some of the basic features of popular open source licenses [here](https://tldrlegal.com). You can find the full text of each license from the [Open Source Initiative](https://opensource.org/licenses).

# Editing the setup build script
`setup.py` is a script that uses [setuptools](https://packaging.python.org/key_projects/#setuptools) to tell Python about the metadata and relevant code files for your package. Here's a basic `setup.py` file:

    import setuptools

    with open("README.md", "r") as fh:
        long_description = fh.read()

    setuptools.setup(
        name="my-pkg-YOUR-USERNAME", # Replace with your username!
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
