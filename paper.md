---
title: 'osfr: An R Interface to the Open Science Framework'
tags:
  - R
  - open science
  - reproducible research
authors:
  - name: Aaron R. Wolen
    orcid: 0000-0003-2542-2202
    affiliation: 1
  - name: Chris H.J. Hartgerink
  - name: Brian G. Richards
    affiliation: 2
  - name: Courtney Soderberg
    affiliation: 3
  - name: Timothy P. York
    affiliation: 4
affiliations:
  - name: James D. Eason Transplant Research Institute, Department of Surgery, University of Tennessee Health Science Center
    index: 1
  - name: Merkle Group Inc.
    index: 2
  - name: Center for Open Science
    index: 3
  - name: Data Science Lab, Department of Human and Molecular Genetics, Virginia Commonwealth University
date: 27 November 2019
bibliography: paper.bib
---

# Summary

`osfr` provides an idiomatic R interface to OSF (Open Science Framework, https://www.osf.io), a free and open source web application that is part open-access repository and part collaborative project management tool. 

# Background

Reproducible research starts with effective workflows that ensure the integrity of raw data and provenance of results through the transparent application of data processing methods.

While technical researchers have long had a myriad of services available that serve these functions (see karthik's git paper), there has been a gap in services for less technically inclined researchers. In many ways, OSF serves to fill this gap. Providing many of the features that make services like github such an excellent platform for managing and distributing research but with a point-and-click web interface that is comparatively much simpler. 

OSF offers a suite of tools for managing project workflows that facilitate 

The first step towards using OSF is to create new project page. Every OSF project can have a title, description

On OSF, individual repositories are referred to as *projects*, which serve as the fundamental unit of content organization. Every OSF project receives
a website with a globally unique URL on the `osf.io` domain, which serves as the primary interface for accessing projects and utilizing their various features. Files are added by dragging them to the project's file browser, where they are uploaded to the free cloud storage provided by OSF. 

# Design

osf provides a suite of functions for performing these project management tasks from within R. 

Exported `osfr` functions are named using the following convention: `osf_<verb>`.  The `osf_` prefix is intended to facilitate auto-completion in supported IDEs and avoid namespace clashes with other packages that perform similar file management tasks. The `<verb>` indications the action to be performed (e.g., `osf_upload()`, `osf_open()`). We adopted the names of common Unix utilities where functional analogs exist (e.g., `osf_mv()`, `osf_mkdir()`). In cases where the target of an action is ambiguous, function names are augmented with the intended target. For example, when passed an OSF project, `osf_ls()` could provide a list of the project's files or a list of the project's sub-components. Therefore, we use `osf_ls_files()` and `osf_ls_nodes()` to avoid such confusion.

All OSF entities are represented in `osfr` as `osf_tbl` objects, which are specialized data frames based on the [tibble][tibble::tibble-package] class and inspired by googledrive's `dribble` class. This approach to representing rather complex data structures provides an interface that feels more natural to R users.


repository designed to support researchers of all technical backgrounds. The service includes unlimited cloud storage and file version history, providing a centralized location for your research materials that can be kept private, shared with select collaborators, or made publicly available with citable DOIs. The osfr package provides a suite of functions for interacting with OSF, including the ability to manage projects, clone them locally, upload or download individual files, and more. The combination of OSF and osfr provides many of the advantages of git-based project workflows without leaving behind less technically inclined collaborators.


# Acknowledgements


# References
