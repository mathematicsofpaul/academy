# Anyscale Academy - Tutorials on Ray and Ray-based Libraries

© 2018-2020, Anyscale. All Rights Reserved

Welcome to the [Anyscale Academy](https://anyscale.com/academy) tutorials on [Ray](https://ray.io), the system for scaling your applications from a laptop to a cluster.

This README tells you how to set up the tutorials, it provides a quick overview of its contents, and it recommends which tutorials to go through depending on your interests.

> **Tips:**
>
> 1. Anyscale is developing a free, hosted version of these tutorials. [Contact us](mailto:academy@anyscale.com) for more information.
> 2. This is an early release of these tutorials. Please report any issues:
>    * [GitHub issues](https://github.com/anyscale/academy/issues)
>    * The [#tutorial channel](https://ray-distributed.slack.com/archives/C011ML23W5B) on the [Ray Slack](https://ray-distributed.slack.com)
>    * [Email](mailto:academy@anyscale.com)
> 3. If you are attending a live tutorial event, please follow the setup instructions provided well in advance.
> 4. For troubleshooting help, see the [Troubleshooting, Tips, and Tricks](reference/Troubleshooting-Tips-Tricks.ipynb) notebook.

Read one of the following setup sections, as appropriate, then jump to [**Launching the Tutorials**](#user-content-launching-the-tutorials).

## Setup for Anyscale Academy Hosted Sessions

There is nothing you need to setup, as the hosted environment will provide everything.

However, consider cloning or downloading a release of the tutorial notebooks and supporting software from the [Academy repo](https://github.com/anyscale/academy), so you have a local copy of everything. The `README` provides instruction for local setup, if desired.

> **Tip:** Make sure you download the notebooks you modified during the session to save those changes.

## Setup for a Local Machine

> **Note:** Ray support for Windows is experimental. See [these release notes](https://github.com/ray-project/ray/releases/tag/ray-0.8.6) for details. Alternatively, [Contact Anyscale](mailto:academy@anyscale.com) for a free hosted option for these tutorials.

Follow these instructions to use the tutorials. Note that some commands can take a while to finish.

Clone the [Academy GitHub repo](https://github.com/anyscale/academy) or [download the latest release](https://github.com/anyscale/academy/releases).

Now install the dependencies using either [Anaconda](https://www.anaconda.com/) or `pip` in your Python environment. We recommend using Anaconda.

### Which Python Version?

Python 3.7 is recommended. While Ray supports Python 3.6, a user reported a problem using _locales_. Specifically, the following code throws an error:

```python
import locale
locale.setlocale(locale.LC_ALL, locale.getlocale())
```

This tutorial doesn't use _locales_ specifically, but you may run into problems with your default locale.

While Ray supports Python 3.8, some dependencies used in `RLlib` (the Ray reinforcement library) are not yet supported for 3.8, at the time of this writing.


### Using Anaconda

If you need to install Anaconda, follow the instructions [here](https://www.anaconda.com/distribution/). If you already have Anaconda installed, consider running `conda upgrade --all`.

Run the following commands in the root directory of this project. First, use `conda` to install the other dependencies, including Ray. Then activate the newly-created environment, named `anyscale-academy`. Finally, run the provided `tools/fix-jupyter.sh` script to install a graphing library extension in Jupyter Lab and perform other tasks.

```shell
conda env create -f environment.yml
conda activate anyscale-academy
tools/fix-jupyter.sh
```

If you are using Windows, see the _Fixing Jupyter Lab on Windows_ section below for an alternative to using `tools/fix-jupyter.sh`.

Note that Python 3.7 is used.

You can delete the environment later with the following command:

```
conda env remove --name anyscale-academy
```

### Using Pip

If you don't use Anaconda, you'll have to install these prerequisites first:

* Python 3.7:
	* See notes above about problems with 3.6 and 3.8. Don't use 3.8, but 3.6 may work for you.
    * The version of Python that comes with your operating system is probably too old. Try `python --version` to see what you have.
    * Installation instructions are at [python.org](https://www.python.org/downloads/).
* Pip: A recent version - consider upgrading if it's not the latest version.
	* Installation instructions are at [pip.pypa.io](https://pip.pypa.io/en/stable/installing/).
* Node.js: Required for some of the Jupyter Lab graphics extensions we use.
	* Installation instructions are [here](https://nodejs.org/en/).

Next, run the following commands in the root directory of this project to complete the setup. First, run the `pip` command to install the rest of the libraries required for these tutorials, including Ray. Then, run the provided script to install a graphing library extension in Jupyter Lab and perform other tasks.

```shell
pip install -r requirements.txt
tools/fix-jupyter.sh
```

If you are using Windows, see the _Fixing Jupyter Lab on Windows_ section below for an alternative to using `tools/fix-jupyter.sh`.

### Fixing Jupyter Lab on Windows

The `tools/fix-jupyter.sh` shell script runs the following commands. If you are using Windows, run them yourself as shown here.

First, see if the following `pyviz` extension is installed:

```
jupyter labextension check --installed "@pyviz/jupyterlab_pyviz"
```

If not, run this command:

```
jupyter labextension install "@pyviz/jupyterlab_pyviz"
```

Finally, run these commands:

```
jupyter labextension update --all
jupyter lab build
jupyter labextension list
```

## Final Notes for Local Installation

The tutorials will start a local Ray "cluster" (one node) on your machine. When you are finished with the tutorials, run the following command to shut down Ray:

```shell
ray stop
```

Also, when you have finished working through the tutorials, run the script `tools/cleanup.sh`, which prints temporary files, checkpoints, etc. that were created during the lessons. You might want to remove these as they can add up to 100s of MBs.

If you decide to delete all the files and directories listed, the following `bash` command will do it:

```shell
tools/cleanup.sh | while read x; do rm -rf $x; done
```

> **Note:** A Windows version of this script is TBD.

## Launching the Tutorials

The previous steps installed [Jupyter Lab](https://jupyterlab.readthedocs.io/en/stable/), the notebook-based environment we'll use for all the lessons. To start run the following command in the project root directory:

```shell
jupyter lab
```

It should automatically open a browser window with the lab environment, but if not, the console output will show the URL you should use.

> **Tip:** If you get an error that `jupyter` can't be found and you are using the Anaconda setup, make sure you activated the `anyscale-academy` environment, as shown above.

## Which Tutorials Are Right for Me?

Here is a recommended reading list, based on your interests:

| You Are... | Best Tutorials |
| :--------- | :------------- |
| A developer who is new to Ray | First, [_Ray Crash Course_](ray-crash-course/00-Overview-Ray-Crash-Course.ipynb), then [_Advanced Ray_](advanced-ray/00-Overview-Advanced-Ray.ipynb) |
| A developer who is experienced with Ray | [_Advanced Ray_](advanced-ray/00-Overview-Advanced-Ray.ipynb) (_alpha_ release) |
| A developer or data scientist interested in Reinforcement Learning | [_Ray RLlib_](rllib/00-Overview-Ray-RLlib.ipynb) |
| A developer or data scientist interested in Hyperparameter Tuning  | _Ray Tune_ |
| A developer or data scientist interested in accelerated model training with PyTorch  |See the _Ray SGD_ lesson in the _Ray Tune_ tutorial |
| A developer or data scientist interested in model serving | _Ray Serve_ |
| A _DevOps_ engineer interested in managing Ray clusters | _Ray Cluster Launcher_ (forthcoming) |

### Tutorial Descriptions

See the [Overview notebook](Overview.ipynb) for detailed, up-to-date descriptions for each tutorial and the lessons it contains.

## Troubleshooting

See the [Troubleshooting, Tips, and Tricks](reference/Troubleshooting-Tips-Tricks.ipynb) notebook.

For details on the Ray API and the ML libraries, see the [Ray Docs](https://docs.ray.io/en/latest/).

