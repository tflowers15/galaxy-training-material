---
layout: tutorial_hands_on
title: Best Practice for Citing Galaxy
zenodo_link: https://zenodo.org/uploads/15756328
tags:
- fair
- introduction
questions:
- How to cite Galaxy in Publications?
objectives:
- Understand how to cite Galaxy.
- Advice on how to prepare your methodology section based on your Galaxy Histories.
time_estimation: 10m
key_points:
- Cite the primary Galaxy Project publication.
- Reference the specific Galaxy server that was used.
contributors:
- tflowers15
- GarethPrice-Aus
- mirelaminkova
- MarisaJL
funding:
- unimelb
- melbournebioinformatics
- AustralianBioCommons

---

# Overview

This is a short primer on how to cite Galaxy in your publication and also how to prepare your Methodology based on your Galaxy history(s).


<agenda-title></agenda-title>
> In this tutorial we will deal with:
>
> 1. TOC
> {:toc}
>
{: .agenda}


# Citing Galaxy
Citing Galaxy comes in two main actions: 

1. Citing the global Galaxy Project that provides the core code that all Galaxy instances operate on. 
2. Citing the instance of Galaxy you did your work on.

## Citing Galaxy Project
Please cite Galaxy Project’s primary publication: 

***The Galaxy platform for accessible, reproducible, and collaborative data analyses: 2024 update***

- Nucleic Acids Research, Volume 52, Issue W1, 5 July 2024, Pages W83–W94, [https://doi.org/10.1093/nar/gkae410](https://doi.org/10.1093/nar/gkae410)

This is also found on the Galaxy Project Hub with more specific examples of how to cite individual aspects of Galaxy Project - [https://galaxyproject.org/citing-galaxy/](https://galaxyproject.org/citing-galaxy/)

## Citing a Galaxy Service

### Service Descriptions
Each public Galaxy service benefits from being able to track the amazing work done by researchers using its service. Provided below are the DOIs for the four main `usegalaxy.*` services and the linked papers are available on Zenodo at [https://zenodo.org/communities/galaxy/](https://zenodo.org/communities/galaxy/):

- Galaxy Australia - DOI for [Galaxy Australia (`usegalaxy.org.au`)](https://docs.google.com/document/d/1l5lkRLSJPZ6OesE5G0M6bmyizOIehtniOmS6c3jDNuw/edit?tab=t.0)
- Galaxy Europe - DOI for [Galaxy Europe (`usegalaxy.eu`)](https://docs.google.com/document/d/1obJEODI8K8V7pHOwclbCvYwQ9W1XGH0ahjHgFht49yg/edit?tab=t.0)
- Galaxy France - DOI for [Galaxy France (`usegalaxy.fr`)](https://docs.google.com/document/d/1zQ9LudBYjk02ejTGN7FoVoumrnEFF1V0L4PCwnXzCm0/edit?tab=t.0)
- Galaxy Main - DOI for [Galaxy Main (`usegalaxy.org`)](https://docs.google.com/document/d/10TwJ2p3U1vvj0hsyyqRc9z1LL7ZmEQ1dKfmeCm2zQZk/edit?tab=t.0)

We recommend including the relevant service name and DOI link into your Methods.


### Acknowledging a Service
Each public Galaxy service is provided through a complex mixture of funding, governance and infrastructure providers. As such, each service provides a cut/paste **Acknowledgement** statement that supports their particular configuration and this can be found on each service. If your publication supports Acknowledgements, we strongly recommend your include the service recommended **Acknowledgements**.


# Writing a Methods section based on your Galaxy work

## Making a History public

We provide the following recommendations and process for making your History persistent and your options for public archiving of your History.

### Preparing a History

We recommend cleaning up your History when preparing to make your History public.

- `Delete` and `Delete (permanently)` (purge) any failed jobs.
- `Delete` and `Delete (permanently)` (purge) any datasets/job outputs that were used for testing and are not required for the final, published analysis.

{% snippet faqs/galaxy/datasets_deleting.md %}

We also suggest providing a description/context of the History in the `History Annotation`.

{% snippet faqs/galaxy/histories_annotation.md %}

### Sharing a History

Galaxy provides a number of options for sharing histories which allows others to import and access the datasets, parameters, and steps of your history.

{% snippet faqs/galaxy/histories_sharing.md %}

### Exporting a History to Zenodo

Integration of InvenioRDM and Zenodo into Galaxy now enables you to export your history directly to Zenodo. Publishing your history on Zenodo will generate a DOI for your history which you can include in your publication and can be used by other researchers to cite your work.

{% snippet faqs/galaxy/histories_export_to_zenodo.md %}

## Making a Workflow public

If you used a workflow in your analysis, we recommend publishing this alongside your data and in your article. 

Two respository options that we recommend for publishing your Workflows are:

- WorkflowHub ([https://workflowhub.eu/](https://workflowhub.eu/))
- Dockstore ([https://dockstore.org/](https://dockstore.org/)) 

For instructions on preparing your workflow, see the following tutorial on the Galaxy Training Network:

- [Annotate, prepare tests and publish Galaxy workflows in workflow registries](https://training.galaxyproject.org/training-material/topics/galaxy-interface/tutorials/workflow-fairification/tutorial.html)


## Citing Public Data

If you used a public data source in your work, we recommend you cite both the data source publication DOI and the repository accession code.

## How to Extract Tool Citations from a Galaxy History

Galaxy can provide a list of the tools used in your history using the following steps.

{% snippet faqs/galaxy/cite-tools-used-in-a-history.md %}

**Hint:** You will also get the Galaxy Project publication in all History citation exports!
 




