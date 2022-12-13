---
layout: docs
title: Metadata
published: 2022-05-09
Author: Dominik Brilhaus <https://orcid.org/0000-0001-9021-3197>
add toc: true
add sidebar: _sidebars\mainSidebar.md
Article Status: Publishable
To-Dos: 
    - Update links to other KB articles
---

<!-- 
# export all .md files in current dir to .docx via pandoc 
for f in *.md; do pandoc -s -o "${f%.md}.docx" "$f"; done
-->

<!-- # Metadata -->
<!-- TOC -->

<!-- [What is metadata?](#what-is-metadata)   -->
<!-- [Where does metadata come from?](#where-does-metadata-come-from)   -->
<!-- [Why do I benefit from metadata?](#why-do-i-benefit-from-metadata)   -->
<!-- [What tasks are important for rich metadata?](#what-tasks-are-important-for-rich-metadata)   -->
<!-- [How does DataPLANT support me in metadata annotation?](#how-does-dataplant-support-me-in-metadata-annotation)   -->

<!-- /TOC -->

This file is used to test sidebar in-page navigation. All links are possibly not working.

## What is metadata?

Metadata is "data that provides information about other data"[^1][Merriam]. In order to put some (plant) life into this web dictionary explanation, let us explore metadata with a plant biology example:

> Viola investigates the effect of the plant circadian clock on sugar metabolism in *W. mirabilis*. For her PhD project, which is part of an EU-funded consortium in Prof. Beetroot's lab, she acquires seeds from a South-African botanical society. Viola grows the plants under different light regimes, harvests leaves from a two-day time series experiment, extracts polar metabolites as well as RNA and submits the samples to nearby core facilities for metabolomics and transcriptomics measurements, respectively. After a few weeks of iterative consultation with the facilities' heads as well as technicians and computational biologists involved, Viola receives back a wealth of raw and processed data. From the data she produces figures and wraps everything up to publish the results in the *Journal of Wonderful Plant Sciences*.

Although overly-simplified, every sentence in this example is packed with metadata. All data that describe the acquisition, transformation, analysis or handling of data "from greenhouse-to-publication" as well as before (where did the plants originate from?) and beyond (what else was deduced from the same dataset?) is considered metadata.
This simple example already illustrates many different types and granular levels as well as common sources and stakeholders in charge for different tasks acting on metadata.

## Where does metadata come from?

Metadata arises along common research tasks, including

- project design (e.g., researcher, institute and project, biological context and research question, purpose of data collection),
- experimental processes (e.g., origin and nature of the biological material, lab protocols), and
- data-analytical processes (e.g., software, versions and dependencies employed).

However, every project typically also produces

- technical (e.g., expected data volume, storage location and file formats),
- bibliographic (e.g., author, publication date and title), and
- legal or administrative (e.g., data origin and ownership, licensing, ethical aspects) metadata.

The different types of metadata are collected from various analog and digital sources, including project grants, electronic lab notebooks, machines used for data acquisition, software used for data analysis. And they are provided by different contributors (stakeholders) including wet-lab biologists, core facilities, computational biologists, librarians or infrastructure providers.

## Why do I benefit from metadata?

Before going any deeper into the what and how, let us understand why we benefit from annotating our data with rich metadata. For this it helps to recap along the [FAIR principles][KB-FAIR] how metadata makes your data comprehensible and utilizable for yourself and your peers.

- **Findable**:  As metadata names the content of the data (e.g., what was examined, for what purpose, with what method), it is the basis for search engines and ideally makes it categorizable for people and machines and thus easier to search for and find.
- **Accessible**: Metadata provides information about the origin (e.g., persons, institutions) and the location of storage (e.g., repository) as well as access rights.
- **Interoperable**: Metadata identifies the software and file formats used for collection and processing, as well as any required conversions between file formats (e.g., from proprietary to open file formats).
- **Reusable**: If the three upper points (F, A, I) are met, research data can be found and obtained and reused according to clear rules described in licenses.

## What tasks are important for rich metadata?

The diversity of metadata types, sources and stakeholders highlights that collecting metadata is rarely a linear one-person or one-time event, but occurs continuously and requires constant updates paralleling a project's development. Here we address a few tasks typically acting on metadata.

### Collection

Metadata stakeholders from different environments have different understandings of what metadata is required for comprehension of the annotated data. As plant biologists we probably agree that, when retrieving data from a public repository or publication, it is beneficial to know what type of measurement was performed on what species of plants. By contrast, a computational biologist and a librarian might emphasize the importance of the programming environment required to interpret a script or the contributing authors and licenses, respectively.  
The more metadata the merrier - wouldn't it be great to capture *all* metadata about a project? Realistically we can only collect a portion of metadata. To guide users on what metadata is encouraged to collect, different domains of data experts have formulated these requirements into what is often referred to as "metadata standards" or "minimum information standards".
Examples for bibliographic and administrative metadata standards include [DublinCore][DublinCore] and [DataCite][DataCite]. Prominent standards to annotate data relevant to different plant science domains are grouped under the "Minimum Information for Biological and Biomedical Investigations" ([MIBBI][MIBBI]) and define e.g. minimum information about a high-throughput SEQuencing Experiment ([MINSEQE][MINSEQE]), Proteomics Experiment ([MIAPE][MIAPE]) or a Plant Phenotyping Experiment ([MIAPPE][MIAPPE]). There are many more metadata standards available which can be explored at [fairsharing.org].  
The metadata standards can be regarded as "checklists", which, when followed, provide that the data is annotated with the required metadata attributes to make it comprehensible at least in the current context.

### Structuring

Comprehensibility also strongly depends on the use of language. And not just the spoken language -English, German, Swahili, etc.- itself, but also different meanings of chosen words. While for a librarian the "title" usually refers to a publication item (e.g. manuscript or book) with "contributors" being "authors", "title" in bio-laboratory routines may refer to the name of a funded project with multiple publications (and titles. In said project "contributors" could include authors, but also other experimenters or data analysts and more. Likewise, the processes coming to a plant biologist's mind thinking about "protocols" (growing plants, collecting material, extracting RNA) will be of little help to a computer scientist trying to retrieve data (via HTTP or FTP) from a database.
Furthermore, the librarian, the computer scientist and the plant biologist would probably have a very different approach to collect and represent the required metadata according to the intuition or conventions of their respective domain.
Two technical solutions, schema and ontologies, help to overcome these ambiguities. Briefly, schema are structured documents that formulate a clear representation of the (metadata) information, thereby making it both human-readable and machine-processable. Ontologies are controlled vocabularies or thesauri with defined relations between the vocables that can be used to fill the schema. In this way, schema define where to find the information and ontologies interpret the information.
The use of schema combined with ontologies is well-established for bibliographic and administrative metadata, where high-level and oftentimes generic metadata relevant to most scientific domains is described. In fact, the two examples of [DublinCore][DublinCore] and [DataCite][DataCite] are not just checklists, but well-defined metadata schema. In more specialized scientific domains the use of schema is much less established.
However, the metadata schema ISA (for investigation &ndash; study &ndash; assay) can be employed for the most versatile data types relevant in plant sciences. ISA allows intuitive, flexible and yet structured and conclusive data annotation with biological as well as bibliographic and administrative metadata. For more details, see [ISA][KB-ISA].

### Sharing and curation

In order to make your data FAIR, it needs to be packaged with metadata and shared in a findable and accessible repository.
There are cases where metadata needs to be made accessible independently of the annotated data, e.g. for legal reasons such as dual-use, intellectual property rights or simply since the data is not yet published. In any case, there are at least as many routines for sharing or publishing metadata as there are for data. For more information please see [DataSharing][KB-DataSharing] and [Repositories][KB-Repositories].
During project lifetime data and metadata continuously develops and requires adaptations and updates. Proper versioning helps to keep an overview of the different stakeholders and tasks acting on metadata. Easy and traceable documentation of these processes can be achieved with general-purpose version control through [git][git].
As data and metadata develops the need to harmonize between metadata outputs may occur. If metadata is properly collected in a schema, converters can help to migrate between different metadata schema or securely export information from one schema to the other.

<div style="page-break-after: always;"></div>

## How does DataPLANT support me in metadata annotation?

The following table gives an overview about DataPLANT tools and services related to metadata. Follow the link in the first column for details.

Name | Type | Tasks on metadata 
----------------|-----------|------------------ 
**[ARC][ARC]**  <br> (Annotated Research Context) | Standard | **Structure:** <ul><li>Package data with metadata</li></ul>
**[Swate][Swate]** <br> (Swate Workflow Annotation Tool for Excel) | Tool | **Collect and structure:** <ul><li>Annotate experimental and computational workflows with ISA metadata schema</li><li>Easy use of ontologies and controlled vocabularies</li><li>Metadata templates for versatile data types</li></ul>
**[ArcCommander]** | Tool | **Collect, structure and share:** <ul><li>Add bibliographical metadata to your ARC</li><li>ARC version control and sharing via DataPLANT's DataHUB</li><li>Automated metadata referencing and version control as your ARC grows</li></ul>
**[DataHUB][DataHUB]** | Service | **Share:** <ul><li>Federated system to share ARCs</li><li>Manage who can view or access your ARC</li></ul>
~~Converter~~ | Tool under construction | **Curate:** <ul><li>Harmonize and migrate between metadata schema</li><li>Manage who can view or access your ARC</li></ul>
**Metadata registry** | Service | **Share:** <ul><li>Find ARC (meta)data</li></ul>

### DataPLANT Support

Besides these technical solutions, DataPLANT supports you with community-engaged data stewardship. For further assistance, feel free to reach out via our [helpdesk](https://support.nfdi4plants.org) or by contacting us <a href="mailto:dataplant@uni-kl.de?subject=DataPLANT%20Metadata">directly</a>.

<div style="page-break-after: always;"></div>

<!-- Knowledgebase Cross-references -->
1. [KB-FAIR]: Link to knowledgebase article "FAIR principles"
2. [KB-ISA]: Link to knowledgeable article "ISA Model"
3. [KB-Repositories]: link to article repositories
4. [KB-DataSharing]: link to article Data Sharing

<!--  -->

[DataHUB]: <https://git.nfdi4plants.org> "ARC DataHUB"
[ARC]: <https://github.com/nfdi4plants/ARC> "ARC specifications"
[ArcCommander]: <https://github.com/nfdi4plants/arcCommander/wiki> "ArcCommander Wiki"
[Swate]: <https://github.com/nfdi4plants/Swate/wiki> "Swate Wiki"

<!-- Reference links -->
[Merriam]: https://www.merriam-webster.com/dictionary/metadata "Merriam Webster definition of metadata"
[DublinCore]: <https://www.dublincore.org/specifications/dublin-core/dcmi-terms/>
[DataCite]: <https://schema.datacite.org>
[MIBBI]: https://fairsharing.org/3518 "MIBBI"
[fairsharing.org]: https://fairsharing.org/search?fairsharingRegistry=Standard "Standards at fairsharing.org"
[MIAPPE]: https://www.miappe.org "MIAPPE"
[MINSEQE]: https://www.fged.org/projects/minseqe "MINSEQE"
[MIAPE]: http://www.psidev.info/miape "MIAPE"
[MIAME]: https://www.fged.org/projects/miame/ "MIAME"
<!-- [EMBL-EBI]: https://www.ebi.ac.uk/services/all "EMBL-EBI repositories"
[NCBI]: https://www.ncbi.nlm.nih.gov/guide/sitemap/ "NCBI repositories" -->
[W3semanticWeb]: <https://www.w3.org/standards/semanticweb/>
[W3schema]: <https://www.w3.org/standards/xml/schema>
[W3ontologies]: <https://www.w3.org/standards/semanticweb/ontology>

<!-- ### types / levels 

The following is neither an exhaustive nor clear-cut list. There will be ambiguities, but it serves the purpose to get a feeling for  -->

<!-- 
- harmonization and migration
- Swate templates, mapping, conversion 
- -->

<!-- <li>Integrates Git, ISA and CWL</li> -->


<!-- 
    [Public data repositories][repositories] frequently co-develop, build on and require adherence to these standards, schemas and formats for both metadata and data to be submitted. Metadata standards continuously evolve, are frequently updated or replaced by the respective initiatives. -->

<!-- 
metadata can be  
- project-related
    - Who acquired the data? In what institute and project? 
    - What was the biological context and research question?
    - What was the purpose of data collection?
- experimental
    - What was the origin and nature of the biological material? 
    - What lab protocol was used?
- data-analytical
    - What software and version was used? 
    - What are possible dependencies? 
- technical
- expected data volume, storage location, file formats and checksums
- purpose: long-term integrity

- bibliographic
- purpose: crediting    
- author or contributor, dates of (data) acquisition or publication 
- legal 
    - Data origin    
    - Ownership
    - Licensing
    - Third-party use
    - funding 
    - ethical (Nagoya, DSI, CARE)  -->

<!-- From a "plant-biologist's perspective"  -->



  <!-- 
  - [MIAME][MIAME]: Minimum Information About a Microarray Experiment,
  - [MIAPE][MIAPE]: Minimum Information About a Proteomics Experiment,
  - [MINSEQE][MINSEQE]: Minimum Information about a high-throughput SEQuencing Experiment,
  - [MIAPPE][MIAPPE]: Minimum Information About a Plant Phenotyping Experiment. 
  - -->


<!-- 
- schema: representation (format) + ontology
  - interoperability  
  - : RDF/XML,

- ISA (see article on [ISA Model][KB-ISA])
 -->


<!-- 

- 
    |   |   |
    |---|---|
    [DublinCore][DublinCore] | title, creator, subject, description, publisher, contributor, date, type, format, identifier, source, language, relation, coverage, rights
    [DataCite][DataCite] | Identifier, Creator, Title, Publisher, PublicationYear , ResourceType, ...

- Prominent standards to annotate data relevant in different plant science domains include

    Acronym | Minimum Information About a ... | Example attributes covered 
    ---------------|----------------------- | ----------------------- 
    [MIAPE][MIAPE] | ...Proteomics Experiment | gel electrophoresis, column chromatography, mass spectrometry, protein and peptide arrays, ...
    [MINSEQE][MINSEQE] | ...high-throughput SEQuencing Experiment | sequence read data, nucleic acid isolation, library preparation strategy, amplification methodologies, alignment algorithms, ...
    [MIAPPE][MIAPPE] | ...Plant Phenotyping Experiment |  

-->


<!-- 
### Other relevant ... 

Name | Type | Task on metadata | More details
---------------|------|------------------|-------------
Git | Tool | Version control | [Git]
ISA <br> (Investigation-Study-Assay) | Standard | Metadata schema to collect bibliographical, project-related, experimental and computational metadata | [KB-ISA]
CWL <br> (Common Workflow Language) | Standard | Automates collection of metadata describing computational workflows | [CWL]
 -->