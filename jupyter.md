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

First off, what is Jupyter for?  Some may see it as a service.  We see
it as an interface to services, more like an ssh server.  Imagine you
have a cluster with all your software and data: you can make JupyterHub
an interface to that, instead of a separate service.

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