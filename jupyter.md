---
layout: default
title: Jupyter
---

# Jupyter and computing facilities

You've probably heard of [Jupyter](https://jupyter.org) (formerly
IPython notebooks), a web-based system of "notebooks" for interactive
computing.  This page is about providing Jupyter as part of
computational facilities.  Some NordicHPC members have expertise in
Jupyter and it is shared as part of NordicHPC.  This page serves as a
reference.

First off, what role does Jupyter server?  Some may see it as a
service.  We see it as an interface to services, like an ssh server.
Imagine you have a cluster with all your software and data: you can
make JupyterHub an interface to that, instead of a separate service
disconnected from your cluster.  Anywhere you might run an SSH server,
you could run JupyterHub in parallel as a parallel interface.

For information on Jupyter at your sites, please join our mailing list
and start a discussion there, and consider coming to NordicHPC
meetings.



## Resources

At the NeIC2019 conference, some NordicHPC members gave a workshop on
[JupyterHub for research
facilities](https://indico.neic.no/event/18/contributions/168/) -
basically, how to use Jupyter in practice.  Here are some of the key
talks:

* [A brief introduction to Jupyter](https://github.com/wikfeldt/neic2019-jupyter-intro)
* [JupyterHub ≠ x, ∀ x: What is JupyterHub really?](https://docs.google.com/presentation/d/17SBWZ-ettIJkbfsGaQenV70a0lu1nrMAIU2-2uzgv64
* [JupyterHub: tech details for sysadmins](https://docs.google.com/presentation/d/14Q5P1ukvehaZdWW1AE-luPqH-fPmgC9AJ3U6ptNi_GY)
* [EGI notebooks example](https://drive.google.com/file/d/1N30jEZWCNCjn54bgJ0duNnlOS5xMTNwa)
* [Batchspawner example](https://docs.google.com/presentation/d/1m1yXIcoRZ1_dczuPGOXxKCoMDy47ka4A8UW7sraC2PM)

This section will be updated with more reference information later.


## Jupyter hints

* [JupyterHub](https://jupyterhub.readthedocs.io/en/stable/) is perhaps the central piece, which accepts logins (authenticatos), allocates resources and starts Jupyter for individual users.

  * The authenticator checks authenticators (usernames).  If you have
    a pre-existing system, the PAM Authenticator (included by default)
    will be quite useful to you.  There are other options for OAuth,
    etc, to integrate into university systems.

  * The spawner allocates resources and starts the single-user servers.

* The hub doesn't have any part in the environment that users get once
  their servers are started.  You need to install Jupyter
  Notebook/JupyterLab with all relevant extensions, software, etc.
  The spawner is configured to start this.


Let's say that you have a cluster, or something like it.  How would
you make Jupyter available as an interface to this?  Here's the steps
(these are implemented in the Aalto deployment below, check that
config for examples of all steps).  The whole process is not that
difficult if you are able to set up and configure a major computer
system already.

1) Assess your Python environment.  At least Python 3.5 is needed.
It's fine and probably recommended to use a miniconda environment on a
shared filesystem to deploy your Python environment.  This will run
both server and user environments.

2) Install [JupyterHub](https://jupyterhub.readthedocs.io/) in that
miniconda environment, and configure it on the machine that will serve
as the gateway.  The configuration does *not* need to be shared across
the cluster, and for security can be limited on only the
non-user-accessible server node.

3) Assess how you will handle authentication.  If you have a cluster,
most likely you can easily deploy PAM authentication on any node.
Deploy PAM authentication and configure the JupyterHub
[PAMAuthenticator](https://jupyterhub.readthedocs.io/en/stable/getting-started/authenticators-users-basics.html).

4) Install
[JupyterLab](https://jupyterlab.readthedocs.io/)/[notebook](https://jupyter-notebook.readthedocs.io/)
in that miniconda environment.  Configure it with useful extensions
(we'll add more on this later).

5) Configure your spawner.  The spawner will use the batch system
([batchspawner](https://github.com/jupyterhub/batchspawner/)) most
likely, but you could also integrate into other resource management
systems such as Kubernetes.  Each of the single-user servers will run
as the user themselves, with access to all of the cluster's systems
that they have access to.  The single-user servers will activate that
miniconda environment if needed (which has the Jupyter notebook/lab
installed along with all the extensions).

6) Install kernels for users.  Kernels can exist anywhere on the
system, but the kernelspecs (definition files, `jupyter kernelspec
list`) are installed in the miniconda environment.  They are usually
Python but can be other languages too.
[envkernel](https://github.com/NordicHPC/envkernel/) may help here.

*The above instructions will be expanded as needed.*



## Site implementations

* Aalto University's (Finland) cluster Triton has JupyterHub
  ([configuration](https://github.com/AaltoScienceIT/triton-jupyterhub),
  [user
  instructions](https://scicomp.aalto.fi/triton/apps/jupyter.html)).
  This is notable of being a textbook example of a hub integrated into
  a compute cluster as a top-level service using the Slurm queue.

* Aalto University also has a JupyterHub for light computing/teaching
  integrated into general Aalto systems
  ([configuration](https://github.com/AaltoScienceIT/jupyterhub-aalto),
  [user
  instructions](https://scicomp.aalto.fi/aalto/jupyterhub.html)).
  This uses kubernetes and containers to manage everything, and
  directly connects to university storage.

* The [NIRD toolkit](https://www.sigma2.no/content/nird-toolkit)
  (Norway) offers Jupyter/JupyterHub.

* CSC (Finland) has a [notebooks service](https://notebooks.csc.fi/)
  which uses Jupyter, but *not* JupyterHub.

* [jupyterhub-deploy-hpc](https://github.com/jupyterhub/jupyterhub-deploy-hpc)
  contains other examples of HPC sites deploying JupyterHub, with
  different levels of detail.
