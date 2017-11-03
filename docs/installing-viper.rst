################
Installing Viper
################
Don't panic if the installation fails. Viper is still under development and
undergoes constant changes. Installation will be much more simplified and
optimized after a stable version release.

Take a deep breath, follow the instructions, and please
`create an issue <https://github.com/ethereum/viper/issues>`_ if you encounter
any errors.

.. note::
   The easiest way to try out the language, experiment with examples, and compile code to ``bytecode``
   or ``LLL`` is to use the online compiler at https://viper.tools.

*************
Prerequisites
*************
Installing Python 3.6
=====================
Viper can only be built using Python 3.6 and higher. If you are already running
Python 3.6, skip to the next section, else follow the instructions here to make
sure you have the correct Python version installed, and are using that version.

Ubuntu
------
16.04 and older
^^^^^^^^^^^^^^^
Start by making sure your packages are up-to-date:
::
    sudo apt-get update
    sudo apt-get -y upgrade

Install Python 3.6 and some necessary packages:
::
    sudo apt-get install build-essential libssl-dev libffi-dev
    wget https://www.python.org/ftp/python/3.6.2/Python-3.6.2.tgz
    tar xfz Python-3.6.2.tgz
    cd Python-3.6.2/
    ./configure –prefix /usr/local/lib/python3.6
    sudo make
    sudo make install


16.10 and newer
^^^^^^^^^^^^^^^
From Ubuntu 16.10 onwards, the Python 3.6 version is in the `universe`
repository.

Run the following commands to install:
::
    sudo apt-get update
    sudo apt-get install python3.6

MacOS
-----
Make sure you have Homebrew installed. If you don't have the `brew` command
available on the terminal, follow `these instructions <https://docs.brew.sh/Installation.html>`_
to get Homebrew on your system.

To install Python 3.6, follow the instructions here:
`Installing Python 3 on Mac OS X <http://python-guide.readthedocs.io/en/latest/starting/install3/osx/>`_

Also, ensure the GMP arithmetic library is installed using `brew`:
::
    brew install gmp

Creating a virtual environment
==============================
It is **strongly recommended** to install Viper in **a virtual Python
environment**, so that new packages installed and dependencies built are
strictly contained in your Viper project and will not alter or affect your
other development environment set-up.


To create a new virtual environment for Viper run the following commands:
::
    virtualenv -p /usr/local/lib/python3.6/bin/python --no-site-packages ~/viper-venv
    source ~/viper-venv/bin/activate
    
If you are using Anaconda run:
::
    conda create -n viper python=3.6
    source activate viper
    
To deactivate the environment simply run:
::
    source deactivate

To find out more about virtual environments, check out:
`virtualenv guide <https://virtualenv.pypa.io/en/stable/>`_.

************
Installation
************
Again, it is **strongly recommended to install Viper** in a **virtual Python environment**. 
This guide assumes you are in a virtual environment containing Python 3.6. 

Get the latest version of Viper by cloning the Github repository, and run the
install and test commands:
::
    git clone https://github.com/ethereum/viper.git
    cd viper
    make
    make test

Additionally, you may try to compile an example contract by running:
::
    viper examples/crowdfund.v.py

If everything works correctly, you are now able to compile your own smart contracts written in Viper.
However, please keep in mind that Viper is still experimental and not ready for production!

.. note::
    For MacOS users:

    Apple has deprecated use of OpenSSL in favor of its own TLS and crypto
    libraries. This means that you will need to export some OpenSSL settings
    yourself, before you can install Viper.

    Use the following commands:
    ::
        export CFLAGS="-I$(brew --prefix openssl)/include"
        export LDFLAGS="-L$(brew --prefix openssl)/lib"
        pip install scrypt

    Now you can run the install and test commands again:
    ::
        make install
        make test
******
Docker
******
A Dockerfile is provided in the master branch of the repository. In order to build a Docker Image please run:
::
    docker build https://github.com/ethereum/viper.git -t viper:1
    docker run -it viper:1 /bin/bash 
To ensure that everything works correctly after the installtion, please run the test commands
and try compiling a contract:
::
    make test
    viper examples/crowdfund.v.py
