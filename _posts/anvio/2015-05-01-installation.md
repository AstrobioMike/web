---
layout: post
title: "Installing anvi'o"
excerpt: "Instructions to install the platform."
modified: 2015-05-01 
tags: []
categories: [anvio]
comments: true
---

{% include _toc.html %}

There are multiple ways to install anvi'o.

This article explains basic steps of installing anvi'o using rather conventional methods. You may also be intersted in these posts if you think they would serve you better:

* [OS X installer for anvi'o]({% post_url anvio/2015-08-20-installation-on-mac %}) (for Maverick and Yosemite).
* [Docker image for anvi'o]({% post_url anvio/2015-08-22-docker-image-for-anvio %}) (for an instant, and painless installation of anvi'o on a server system).

**Regardless** of which installation method you'd like to go with, you should take a look at these anvi'o requirements before going any further:

* [Chrome Web Browser](https://www.google.com/chrome/browser/desktop/). Chrome should be not only installed on your system, but unfortunately it should also be the default browser (otherwise everytime interactive interface pops up, you will need to copy-paste the address to a Chrome window). Anvi'o does not support any other browser, and __it will not perform optimally__ on others.

* [DB Browser for SQLite](http://sqlitebrowser.org/). Anvi'o uses SQLite to create self-contained databases to store information. There are many bindings for many programming languages to access to these database files and explore them, and it is also possible to use `sqlite3` program from the terminal to play witht them. DB Browser for SQLite is a very easy-to-install open-source software that does what `sqlite3` is doing with a nice graphical interface. I urge you to stick with the terminal as much as possible, but having a GUI option is always a nice thing.

* [MyRAST](http://blog.theseed.org/servers/). This is optional, and it is useful only if you are planning to do metagenomics with a focus on bacteria. In that case MyRAST can be quite useful, at least to get a broad idea about what is going on in your data. If you type `svr_assign_to_dna_using_figfams` on your terminal and and do not get an error, you have it (press `CTRL+C` to quit). You need to know that your annotations with MyRAST will be *OK* for human gut, but you shouldn't expect too much from it if you are working with other environments.


Please post a comment down below if you have any questions about installation. You may want to consider opening an <a href="https://github.com/meren/anvio/issues">issue</a> for more technical problems.

Here I would like to thank Inés Martínez, Rika Anderson, and Sharon Grim for helping me a lot by volunteering themselves to test the installation.


## An overview of anvi'o dependencies

You need to make sure your system does have all the following software if you are going to follow the installation instructions on this page (it is not as scary as it looks, you will be fine):

{: .notice}
If you are using Ubuntu, there is a little recipe here to install anvi'o with all of its dependencies: https://gist.github.com/meren/f1e674f774a30a209d82

* [Prodigal](http://prodigal.ornl.gov/) (go to your terminal, type `prodigal -v` if you get an error, you need to install it, __if the version number is smaller than 2.6.2__, you need to update it). Here is a quick way to install the 2.6.2 version, but feel free to do visit the [latest releases page](https://github.com/hyattpd/prodigal/releases/) and do it yourself (the first line will not work if you don't have wget, but you can get wget installed esily typing `sudo port install wget` if you are using MacPorts system on your Mac computer):

<div style="padding-left:30px">
<pre>
wget https://github.com/hyattpd/Prodigal/archive/v2.6.2.tar.gz
tar -zxvf v2.6.2.tar.gz && cd Prodigal-2.6.2/ && make
sudo cp prodigal /usr/bin/
</pre>
</div>

* [HMMer](http://hmmer.janelia.org/) (go to your terminal, type `hmmscan`, if you get an error, you need to install this one). It is quite easy to install. Go to the downloads page, [http://hmmer.janelia.org/download.html](http://hmmer.janelia.org/download.html), download the *source* for the latest version, unpack it, go into that directory with your terminal, and then type (don't forget to check whether it is installed properly by typing `hmmscan` again after installation):

<div style="padding-left:30px">
<pre>
./configure && make && sudo make install
</pre>
</div>

* [SQLite](http://www.tutorialspoint.com/sqlite/sqlite_installation.htm) (go to your terminal, type sqlite3, if it gives you an error, you need to install this one). There is installation instructions on the web page if you follow the link. Or you can install it by typing `sudo port install sqlite3` if you are using the port system on your Mac.

* [GSL](http://www.gnu.org/software/gsl/), which is the GNU Scientific Library. It is quite straightforward. If you are using MacPorts, you can install `gsl`, `gsl-devel`, and `py27-gsl` packages from the terminal using `port install` (Rika tells me homebrew on Mac works, too). Otherwise, try these commands and you should be OK:

<div style="padding-left:30px">
<pre>
wget ftp://ftp.gnu.org/gnu/gsl/gsl-latest.tar.gz
tar -zxvf gsl-latest.tar.gz
cd gsl-*
./configure && make && sudo make install
</pre>
</div>

* [numpy](http://www.numpy.org/). You don't need to install numpy if you get no complaints back when you type `python -c "import numpy"` in your terminal. If you do get an import error, then you need to install numpy. You can try this:

<div style="padding-left:30px">
<pre>
sudo pip install numpy
</pre>
</div>

* [Cython](http://cython.org/). Similar to the numpy case. Test whether you are good to go by typing `python -c "import Cython"` in your terminal, and install it by running this if there is an import error:

<div style="padding-left:30px">
<pre>
sudo pip install Cython
</pre>
</div>

* [HDF5](https://www.hdfgroup.org/HDF5/). If you are not sure what it is, you probably don't have it. If you are using macports on your Mac, you can get away with `sudo port install hdf5`, otherwise you can run these commands on your terminal:

<div style="padding-left:30px">
<pre>
wget http://www.hdfgroup.org/ftp/HDF5/current/src/hdf5-1.8.15-patch1.tar.gz
tar -zxvf hdf5-1.8.15-patch1.tar.gz
cd hdf5-1.8.15-patch1
./configure && make && sudo make install
</pre>
</div>

## Installation

You can either install a stable release of anvi'o, or you can get a copy of the latest snapshot from the repository (clearly, it is always safer to go with the stable release).

### Installing the latest stable release (safe mode)

The best way to install stable release is to do it through pip. If you are have your dependencies sorted, try running this on your terminal:

    sudo pip install anvio

Pleaes keep an eye on the output to make sure there are no errors.

If the installation finishes properly, run this in your terminal:

    anvi-profile --version

If everything looks alright, you are golden. Now you can run `mini test` if you would like to make sure everything else works as expected.

If you get a '*command not found*' error despite a successful installation, this would mean that the directory where your anvi'o programs live is not listed in your `PATH` variable. Please [follow this post]({{ site_url }}/projects/issues/missing-binaries.html) to fix that first (and once you are done with it you can try running the `mini test`).


### Installing or updating from the current codebase (semi-pro)

If this is your first time with the codebase, get a fresh copy (with all the submodules necessary):

    git clone --recursive https://github.com/meren/anvio.git

Then go into the anvio directory, and then run the installation:

    cd anvio
    sudo python setup.py install

If you already have the codebase, and if your purpose is to _update_ your already existing installation, you are going to need to run these commands from within the anvio directory instead of the ones above:

    git pull
    git submodule update --init --recursive
    sudo python setup.py install

No errors? Perfect. Run the mini test!

### Installation for developers (you're a wizard, arry)

If you are planning to do this you need no introduction, but I will give you one anyway. Clone the codebase into a `$DIR` you like:


    cd $DIR
    git clone --recursive https://github.com/meren/anvio.git

Then edit your `~/.bashrc` or `~/.bash_profile` files depending on your system configuration to update your `PATH` and `PYTHONPATH` environment variables:

    export PYTHONPATH=$PYTHONPATH:$DIR/anvio/
    export PATH=$PATH:$DIR/anvio/bin:$DIR/anvio/sandbox

Because you didn't run "build", your C extensions will not be compiled. This is the fast way to get them compiled and put in the right place:

    cd $DIR/anvio
    python setup.py build
    cp build/lib.*/anvio/*so anvio/

That's it.

After sourcing your `.bashrc` (or `.bash_profile`) and get the new environment variables set, you should be able run the 'mini test'.

Now you can edit the codebase, and test it, without re-installing anvi'o over and over again.

## Running the "Mini Test"

"Mini test" is [a tiny shell script](https://github.com/meren/anvio/blob/master/tests/run_mini_test.sh) that runs almost everything implemented in anvi'o on a very small dtaset.

If you have a proper installation, you shouldn't get any errors when you run it.

If you installed anvi'o via `pip` (following the safe mode), you can go to an empty directory, and type these (don't forget to replace the version number (which is 1.2.0 in this example) with whatever version you have installed. If you are not sure, type `anvi-profile -v`):

    git clone -b v1.2.0 --depth=1 https://github.com/meren/anvio.git
    cd anvio/tests
    ./run_mini_test.sh



If you installed anvi'o from the codebase, you can go to the anvi'o source code directory, and simply type these:

    cd tests
    ./run_mini_test.sh

Upon the successful completion of the mini test run, your browser should popup to take you to the interactive interface. When you click that 'Draw' button, you should see something like this (this is the old version of the anvi'o interface, and it shall stay here so we remember where we came from):

<div class="centerimg">
<a href="{{ site.url }}/images/anvio/misc/mini-test-screenshot.png"><img src="{{ site.url }}/images/anvio/misc/mini-test-screenshot.png" width="50%" /></a>
</div>

All fine? Perfect! Now you have a running installation of anvi'o!

Maybe you would like to continue with the [other posts on the platform]({{ site.url }}/projects/anvio)?