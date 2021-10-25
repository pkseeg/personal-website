---
title: How to use Jupyter Lab and Python Virtual Environments (Ubuntu/Debian)
subtitle: I got so sick of googling around every time that I decided to just post it here

# Summary for listings and search engines
summary: How to use Jupyter Lab and Python Virtual Environments simultaneously in an Ubuntu/Debian system for better python package management, better data science project management, and general project reproducibility.

# Link this post with a project
projects: []

# Date published
date: "2021-10-24T00:00:00Z"

# Date updated
lastmod: "2021-10-24T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: true

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Dr. Farrell**](https://faculty.cs.byu.edu/~farrell/)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags:
- python
- jupyter
- data science

categories:
- python
---

Python's `venv` virtual environment system is meant to help developers manage their python library versions so that when they update 
some package or tool on their system, nothing inside their projects will break unexpectedly. As a PhD student and data scientist 
I strongly believe in this system as a means for releasing reproducable, easy-to-follow projects in my research and other projects.

One of my favorite data science tools is jupyter lab. It's a browser work environment for jupyter notebooks, which are obviously a 
staple of the data science community, and other useful tools like terminals and python code editors. 

Aaaaand I'm sick of having to look for the same 3 stack overflow answers to piece together how to use jupyter lab inside of a 
virtual environment. And I told myself when I started grad school that if I had to look the same thing up 3 times, I'd just write a post 
about it for my budding little personal website.

Anyway here's how to do it.

# **-1. Here's all the commands up front, read on for a walkthrough**

```console
mkdir example-project && cd example-project
python3 -m venv env
source env/bin/activate
python3 -m pip install --user virtualenv
python3 -m pip install ipykernel
python3 -m pip install jupyterlab
python3 -m pip install pandas
jupyter lab
```


# **0. Get venv**

If you're new to virtual environments generally, make sure you a) 
[have python installed](https://linuxhint.com/install-python-debian-10/) and b) use the following command to install `virtualenv`.

```console
parker@pkseeg:~$ python3 -m pip install --user virtualenv
```

# **1. Create a project folder and get into it**

Make sure to rename `example-project` to whatever you want to call your project.

```console
parker@pkseeg:~$ mkdir example-project && cd example-project
```

# **2. Initialize a virtual environment**

This will initialize a `venv` in your project folder called `env` (you can call it whatever you want, but for me consistency 
is helpful.

```console
parker@pkseeg:~/example-project$ python3 -m venv env
```

# **3. Activate your virtual environment**

This is a step you'll have to use every time you work on your project. You can think about it as assigning your python 
environment to the environment specific to your project. Remember that if you named your folder something other than 
`env`, you'll have to replace that here.

```console
parker@pkseeg:~/example-project$ source env/bin/activate
```

# **4. Install `ipykernel`**

This is important for jupyter lab.

```console
(env) parker@pkseeg:~/example-project$ python3 -m pip install ipykernel
```

# **5. Install `jupyterlab`**

This piece always got lost for me, initially `ipykernel` would include `jupyterlab` but I guess it doesn't anymore.

```console
(env) parker@pkseeg:~/example-project$ python3 -m pip install jupyterlab
```

# **6. (OPTIONAL) Install `pandas`, other packages**

This is why `venv` is so powerful - it allows you to keep different versions of packages for different projects. 
`pandas` isn't a package that will break easily when updated, but you get the idea.

```console
(env) parker@pkseeg:~/example-project$ python3 -m pip install pandas
```

# **7. (OPTIONAL) Add packages to `requirements.txt`**

Here you can create a `requirements.txt` file to store all the required library for your project. This is very 
important for readability and reproducability.

```console
(env) parker@pkseeg:~/example-project$ touch requirements.txt
(env) parker@pkseeg:~/example-project$ echo 'pandas' > requirements.txt
```

# **8. Launch `jupyter lab`**

```console
(env) parker@pkseeg:~/example-project$ jupyter lab
```

And voila! Should be working. You have a reproducible, readable, safe python project which you can work on in jupyter lab.

Happy development!
