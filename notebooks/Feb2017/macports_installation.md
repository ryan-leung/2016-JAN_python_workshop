##Installing Python using Macports (beginner guide)

Original context : https://gist.github.com/titipata/cfae77f5f7ac7f24368d

I think package management system is good for long-term installation. Since lab members use a lot of Apple product,
I wrote Macports documentation which is package management system for Mac OSX which hopefully will be useful for members who use Mac. Note that this is not an official document but probably an easy way to get start with Macports. Macports depends mostly by its community and ones who update the port. We may have to migrate our ports when Mac announce new operating system. From my experience, it is normal to have some port problem with macports when new Mac operating system, for example, when Maverick or Yosemite was announced or when new XCode version were updated. It will
take some time (a day or a week) for them to update the new port that are compatible
with new operating system. But yeah, most ports work very well even though OS changes since
the community is very active.

### Macports

In order to install Macports. Firstly, we need to install `Xcode` (see also the version of Xcode
you have is not too old) and its commandline tools, X11 and some other things first. Then, we
will install macports from the [macports website](https://www.macports.org/install.php) (see your OS and download the right one). All available ports are on this [site](https://www.macports.org/ports.php). Note that the port name that are related to `python2.7` will be in the form of `py27-...` or `py-...` e.g. `py27-ipython`, `py27-pandas`, `py27-numpy`, `py27-scipy`, `py27-scikits-lean`, `py27-matplotlib`. The name is different from `pip` install.
More note is to make sure that we have installed the command line in XCode. In order to
check whether we have installed commandline tools in XCode and have Macports up-to-date, you can type as follow:

```bash
sudo xcode-select --install
sudo port -v selfupdate
```

As I have seen from now selfupdate should not take that long time. If it takes too long, probably
something was wrong such as XCode version or Macports that we have installed. Also add `macports` path to `~/.bash_profile`
to include `macports` path (i.e. `emacs ~/.bash_profile`) as follows:

```bash
export PATH="/opt/local/bin:/opt/local/sbin:$PATH"
```

### Installing Python 2.7

After we get macports installed, there are almost 18000 ports that we can install from `git`, `emacs`, `vim`
to video downloader like `youtube-dl` or music player like `cmus`. A lot of ports will have dependencies (we can check on the website above). When we download one port, its dependencies will come together. However, when we
want to uninstall each port, we again need to uninstall its dependencies first before uninstall it.
For `python27` (or `python version 2.7`), I have some recommendation command line as follow:

```bash
sudo port install vim
sudo port install emacs
sudo port install git
sudo port install python27
sudo port install py27-matplotlib py27-numpy py27-scipy py27-ipython +notebook
sudo port install opencv +python27
sudo port install py27-pip
```

`Emacs` and `Vim` are classic text editors and also in this case, we use it to prove that our installation
before worked. `pip` is a package management to help you install python packages. We can use
`pip` to install python library and update library. And to check recent version, install package and upgrade, we can use following commands:

```bash
pip list --outdated
sudo pip install 'package name'
sudo pip install --upgrade 'package name'
```

Additional useful library including `pandas`(data analysis library) and `scikits-learn`(machine learning library):

```bash
sudo port install py27-pandas py27-scikits-learn
```

### Installing from source code

Sometimes, if you want to install developing version of the package or you want to install package that 
`macports` does not provide. We can use `git` to clone source code directly and install. Here is an 
example of how to install `tornado` package (other packages works in similar flow).

```bash
git clone https://github.com/tornadoweb/tornado
cd tornado
python setup.py build
sudo python setup.py install
```

### Select Python version and run

We want to set usual `python` command to replace `python27` and also `ipython`. This is the way to setup,

```bash
sudo port select --set python python27 (or python33 in the future)
sudo port select --set ipython ipython27
```

We can run python by typing given command line in the terminal by either of this command line:

```bash
ipython
ipython notebook --profile 'profile_name'
```

### Some useful Macports command line

The full documentation [link](https://guide.macports.org/) is given if you want to search for more command. 
However, I have some command that I mostly use including how to install specific port, uninstall ports and search ports.

To uninstall or uninstall with dependent port:
```bash
sudo port uninstall 'portname'
sudo port uninstall --follow-dependents 'portname'
```

This command will print the list of port that we have installed and will note active if the port
are currently in used
```bash
port installed
```

This command line is used to update the Macport itself. Options can be added such
as `-d`, `-v`, `-f`, to see how it works search for `bash options`, for example.
```bash
sudo port selfupdate
```

Once in a while, we can run this line to uninstall inactive ports.
```bash
sudo port uninstall inactive
```

I know sometime we mess up the port and may have no way to fix it. This is how to uninstall
all ports and lets start installing all again!
```bash
sudo port -fp uninstall installed
```

Another useful port commands include:
  - `port search <part_of_port_name>` search ports that are closed/related to the given ports
  - `port dependents <port_name>` list all dependent ports under `<port_name>`


#### Some UNIX command line
  - To see the type history that you used before, use `history`
  - Simple change the directory `cd ...` (`cd ..` is to move up one directory)
  - See the directory of python that we currently used `which python / which ipython`
  - `Emacs` shortcuts [link](http://www.shortcutworld.com/en/linux/Emacs_23.2.1.html)
  - How to create and custom ipython profile [link](https://github.com/titipata/klab_ipython_notebook)
