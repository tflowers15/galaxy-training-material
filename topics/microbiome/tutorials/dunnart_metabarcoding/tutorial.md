---
layout: tutorial_hands_on

title: "Hi-C analysis of Drosophila melanogaster cells using HiCExplorer"
zenodo_link: "https://doi.org/10.5281/zenodo.16416373"
questions:
  - Why is the fat‑tailed dunnart a useful model for microbiome studies?
  - What are the expected experimental differences between captive and wild animals?
  - Why use a byobu / screen session on a remote instance?
  - What are symbolic links and why are they used here?
objectives:
  - Place the dataset in ecological and conservation context.
  - Relate host ecology and sample provenance to interpretation of microbiome results.
  - Launch and reconnect to a persistent byobu‑screen session.
  - Create symbolic links to shared tutorial data to avoid redundant copies.
time_estimation: "2h"
key_points:
  - Captivity can alter diet, exposure and behaviour — all of which may reshape the gut microbiome.
  - The dataset contains a small, balanced subset (5 captive, 5 wild) suitable for teaching and demonstrating methods.
  - 
contributions:
  authorship:
    - tflowers15
    - gayle
    - ashley
  funding:
    - unimelb
    - melbournebioinformatics
    - AustralianBioCommons

---

# Background

What is the influence of captivity on gut microbiota of the fat-tailed dunnart?

## The Players

![dunnart](./images/dunnart.jpg)
(Photo credit: Emily Scicluna)


