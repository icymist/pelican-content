Title: Install Anaconda for a painless Python experience
Date: 2015-03-27 16:00
Category: How To
Tags: linux, python


I have recently migrated from the Enthought Python Distribution to the Anaconda Python Distribution.
Using anaconda has been a breeze compared to Enthought.
Somehow, I couldn't get around my head to understand the User and System enviroments in Enthought.
Also, I didn't quite understand how the command line management is different from the GUI.
With Anacond it has been pretty simple.
Just install, clone to get a new environment and start working.


To install a python environment for my blog using pelican, I just had to do the following.

1. Install anaconda and add anaconda python to your path.

        :::bash
        chmod +x Anaconda-2.1.0-Linux-x86_64.sh
        ./Anaconda-2.1.0-Linux-x86_64.sh

1. Clone the `root` environment to a new environment named `pelican`.

        :::bash
        conda create -n pelican --clone root

1. Install pelican and markdown. markdown wasn't present in the base Anaconda distribution.

        :::bash
        pip install pelican

1. Change to the new pelican python environment and start working.

        :::bash
        source activate pelican

1. That was it. And, to get back to the root environment:

        :::bash
        source deactivate


Other useful conda commands.

* Info about available environments.

        :::bash
        conda info -e

* Completely remove an environment.

        :::bash
        conda remove -n <name of environment> --all
