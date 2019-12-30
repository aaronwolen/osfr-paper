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

Reproducible research requires effective project management workflows that promote consistency and facilitate transparency. Hallmarks of effective workflows include strategies for tracking the provenance of results, recording intermediate changes, conveniently documenting procedures, and working with collaborators without duplicating effort [@Sandve:2013]. For technically skilled researchers, the combination of version control software (VCS) and cloud-based project repositories (e.g., git and GitHub) enable highly effective workflows [@Ram:2013de] and represent a near gold-standard for computational reproducibility. However, these tools have a steep learning curve, especially for researchers whose training is far removed from software development. Alternatively, the Open Science Framework (OSF) offers much of the same functionality through an intuitive point-and-click web-based interface, significantly lowering the barrier to adopting best practices for researchers of all skill levels, or research groups composed of individuals with different levels of computational expertise [@Sullivan:2019]. Yet, this increase in user accessibility comes at the cost of limiting opportunities for automating certain tasks that are inherent to VCS-based workflows. `osfr` fills this gap for R users by allowing them to programmatically interact with OSF through a suite of functions for managing their projects and files.

# Functional Overview

On OSF, individual repositories are referred to as *projects* and serve as the top-level unit of content organization. New projects can be created with osfr using `osf_create_project()`, which allows you to specify the project's title, provide a description, and indicate whether it should be private (the default) or publicly accessible. Every OSF project includes a cloud-based storage bucket where *files* can be stored and organized into *directories*. You can use `osf_mkdir()` to add directories and `osf_upload()` to populate the project with files. osfr supports recursively uploading nested directories, making it possible to easily mirror the contents of a local project on OSF. For existing projects and project files, osfr provides functions for most common file operations such as copying (`osf_cp()`), moving (`osf_mv()`), deleting (`osf_rm()`), and downloading (`osf_download()`).

A key organizational feature of OSF is the ability to augment a project's structure with sub-projects, which are referred to as *components* on OSF, and can be added with the `osf_create_component()` function. Like top-level *projects*, every *component* is assigned a unique URL upon creation and contains its own cloud-based storage bucket, activity log, wiki, and user permissions, allowing users to create arbitrarily nested projects that can easily scale to meet the needs of even large, multi-institutional collaborations (see the [Cancer Biology Reproducibility Project][cbrp] for a great example). Whatever the scale of your work, adopting a consistent structure across projects creates predictable expectations, facilitates understanding for you and your collaborators [@Wilson:2017], and makes it easier to stay organized as a project inevitably grows in complexity over time. Of course, consistency is hard, especially *ad hoc*, but with osfr the process of creating new projects with specific sets of components and directories can be automated by codifying your preferred organizational structure in a simple script that is run at the outset of every new project.


## Implementation

osfr leverages OSF's REST API (https://developer.osf.io) to represent and manipulate the following types of entities: projects, components, files, directories, and users (i.e., accounts). What follows is a brief description of each entity type and how they relate to one another. The OSF API represents these entities using 1 of 3 different JavaScript Object Notation (JSON) structures: `node` for projects and components, `file` for files and directories, and `user` for user accounts. Because working with such deeply nested data structures is foreign for the typical R user, these entities are represented in `osfr` as `osf_tbl` objects, which are specialized data frames based on the `tibble` class [@tibble] and inspired by [googledrive][]'s `dribble` class [@googledrive]. This `data.frame`-like approach to representing rather complex data structures presents an interface more natural to most R users.

# Design

Exported osfr functions all start with the prefix, `osf_`, following the `<prefix>_<verb>` convention used in packages like googledrive [@googledrive] and [stringr][] [@stringr], which facilitates auto-completion in supported IDEs (like RStudio) and avoids namespace clashes with other packages that perform similar file-based tasks. Where possible, we adopt the names of common Unix utilities that perform analogous functions (e.g., `osf_cp()`, `osf_mkdir()`). In cases where the target of an action is ambiguous, function names are augmented with the intended target. For example, when passed an OSF project, `osf_ls()` could provide a list of the project's files or a list of the project's sub-components. Therefore, we use `osf_ls_files()` and `osf_ls_nodes()` to avoid such confusion. 

# References

<!-- link -->
[cbrp]: https://osf.io/e81xl/ "Reproducibility Project: Cancer Biology"
[googledrive]: https://googledrive.tidyverse.org
[stringr]: https://stringr.tidyverse.org