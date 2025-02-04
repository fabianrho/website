---
title: "Set up Python"
description: "Python is widely use programming language. Learn how to set it up on your computer."
keywords: "install, python, anaconda, conda, distribution, configure, PATH, statistics"
#date: 2020-11-11T22:02:51+05:30
draft: false
weight: 1
aliases:
  - /get/python
  - /install/python
  - /setup/python/
  - /topics/other-category/implement-an-efficient-and-reproducible-workflow/setup/python.md
---

## Installing Anaconda Python

Anaconda is a pre-packaged Python distribution for scientific users. To customize Python with packages and properly use it in combination with [automation tools](/topics/configure-your-computer/automation-and-workflows/make/), we prefer a *locally installed Anaconda distribution* over cloud-based alternatives.

Watch our YouTube video, in which we walk you through the setup on Windows.

{{< youtube hGZSAuDcmQc iframe-video-margins >}}

### Instructions
Direct your browser to [Anaconda download page](https://www.anaconda.com/download/) and download the Python 3.x Graphical Installer for your machine.
Sometimes, the download defaults to Mac, so if you're on Windows or Linux, make sure to select the right version.

## Overview

Anaconda is a pre-packaged [Python](https://www.python.org/) distribution designed for scientific and data-intensive computing, ideal for tasks such as data analysis and machine learning.

We recommend using a *locally installed Anaconda distribution* over cloud-based alternatives, as this allows you to customize Python with [packages](/install/python-packages) and effectively integrate it with [automation tools](/practice/pipeline-automation).

## Installing Python via Anaconda

Watch our YouTube video, where we guide you through the installation and setup process on Windows. 

{{< youtube hGZSAuDcmQc iframe-video-margins >}}

## Set-up instructions

Direct your browser to [Anaconda download page](https://www.anaconda.com/download/). You don't need to provide your email address; simply click "Skip registration" below the green "Submit" button to go directly to the [downloads page](https://www.anaconda.com/download/success). Download the Python 3.x Graphical Installer for your machine. Note that the download may default to Mac, so if you're using Windows or Linux, be sure to select the right version.
Then, follow the steps provided on the website.

{{% warning %}}
During the installation, you will be asked whether you want Anaconda Python to be added to your PATH. **Click yes!**
Even if the installation window gives a warning about adding it to your PATH, please still check that box.
{{% /warning %}}

Note that the installation of Anaconda may take about 5-10 minutes, depending on how fast your computer is.

{{% warning %}}
**For Windows Users**

*   When asked if you want single or multiple user installation, choose **single user**.
*   Accept all defaults that are set in the installation window.
*   Check the box for adding Anaconda to your PATH.
*   In the last step, you are asked if you want Visual Studio, click **Yes**.
{{% /warning %}}
{{% warning %}}
**For Linux Users**

For some users, Python was not added to the path. To quickly do this, please open a terminal window, paste ```echo '$HOME/anaconda3/bin:$PATH' >> ~/.bashrc``` and press `Return`.
{{% /warning %}}

## Verifying that the installation was successful

To verify that the correct version of Python has been installed and was made available in your PATH settings, close your terminal and open a **new** terminal interface and enter:

{{% codeblock %}}
```bash
python --version
```
{{% /codeblock %}}

followed by hitting the `Return` key.

You should see the following information returned:

### Windows users

```bash
Python 3.x.x :: Anaconda, Inc.
```

### Mac & Linux/Ubuntu users

```bash
Python 3.x.x :: Anaconda custom (64-bit)
```

{{% tip %}}
**Python 2 versus Python 3**

Python 2 and 3 are incompatible in syntax.
If you had Python 2 previously installed on your machine,
you might have seen `Python 2.x.x` above. In that case, try typing

```python3 --version```

instead. Now you should see a message like the one above and are good to go.

{{% /tip %}}


{{% summary %}}

With Python set up, you can start using it. Explore these resources to get started: 

- [Install Python Packages](/install/python-packages): Discover what packages are, and how to install them.
- [Get Started With Python](/learn/python) through simple examples of the fundamental basics, such as variables and data types, functions, etcetera.
- [Python Coding Style Guidelines](python/style-guides): Understand the importance of coding style with these essential guidelines.

{{% /summary %}}

