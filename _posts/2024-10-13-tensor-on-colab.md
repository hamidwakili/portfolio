---
layout: post
title: Setting up TensorFlow 1.15 on Google Colab
description: In this guide, we will walk through the steps to set up TensorFlow 1.15 with Python 3.8 on Google Colab using Miniconda.
image: /images/tensorflow.jpg
---

In this guide, we will walk through the steps to set up TensorFlow 1.15 with Python 3.8 on Google Colab using Miniconda.
TensorFlow 1.x versions are still relevant for some legacy projects, and setting up the environment can be tricky since Colab natively supports newer Python versions and TensorFlow 2.x.

Let's dive into the setup process!

## Step 1: Check the Current Python Environment Path

Before starting the setup, it’s always good to inspect the current environment path. In Google Colab, you can check the `PYTHONPATH` by running:

```python
%env PYTHONPATH
```
This will show you the current paths where Python searches for modules.

## Step 2: Install Miniconda with Python 3.8

Next, we need to install Miniconda with Python 3.8. Google Colab doesn’t natively support Python 3.8 with TensorFlow 1.15, so we use Miniconda to create a custom environment.

Run the following commands in your Colab cell to download and install Miniconda:
```bash
!wget https://repo.anaconda.com/miniconda/Miniconda3-py38_4.12.0-Linux-x86_64.sh
!chmod +x Miniconda3-py38_4.12.0-Linux-x86_64.sh
!./Miniconda3-py38_4.12.0-Linux-x86_64.sh -b -f -p /usr/local
```
* wget fetches the Miniconda installer.
* chmod +x makes the installer executable
* The last command installs Miniconda to /usr/local

After installation, update conda to the latest version:

```bash
!conda update conda
```

## Step 3: Append the New Python Path
```python
import sys
sys.path.append('/usr/local/lib/python3.8/site-packages')
```
This appends the Miniconda site-packages directory to the Python path.

## Step 4: Create a Conda Environment with Python 3.7

TensorFlow 1.15 officially supports Python 3.7, so we’ll create a new environment using conda:
```bash
!conda create -n my-env python=3.7
```
This creates a virtual environment named my-env with Python 3.7.

## Step 5: Activate the Conda Environment
Now, activate the environment using the following shell command:
```bash
%%shell
eval "$(conda shell.bash hook)"
conda activate my-env
```
The eval command initializes the Conda environment, and conda activate switches to the newly created environment.

## Step 6: Set TensorFlow 1.15 Compatibility
Finally, to ensure compatibility with TensorFlow 1.15, we need to set the following environment variable:
```python
import os
os.environ["PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION"] = "python"
```
This prevents issues related to protocol buffers used by TensorFlow.

Once you’ve followed these steps, you will have a Colab environment ready to use TensorFlow 1.15 with Python 3.7. This setup is useful for legacy TensorFlow projects that require older dependencies.

You can now install TensorFlow 1.15 using pip in this environment:
```bash
%%shell
eval "$(conda shell.bash hook)"
pip install tensorflow==1.15
```
