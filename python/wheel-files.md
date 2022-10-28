- A wheel file is a zip archive with a specially crafted name that tells installers what Python versions and platforms are supported
    - It is a ready to install format
    - filename is broken into parts:
    `{dist}-{version}(-{build})?-{python}-{abi}-{platform}.whl`
- Python Wheels made the installation faster and more efficient
    - They are smaller in size than source distributions -> lower network latency
    - Avoid building stage -> faster
    - Avoids executing setup.py code
    - No need for a compiler for extension modules
    - pip automatically generates .pyc files
- **Source Distributions** are the source code and extension modules (mostly written in C/C++) bundled together. Those extensions are compiled at the user side **NOT** developer side
    - They also contain metadata directory called `<package-name>.egg_info`. This metadata helps with the building and isntalling of the package
    - It is the result of `python setup.py sdist` command
- **Wheel files** are sometimes provided by packages on PyPI
    - Each OS has its own wheel file
    - Pip prefers wheels over source distributions when trying to install a package
- Example wheel filenames: 
    - `cryptography-2.9.2-cp35-abi3-macosx_10_9_x86_64.whl`
        - `cryptography` is the name of the package
        - `2.9.2` is the package version which is formatted according to PEP 440 recommendation
        - `cp35` is CPython with Python version 3.5
        - `abi3` is version 3 of Application Binary Interface
        - `macosx_10_9_x86_64`:
            - `macosx` MacOs operating system
            - `10_9` is the version of MacOs
            - `x86_64` is the x86_64 instruction set architecture
    - `chardet-3.0.4-py2.py3-none-any.whl`
        -  `chardet` is the package name
        - `3.0.4` is the package version
        - `py2.py3` works on any version of Python 2 & 3
        - `none` means ABI is not factor
        - `any` works virtually on all platforms
- We can view the contents of the wheel file using `unzip`
- We can force pip to only install wheel files with `--no-binary`
    - `:all:` would apply this not only to the package we are installing but to all its dependencies
- Since there are so many variants of Linux such as CentOS, Debian, etc., package developer may have to provide many wheels for different variations of Linux. This is especially true if the package has module extensions written in C/C++ and may potentially have issues due to compilation error. There are platform tag family:
    - `manylinux1`
    - `manylinux2010`
    - `manylinux2014`
- Types of wheels:
    - **Universal wheels**: support both Python 2 & 3 on all platforms
    - **Pure-Python wheels**: support either Python 2 or Python 3 on all platforms, but not both
    - **Platform wheels**: support specific Python version and platform
- To build s pure Python wheel:
    - `python setup.py sdist bdist_wheel`. By default, it will be stored in `dist` directory
    - `python setup.py sdist -d dir_name bdist_wheel -d dir_name`
- To build universal wheel:
    - Use .cfg file by adding: 
    ```bash
    [bdist_wheel]
    universal = 1
    ```
    - Use `python setup.py sdist bdist_wheel --universal`
    - Add this line to setup.py file: `options={"bdist_wheel": {"universal": True}}`
- Check resources to build platform wheels or manylinux wheels
- We can use CI pipelines such as GithubActions to test the package on multiple platforms
- [check-wheel-contents](https://github.com/jwodder/check-wheel-contents) is a tool that helps detecting any problems with the wheel file
- [TestPyPI](https://packaging.python.org/en/latest/guides/using-testpypi/) allows us to test the wheel file as if it's a real thing:
    - We first upload it to TestPyPI: 
    ```bash
    python -m twine upload --repository-url https://test.pypi.org/legacy/ dist/*
    ```
    - Then try to install it and see if the wheel file works correctly: 
    ```bash
    python -m pip install --index-url https://test.pypi.org/simple/ <pkg-name>
    ```
- We can use [twine](https://github.com/pypa/twine) tool to upload the package to PyPI:
    - Update twine: `python -m pip install -U twine`
    - Upload package: `python -m twine upload dist/*` which uploads both source distribution sdist and wheel file bdist_wheel. By default they will be is dist directory
