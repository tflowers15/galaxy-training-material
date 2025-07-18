---
layout: tutorial_hands_on
title: Best Practice for Citing Galaxy
tags:
- fair
- introduction
level: Introductory
questions:
- How to cite Galaxy in Publications?
objectives:
- Understand how to cite Galaxy.
- Prepare your methodology section based on your Galaxy Histories.
time_estimation: 10m
key_points:
- Please remember to cite the primary Galaxy Project publication.
- Reference the specific Galaxy server that was used.
- When preparing your methodology we recommend publishing your Galaxy Histories and Workflows.
- Remember to cite any public data used in your analysis.
- You can extract a list of tool citations from your Galaxy History.
subtopic: core
contributors:
- tflowers15
- GarethPrice-Aus
- mirelaminkova
- MarisaJL
funding:
- unimelb
- melbournebioinformatics
- AustralianBioCommons
- SURF

---

# Overview

This is a short primer on how to cite Galaxy in your publication and also how to prepare your Methodology based on your Galaxy history or histories. Following these steps will make it easy to cite Galaxy, share your methods, and adhere to best practices for FAIR and open science.


> <agenda-title></agenda-title>
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

> <comment-title></comment-title>
> The main Galaxy Project publication will be included in the list if you follow the instructions below to extract tool citations from your History.
>
{: .comment}

## Citing a Galaxy Service

### Service Descriptions
Each public Galaxy service benefits from being able to track the amazing work done by researchers using its service. Provided below are the DOIs for the four main `usegalaxy.*` services. The linked papers are available on Zenodo at [https://zenodo.org/communities/galaxy/](https://zenodo.org/communities/galaxy/):

- Galaxy Australia - DOI for [Galaxy Australia (`usegalaxy.org.au`)](https://docs.google.com/document/d/1l5lkRLSJPZ6OesE5G0M6bmyizOIehtniOmS6c3jDNuw/edit?tab=t.0)
- Galaxy Europe - DOI for [Galaxy Europe (`usegalaxy.eu`)](https://docs.google.com/document/d/1obJEODI8K8V7pHOwclbCvYwQ9W1XGH0ahjHgFht49yg/edit?tab=t.0)
- Galaxy France - DOI for [Galaxy France (`usegalaxy.fr`)](https://docs.google.com/document/d/1zQ9LudBYjk02ejTGN7FoVoumrnEFF1V0L4PCwnXzCm0/edit?tab=t.0)
- Galaxy Main - DOI for [Galaxy Main (`usegalaxy.org`)](https://docs.google.com/document/d/10TwJ2p3U1vvj0hsyyqRc9z1LL7ZmEQ1dKfmeCm2zQZk/edit?tab=t.0)

We recommend including the relevant service name and DOI link in your Methods.


### Acknowledging a Service
Each public Galaxy service is provided through a complex mixture of funding, governance and infrastructure providers. As such, each service provides a cut/paste **Acknowledgement** statement that supports their particular configuration and this can be found on each service. If your publication supports Acknowledgements, we strongly recommend you include the service-recommended **Acknowledgements**.

**Acknowledgement** statements for the four main `usegalaxy.*` services can be found using the following links:

- Galaxy Australia - [https://site.usegalaxy.org.au/about#acknowledgement-statement](https://site.usegalaxy.org.au/about#acknowledgement-statement)
- Galaxy Europe - [https://usegalaxy-eu.github.io/about](https://usegalaxy-eu.github.io/about)
- Galaxy France - [https://www.france-bioinformatique.fr/en/services/acknowledgement/](https://www.france-bioinformatique.fr/en/services/acknowledgement/)
- Galaxy Main - [https://usegalaxy.org/#about](https://usegalaxy.org/#about)

# Writing a Methods section based on your Galaxy work

## Making a History public

We provide the following recommendations and process for making your History persistent and your options for public archiving of your History. Sharing your History will make it easier for others to understand or replicate your analysis. You can also add annotations and tags to ensure your history is FAIR.

### Preparing a History

We recommend cleaning up your History when preparing to make your History public.

- `Delete` and `Delete (permanently)` (purge) any failed jobs.
- `Delete` and `Delete (permanently)` (purge) any datasets/job outputs that were used for testing and are not required for the final, published analysis.
- `Delete` and `Delete (permanently)` (purge) any datasets that you don't want to share publicly (e.g. restricted data, unpublished results) - but make sure you save them to a private history first.

{% snippet faqs/galaxy/datasets_deleting.md %}

We also suggest providing a description/context of the History in the `History Annotation`.

{% snippet faqs/galaxy/histories_annotation.md %}

Users can add tags to their Galaxy histories to organise and connect them to specific analyses. Tags improve the findability and traceability of your work, aligning with the FAIR principles. Applying relevant tags before publishing your history is recommended to enhance its clarity and usefulness for both yourself and others.

{% snippet faqs/galaxy/histories_tagging.md %}
### Sharing a History

Galaxy provides a number of options for sharing histories which allows others to import and access the datasets, parameters, and steps of your history.

{% snippet faqs/galaxy/histories_sharing.md %}

### Exporting a History to Zenodo

Integration of InvenioRDM and Zenodo into Galaxy now enables you to export your history directly to Zenodo. Publishing your history on Zenodo will generate a DOI for your history which you can include in your publication and can be used by other researchers to cite your work.

For instructions on connecting to Zenodo and preparing your history, see the following tutorial on the Galaxy Training Network:

- [Integrating InvenioRDM-compatible Repositories with Galaxy](https://training.galaxyproject.org/training-material/topics/fair/tutorials/inveniordm-integration/tutorial.html)

## Making a Workflow public

If you used a workflow in your analysis, we recommend publishing this alongside your data and in your article. In addition to providing a complete description of your method, the published workflow will also make your approach reproducible and citeable.

Two repository options that we recommend for publishing your Workflows are:

- WorkflowHub ([https://workflowhub.eu/](https://workflowhub.eu/))
- Dockstore ([https://dockstore.org/](https://dockstore.org/)) 

For instructions on preparing your workflow, see the following tutorial on the Galaxy Training Network:

- [Annotate, prepare tests and publish Galaxy workflows in workflow registries](https://training.galaxyproject.org/training-material/topics/galaxy-interface/tutorials/workflow-fairification/tutorial.html)

## Citing Public Data

If you used a public data source in your work, we recommend you cite both the data source publication DOI and the dataset itself. Most citation styles will include options for citing datasets. You should include the repository name and accession code in your Methods section to make it easy to find.

## Extract Tool Citations from a Galaxy History

Galaxy can provide a list of the tools used in your history using the following steps. You might find this helpful when writing up your methods, but it is also the quickest way to add all these tools to your references.

{% snippet faqs/galaxy/cite-tools-used-in-a-history.md %}

> <comment-title></comment-title>
> You will also get the Galaxy Project publication in all History citation exports!
>
{: .comment}
 
# Conclusion

In this tutorial, we have covered how to cite Galaxy Project and the specific Galaxy server that you used and how to prepare your methodology based on your Galaxy History.