Fat-tailed dunnart [*Sminthopsis crassicaudata*](https://en.wikipedia.org/wiki/Fat-tailed_dunnart) - a species of mouse-like marsupial in the family Dasyuridae, which includes quolls, the Tasmanian devil, and the extinct Thylacine. There are 10 samples in this dataset (*This data is a subset from a larger experiment*); 5 faecal samples each from captive and wild fat-tailed dunnarts.  
   

## The Study
Indigenous microbial communities (microbiota) play critical roles in host health. Small marsupials, such as the fat-tailed dunnart, are increasingly used as model systems to understand how environmental conditions shape host-associated microbiomes. Transitions between wild and captive environments can substantially alter diet, behaviour, and microbial exposure, providing a natural framework to investigate microbiome restructuring and its potential consequences for host physiology and health. Here, we characterise the gut microbiome of wild and captive fat-tailed dunnarts to assess how captivity influences microbial community composition. This dataset represents a subset of a larger experimental framework examining microbiome-mediated effects on host function and conservation outcomes.

## QIIME 2 Analysis platform

> <caution></caution>
> 
> The version used in this workshop is `qiime2-2026.1`. Other versions of QIIME2 may result in minor differences in results.
>
{: .caution}


Quantitative Insights Into Microbial Ecology 2 ([QIIME 2](https://www.nature.com/articles/s41587-019-0209-9)) is a next-generation microbiome [bioinformatics platform](https://qiime2.org/) that is extensible, free, open source, and community developed. It allows researchers to:

  - Automatically track analyses with decentralised data provenance
  - Interactively explore data with beautiful visualisations
  - Easily share results without QIIME 2 installed
  - Plugin-based system — researchers can add in tools as they wish


#### Viewing QIIME2 visualisations


> <callout></callout>
> 
> In order to use QIIME2 View to visualise your files, you will need to use a Google Chrome or Mozilla Firefox web browser (not in private browsing). For more information, click [here](https://view.qiime2.org).
>
{: .callout}

As this tutorial uses Galaxy Australia, you will need to download the visual files (*.qzv) to your local computer and view them in [QIIME2 View](https://view.qiime2.org) (q2view).

> <callout></callout>
> 
> We will be doing this step multiple times throughout this workshop to view visualisation files as they are generated.
>
{: .callout}

> <comment></comment>
> 
> Within Galaxy, the `QIIME vizualisation extractor` tool can be used to view QIIME2 `.qzv` visualisation files. However, some QIIME2 visualisation files will not properly display or will lose some of the visualisation's interactive features.
> 
{: .comment}

This Galaxy tutorial based on material from the [Metabarcoding of bacteria in dunnart faecal samples across Australia (wild + captive)](https://mbite.mdhs.unimelb.edu.au/qiime2_dunnart/aio.html) tutorial and workshop created by [Melbourne Bioinformatics](https://mdhs.unimelb.edu.au/melbournebioinformatics) at the University of Melbourne.

> <agenda-title></agenda-title>
>
> In this tutorial, we will deal with:
>
> 1. TOC
> {:toc}
>
{: .agenda}

# Data upload

These [samples](./index.html#data) were sequenced on a single Illumina NextSeq run at the Walter and Eliza Hall Institute (WEHI), Melbourne, Australia. Data from WEHI came as paired-end, demultiplexed, unzipped *.fastq files with adapters still attached. Following the [QIIME2 importing tutorial](https://amplicon-docs.qiime2.org/en/stable/how-to-guides/how-to-import.html), this is the Casava One Eight format. The files have been renamed to satisfy the Casava format as SampleID_FWDXX-REVXX_L001_R[1 or 2]_001.fastq e.g. CTRLA_Fwd04-Rev25_L001_R1_001.fastq.gz. The files were then zipped (.gzip).

Here, the data files (two per sample i.e. forward and reverse reads `R1` and `R2` respectively) will be imported and exported as a single QIIME 2 artefact file. These samples are already demultiplexed (i.e. sequences from each sample have been written to separate files), so a metadata file is not initially required.


> <hands-on-title>Data upload</hands-on-title>
>
> 1. Create a new history
>
>    {% snippet faqs/galaxy/histories_create_new.md %}
>
> 2. Import from [Zenodo](https://doi.org/10.5281/zenodo.16416373).
>
>    > <tip-title>Importing data via links</tip-title>
>    >
>    > 1. Copy the link location
>    > 2. Open the Galaxy Upload Manager
>    > 3. Select **Paste/Fetch Data**
>    >
>    >    Below are the links to the read files that can be copied and pasted in the upload manager.
>    >
>    >    ```
>    >    https://zenodo.org/records/16416373/files/HiC_S2_1p_10min_lowU_R1.fastq.gz
>    >    https://zenodo.org/records/16416373/files/HiC_S2_1p_10min_lowU_R2.fastq.gz
>    >    ```
>    >
>    > 4. Paste the links into the text field
>    > 5. Press **Start**
>    {: .tip}
>
> 3. Create a list collection of the imported raw reads (`.fastq.gz`) datasets.
>
{: .hands_on}


# Importing, cleaning and quality control of the data

Run the command to import the raw data located in the directory `raw_data` and export it to a single QIIME 2 artefact file, `combined.qza`.


> <hands-on-title>Create QIIME2 Artefact</hands-on-title>
>
> 1. {% tool [`qiime2 tools import`](toolshed.g2.bx.psu.edu/repos/q2d2/qiime2_core__tools__import/qiime2_core__tools__import/2026.1.0+dist.h02a552c2) %}: 
>    - *"Type of data to import"*: `SampleData[PairedEndSequencesWithQuality]`
>    - *QIIME 2 file format to import from:*: `Casava One Eight Single Lane Per Sample Directory Format`
>    - *"Import sequences"*: 
>      - *"Select a mechanism"*: `Use collection to import`
>      - *"elements"*: `raw reads`
>    - *"Append an extension?"*: `No, use element identifiers as is` (*If the datasets in the collection include the extension `.fastq.gz`*)
>    - *"Append an extension?"*: `Yes` (*If the datasets in the collection DO NOT include the extension `.fastq.gz`*)
>      - *"Extension to append (e.g. '.fastq.gz')"*: `.fastq.gz`
>
> 2. Rename the output to: `combined.qza`
>
{: .hands_on}


## Remove primers

> <callout></callout>
> 
> Remember to ask your sequencing facility if the raw data you get has the primers attached - they may have already been removed.
>
{: .callout}


These sequences still have the primers attached and must be removed prior to denoising. For this workshop, primer trimming was performed using the QIIME 2 `cutadapt trim-paired` plugin to maintain a fully reproducible workflow within the QIIME 2 framework. Amplicons were generated using standard 16S rRNA gene primers for the v4 region, and the reads returned from the sequencer therefore include these primer sequences at the 5′ ends. Using cutadapt, the specified primer sequence and any bases upstream of the match are removed, with an error rate of 0.10 to balance sensitivity of primer detection with specificity of trimming. Degenerate bases in the primers are accommodated using wildcard matching, and any reads lacking the expected primer sequences are discarded to minimise inclusion of off-target amplification products. A modest 3′ quality trimming threshold (Phred score = 20) is also applied to remove low-quality bases prior to downstream denoising.

It is important to note that these data were generated on an Illumina NextSeq platform, which uses 2-colour chemistry and can produce artificial poly-G tails at the ends of reads under low-signal conditions. The QIIME 2 implementation of cutadapt does not have the `--nextseq-trim` parameter, which is specifically designed to remove these artefacts. As such, the trimming approach used here represents a simplified, self-contained workflow appropriate for teaching purposes. For production analyses of NextSeq data, best practice is to perform trimming with standalone cutadapt (including --nextseq-trim) prior to importing reads into QIIME 2, as this improves removal of sequencing artefacts and can enhance downstream denoising and taxonomic resolution.


> <hands-on-title>Run Cutadapt</hands-on-title>
>
> 1. {% tool [`qiime2 cutadapt trim-paired`](toolshed.g2.bx.psu.edu/repos/q2d2/qiime2__cutadapt__trim_paired/qiime2__cutadapt__trim_paired/2026.1.0+q2galaxy.2026.1.0) %}: 
>    - *"demultiplexed_sequences: SampleData[PairedEndSequencesWithQuality]"*: `combined.qza`
>    - *"Click here for additional options"*
>    - *"front_f: List[Str]"*: `+ Insert front_f: List[Str]"`
>        - *"1: front_f: List[Str]"*: `GTGYCAGCMGCCGCGGTAA`
>    - *"front_r: List[Str]"*: `+ Insert front_r: List[Str]"`
>        - *"1: front_r: List[Str]"*: `GGACTACNVGGGTWTCTAAT`
>    - *"error_rate: Float % Range(0, 1, inclusive_end=True)"*: `0.1`
>    - *"overlap: Int % Range(1, None)"*: `10`
>    - *"match_adapter_wildcards: Bool"*: `Yes`
>    - *"discard_untrimmed: Bool"*: `Yes`
>    - *"quality\_cutoff\_5end: Int % Range(0, None)"*: `0`
>    - *"quality\_cutoff\_3end: Int % Range(0, None)"*: `30`
>
> 2. Rename the output to: `trimmed_sequences.qza`
>
{: .hands_on}

> <caution></caution>
> 
> The primers specified are the Earth Microbiome Project (EMP) 16S V4 primers (515F (Parada)– 806R (Apprill) targeting the v4 region of the bacterial 16S rRNA gene), which correspond to *this* specific experiment. Unless you are using these exact primers for your experiment, you need to adapt the code accordingly.
>
{: .caution}


> <discussion></discussion>
> 
> The error rate, `error_rate`, and overlap, `overlap`, parameters will likely need to be adjusted for your own sample data to maximise the proportion of reads successfully trimmed while avoiding nonspecific matches. Play around with these values and see what happens.
>
{: .discussion}


## Create and interpret sequence quality data

Create a viewable summary file so the data quality can be checked. Viewing the quality plots generated here helps determine settings for dada2, which we will run next.

Trimmed sequences are processed using the `dada2` [plugin](https://pubmed.ncbi.nlm.nih.gov/27214047/) within QIIME2. dada2 denoises data by modelling and correcting Illumina amplicon sequencing errors, and infers exact amplicon sequence variants (ASVs), resolving differences of as little as a single nucleotide. Its workflow includes filtering, dereplication, paired-end read merging, and reference-free chimera detection, resulting in a feature (ASV) table.

Truncation removes bases from the 3′ end of reads at the specified position. When choosing DADA2 truncation lengths, the first step is to inspect the forward and reverse quality plots you just created. In many modern Illumina datasets, especially after primer and basic quality trimming, these plots may appear relatively flat with consistently high quality across most of the read length. In these cases, there is no obvious “cut point” where quality sharply declines. Instead of looking for a specific quality threshold (for example, Q35), you should choose truncation lengths conservatively, trimming only the very ends of reads if needed while retaining as much high-quality sequence as possible without compromising read overlap.

For paired-end data, an additional and critical consideration is read overlap. After truncation, the forward and reverse reads must still overlap sufficiently to merge. While the absolute minimum overlap is ~12 bp, an overlap of ~50 bp is recommended to ensure robust merging and reduce the risk of losing reads during this step. As a result, truncation lengths are often chosen by balancing two factors: maintaining high-quality sequence and preserving enough overlap for successful merging.

TL;DR: when quality plots are essentially straight lines, truncation is less about identifying where quality drops and more about keeping as much usable sequence as possible while ensuring adequate overlap between reads.

> <discussion></discussion>
> 
> #### Things to look for when choosing truncation lengths
> 
> 1. Do the forward and reverse quality profiles show a clear decline near the ends of the reads? If so, truncate before the low-quality tail.
> 2. If the quality profiles remain high and relatively flat, avoid trimming too aggressively and retain as much high-quality sequence as possible.
> 3. Will the chosen forward and reverse truncation lengths still leave enough overlap for paired-end merging? A minimum overlap of ~50 bp is recommended.
>
{: .discussion}


> <hands-on-title>Summarise Trimmed Sequences</hands-on-title>
>
> 1. {% tool [`qiime2 demux summarize`](toolshed.g2.bx.psu.edu/repos/q2d2/qiime2__demux__summarize/qiime2__demux__summarize/2026.1.0+q2galaxy.2026.1.0) %}: 
>  - *"data: SampleData[SequencesWithQuality | PairedEndSequencesWithQuality | JoinedSequencesWithQuality]"*: `trimmed_sequences.qza`
>
> 2. Rename the output to: `trimmed_sequences.qzv`
> 
> 3. Visualisations: Read quality and demux output
> 
>   - Download `trimmed_sequences.qzv` to your local computer and view in [QIIME 2 View](https://view.qiime2.org) (q2view).
>   - [Click to view the **`trimmed_sequences.qzv`** file in QIIME 2 View](https://view.qiime2.org/visualization/?src=https://www.dropbox.com/scl/fo/romu76hw5alep6qj4xfws/AAF9YHZ2oAZQ48Kl-k1Jvyo/trimmed_sequences.qzv?rlkey=z0rtnozon2hlic4ba6i30c301).
>   - Make sure to switch between the "Overview" and "Interactive Quality Plot" tabs in the top left hand corner. Click and drag on the plot to zoom in. Double click to zoom back out to full size. Hover over a box to see the parametric seven-number summary of the quality scores at the corresponding position.
>   ![OverviewQualPlotTabs](./images/q2view_OverviewQualPlotTabs.png)
>
{: .hands_on}




##  Denoising the data

> <callout></callout>
> 
> This step may take a long time to run (i.e. hours), depending on file sizes and available computational power.
>
> Remember to adjust `trunc\_len\_f` and `trunc\_len\_r` according to your own data.
>
{: .callout}


In the following command, a pooling method of 'pseudo' is selected. Pseudo-pooling improves sensitivity to shared low-abundance ASVs across samples while remaining computationally efficient. This is better than the default of 'independent' (where samples are denoised independently) when you expect samples in the run to have similar ASVs overall.

> <caution></caution>
> 
> #### STOP - workshop participants only
> 
> Due to time limitations in a workshop setting, please do NOT run the commands below. You will need to access pre-computed files that this command generates by running the following: `cd; mkdir analysis/dada2out; cp /mnt/shared_data/pre_computed/dada2out/* analysis/dada2out`. If you have accidentally run the command below, `ctrl-c` will terminate it.
>
{: .caution}


> <hands-on-title>DADA2 Denoise Sequences</hands-on-title>
>
> 1. {% tool [`qiime2 dada2 denoise-paired`](toolshed.g2.bx.psu.edu/repos/q2d2/qiime2__dada2__denoise_paired/qiime2__dada2__denoise_paired/2026.1.0+q2galaxy.2026.1.0) %}: 
>  - *"demultiplexed_seqs: SampleData[PairedEndSequencesWithQuality]"*: `trimmed_sequences.qza`
>  - *"trunc\_len\_f: Int"*: `xxx`
>  - *"trunc\_len\_r: Int"*: `xxx`
>  - *"Click here for additional options"*
>  - *"pooling_method: Str % Choices('independent', 'pseudo')"*: `pseudo `
>
> 2. Rename the `table.qza` output to: `dada2out_table.qza`
> 
> 3. Rename the `representative_sequences.qza` output to: `dada2out_representative_sequences.qza`
> 
> 4. Rename the `denoising_stats.qza` output to: `dada2out_denoising_stats.qza`
>
{: .hands_on}


> <challenge></challenge>
>
> #### Calculating truncation lengths
>
> The above code for you likely didn't work if you didn't adjust the truncation length from `xxx` to an integer!
>
> Overlap = (forward truncation length + reverse truncation length) − amplicon length.
>
> For this amplicon, the expected length is ~255 bp. Try a few sensible truncation-length combinations and compare read retention and merging success.
>
> > <solution></solution>
> > 
> > Change this part of the command from:
> > 
> > - *"trunc\_len\_f: Int"*: `xxx`
> > - *"trunc\_len\_r: Int"*: `xxx`
> > 
> > to
> > 
> > - *"trunc\_len\_f: Int"*: `210`
> > - *"trunc\_len\_r: Int"*: `170`
> > 
> > *Tip: Use the up arrow to go back if you tried to run the command before. You can use your arrow keys to edit the command before re-running to replace `xxx` with the numerical values.*
> > 
> {: .solution}
> 
{: .challenge}


## Generate summary files

A [metadata file](https://use.qiime2.org/en/stable/references/metadata.html) is required which provides the key to gaining biological insight from your data. The file <fn>dunnart_metadata.tsv</fn> is provided in the home directory of your Nectar instance. This spreadsheet has already been verified using the plugin for Google Sheets, [keemei](https://keemei.qiime2.org/).  


> <discussion></discussion>
> 
> #### Things to look for
>
> 1. *How many features (ASVs) were generated?* Does this seem reasonable for the sample type? High-diversity communities will usually yield more ASVs than low-diversity communities, but very large numbers can also reflect residual noise or non-target amplification.
> 
> 2. *Do the representative sequences make biological sense?* Taxonomic assignments or BLAST hits should broadly match the expected environment or host (for example, marine, soil, gut, or terrestrial communities).
>     
> 3. *How many reads were retained after filtering, denoising, merging, and chimera removal?* If a large proportion of reads were lost (for example, >50%), this may indicate that trimming or truncation settings were too stringent, read quality was poor, or overlap between forward and reverse reads was insufficient.
> 
> 4. *Did most samples retain enough reads for downstream analysis?* Samples with very low final read counts may still be usable in some contexts, but they should be interpreted cautiously and may need to be excluded later.
>
{: .discussion}


> <hands-on-title>Tabulate Denoising Stats</hands-on-title>
>
> 1. {% tool [`qiime2 metadata tabulate`](toolshed.g2.bx.psu.edu/repos/q2d2/qiime2__metadata__tabulate/qiime2__metadata__tabulate/2026.1.0+q2galaxy.2026.1.0) %}: 
>  - *"1: input: Metadata"*: 
>    - *"input: Metadata"*: `Metadata from Artifact`
>    - *"Metadata Source"*: `dada2out_denoising_stats.qza`
>
> 2. Rename the output to: `16s_denoising_stats.qzv`
> 
> 3. Visualisation: Denoising Stats
> 
>   - Download `16s_denoising_stats.qzv` to your local computer and view in QIIME 2 View (q2view).
>   - [Click to view the **`16s_denoising_stats.qzv`** file in QIIME 2 View](https://view.qiime2.org/visualization/?src=https://www.dropbox.com/scl/fo/romu76hw5alep6qj4xfws/AAsCKOqmM-t2RhSr39K7E_g/16s_denoising_stats.qzv?rlkey=z0rtnozon2hlic4ba6i30c301).
>
{: .hands_on}


> <hands-on-title>Summarise DADA2 Table</hands-on-title>
>
> 1. {% tool [`qiime2 feature-table summarize`](toolshed.g2.bx.psu.edu/repos/q2d2/qiime2__metadata__tabulate/qiime2__metadata__tabulate/2026.1.0+q2galaxy.2026.1.0) %}: 
>  - *"table: FeatureTable[Frequency | PresenceAbsence]"*: `dada2out_table.qza`
>  - *"Click here for additional options"*
>      - *"1: input: Metadata"*: 
>          - *"input: Metadata"*: `Metadata from TSV`
>          - *"Metadata Source"*: `dunnart_metadata.tsv`
>
> 2. Rename the output to: `summary_table.qzv`
> 
> 3. Visualisation: Feature/ASV summary
> 
>   - Download `summary_table.qzv ` to your local computer and view in QIIME 2 View (q2view).
>   - [Click to view the **`summary.qzv`** file in QIIME 2 View](https://view.qiime2.org/visualization/?src=https://www.dropbox.com/scl/fo/romu76hw5alep6qj4xfws/ADpnQOqVK-JD1zIkLejSfmY/summary_table/summary.qzv?rlkey=z0rtnozon2hlic4ba6i30c301).
>   - Make sure to switch between the "Overview" and "Feature Detail" tabs in the top left hand corner. 
>    ![ASV_detailPNG](./images/q2view_ASV_detail.png)
>
{: .hands_on}


> <hands-on-title>Tabulate Representative Sequences</hands-on-title>
>
> 1. {% tool [`qiime2 feature-table tabulate-seqs`](toolshed.g2.bx.psu.edu/repos/q2d2/qiime2__feature_table__tabulate_seqs/qiime2__feature_table__tabulate_seqs/2026.1.0+q2galaxy.2026.1.0) %}: 
>  - *"data: FeatureData[Sequence | AlignedSequence]"*: `dada2out_representative_sequences.qza`
>
> 2. Rename the output to: `16s_representative_seqs.qzv`
> 
> 3. Visualisation: Denoising Stats
> 
>   - Download `16s_representative_seqs.qzv ` to your local computer and view in QIIME 2 View (q2view).
>   - [Click to view the **`16s_representative_seqs.qzv`** file in QIIME 2 View](https://view.qiime2.org/visualization/?src=https://www.dropbox.com/scl/fo/romu76hw5alep6qj4xfws/AHIIyoQHzEzPyoEXzjBVxBc/16s_representative_seqs.qzv?rlkey=z0rtnozon2hlic4ba6i30c301).
>
{: .hands_on}







# Conclusion
