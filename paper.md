---
title: 'osfr: An R Interface to the Open Science Framework'
tags:
  - R
  - open science
  - reproducible research
  - project management
authors:
  - name: Aaron R. Wolen
    orcid: 0000-0003-2542-2202
    affiliation: 1
  - name: Chris H.J. Hartgerink
    affiliation: 2
  - name: Brian G. Richards
    affiliation: 3
  - name: Courtney Soderberg
    affiliation: 4
  - name: Timothy P. York
    orcid: 0000-0003-4068-4286
    affiliation: 5
affiliations:
  - name: James D. Eason Transplant Research Institute, Department of Surgery, University of Tennessee Health Science Center
    index: 1
  - name: Department of Methodology and Statistics, Tilburg University
    index: 2
  - name: Merkle Group Inc.
    index: 3
  - name: Center for Open Science
    index: 4
  - name: Data Science Lab, Department of Human and Molecular Genetics, Virginia Commonwealth University
    index: 5
date: 27 November 2019
bibliography: paper.bib
---

# Summary

`osfr` provides an idiomatic R interface to OSF (Open Science Framework, https://www.osf.io), a free and open source web application that is part open-access repository and part collaborative project management tool.

# Background

Reproducible research requires effective project management workflows that promote consistency and facilitate transparency. Hallmarks of effective workflows include strategies for tracking the provenance of results, recording intermediate changes, conveniently documenting procedures, and working with collaborators without duplicating effort. 

For technically skilled researchers, the combination of version-control software (VCS) and cloud-based project repositories (e.g., git and GitHub) enable incredibly effective workflows and represent a near gold-standard for computational reproducibility [@Ram:2013de]. However, these tools have a steep learning curve, especially for researchers whose training is far removed from software development. Alternatively, the Open Science Framework (OSF) offers much of the same functionality through an intuitive point-and-click web-based interface, significantly lowering the barrier to adopting best practices
for researchers of all skill levels, or research groups composed of individuals with different levels of computational expertise [@Sullivan:2019]. Yet, this increase in user accessibility comes with the cost of limiting opportunities for automating certain tasks that are inherent to VCS-based workflows. `osfr` fills this gap for R users by allowing them to programmatically interact with OSF through a suite of functions for managing their projects and files.

On OSF, individual repositories are referred to as *projects* with a globally unique URL on the `osf.io` domain, which serve as the fundamental unit of content organization. User files can be uploaded to project storage buckets with access permissions specified for each user. Nested projects serve as *components* of the parent project and provide a highly flexible framework for project organization. The main features of `osfr` is to automate the retrieval of existing project files and to facilitate the creation of new project structures.

# Design

This R package provides a suite of functions for performing project management tasks from within R. Exported `osfr` functions are named using the following convention: `osf_<verb>`.  The `osf_` prefix is intended to facilitate auto-completion in supported IDEs and avoid namespace clashes with other packages that perform similar file management tasks. The `<verb>` indications the action to be performed (e.g., `osf_upload()`, `osf_open()`). We adopted the names of common Unix utilities where functional analogs exist (e.g., `osf_cp()`, `osf_mkdir()`). In cases where the target of an action is ambiguous, function names are augmented with the intended target. For example, when passed an OSF project, `osf_ls()` could provide a list of the project's files or a list of the project's sub-components. Therefore, we use `osf_ls_files()` and `osf_ls_nodes()` to avoid such confusion.  

All OSF entities are represented in `osfr` as `osf_tbl` objects, which are specialized data frames based on the [tibble][tibble::tibble-package] class and inspired by googledrive's `dribble` class. This approach to representing rather complex data structures provides an interface that feels more natural to R users. The setup of a personal access token (PAT) is recommended for use of the `osfr` package and instructions can be access in an introductory vignette.  

# References
