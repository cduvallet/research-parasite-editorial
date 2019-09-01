Data detectives, README's, and humility: a research parasite's perspective
Claire Duvallet, PhD

# Introduction

In sharp contrast with some unfounded fears that open data will lead to the rise of "research parasites," enabling re-analyses of existing datasets by making them publicly available adds substantial value to scientific research.
Publicly available raw data allows researchers to ask and answer new questions, testing their hypotheses \textit{in silico} without the need for costly new studies.
New studies can also be compared with existing work to determine which findings hold across different studies and contexts.
In my PhD, I performed a meta-analysis of 28 gut microbiome studies, where I downloaded and reprocessed raw sequencing data to look at patterns of associations between the gut microbiome and 10 different diseases (Duvallet et al. 2018).

When I first embarked on this project, I thought it would be straight-forward and easy to use existing data to answer some low-hanging-fruit questions about my field.
Of course, it wasn't: through this project, I learned that performing a meta-analysis is much more than a simple `stamp collection` endeavor that anyone with basic knowledge of computational tools could do, but is rather a unique and valuable contribution to the field.
As the 2019 Junior Research Parasite, I was recognized for my work and given this opportunity to share some of my thoughts and perspectives on life as a parasite.

# Becoming a data detective

The first step to becoming a research parasite is to learn the skills of a data detective: finding, downloading, and reprocessing data.
While public databases and literature search engines make the process of finding data much easier, identifying datasets for a specific research question remains challenging.
In my meta-analysis, I used a combination of NCBI literature searches, finding papers from review papers, and most importantly following chains of references from individual studies.
Many of the datasets I ended up using were deposited in publicly available databases, but not all.
I learned to carefully scrutinize the paper and its supplement to find raw data links and associated metadata, information which was often scattered through multiple supplementary files.
Eventually I gained a short-hand intuition: if a ctrl-F for "deposited," "available," "accessed," "SRA", "ENA" was not fruitful, I knew I should probably go ahead and email the authors.
But even this simple act wasn't always straightforward: some of my emails went to long-dead addresses, others went to very busy PI's who never responded.
So I learned to scour the internet to find the most up-to-date corresponding author email and, at times, also identifying the first author who might have a better response rate.

## Data without metadata is useless

Beyond downloading data, gathering all of the metadata required to reprocess and reanalyze a datasets is often the most Herculean task of all.
In my meta-analysis, I identified three sorts of required metadata: (1) metadata linking the raw data IDs (e.g. file names, SRA run IDs) to their corresponding sample IDs, (2) metadata containing technical processing information (e.g. sequencing barcodes, sample replicate, sampling date, etc) and (3) biological or clinical metadata (e.g. disease status, tissue type, etc).
Without any one of these, the entire dataset is useless.
Here also, I learned some tricks. Among my favorites: looking at the raw data itself to infer the presence or absence of primers or barcodes, making educated guesses about disease status from the sample IDs, and learning to look in all the nooks and crannies of the SRA sample descriptors to find what I needed.

In total, I identified 58 studies from my ad hoc literature search that passes the inclusion criteria for my meta-analysis, 28 of which were included in the paper: a success rate of just under 50%.
The majority of my failures came from studies which shared data upon request: only three of the sixteen authors I emailed yielded a full dataset that I could use and which I acquired in time for my meta-analysis.
Another very common failure mode was the lack of metadata.
Even in cases where the raw data was readily available in a database, the metadata required some detective work about a third of the time.


# Reproducible analyses as an act of self-love

It turns that acquiring data is only half of the battle: keeping track of all the wrangling and re-analyzing is another underestimated task of its own in data re-analysis.
A turning point in this project (and my PhD in general) was learning about the concepts behind Cookie Cutter Data Science: setting up a standard project structure; tracking raw data, intermediate data, and analysis results separately; and writing an automated pipeline to put all the work together was critical to my success as a research parasite.

## Data processing

Parallel processing and save intermediate files so you don't have to re-process every single dataset each time you realize you need to fix something in one.

Makefiles are for the world and for you.

Save intermediate files


## README's are your friend

README's about:
- downloading and processing data steps, including weird stuff that happened and why you made the decisions you made
- how you organized everything and where all the data lives
- what code does what and how they all fit together
- how others can use or build upon what you've done

hmm, need to add something about README's here. Maybe as a new section before the reproducible analyses introduction?

# Data

## Data without metadata is useless

## How to be a data detective

## Success rates

# Reproducible analyses

## Data and code without documentation is useless

## Pipeline your analysis: it's good for you first!

I used Make, have heard great things about other pipelining tools like snakemake. A friend of mine once pointed out that Makefiles are actually most useful for you: they explicitly document all of the steps needed to reproduce an analysis, so that you can remember exactly what you did when you go back six months later for those reviewer comments.

# Perspective / conclusions

## Beyond data: code and community to democratize access to scientific research

## Humility

- getting all the metadata together and in the right place is hard (one-third of datasets in SRA had metadata elsewhere)
- but requiring metadata fields is a delicate balance: I myself was incredibly confused when I needed to deposit data for a different project, and I'm sure I missed some important information. Data generation is a collaborative, lengthy process, and the person depositing the data is rarely if ever involved in every step of the data generation. Thus, not only do we need to require data sharing, but we also need to make it easier, more accessible, and more amenable to asking questions and making edits to the submission.

# Conclusions

Thanks to people leading the way to recognize and value this sort of work.



# Notes/drafts

A core theme that has emerged from my thesis work is that re-analyzing existing microbiome datasets can add substantial value to our field.
One of my personal conclusions from the meta-analysis is that new cross-sectional gut microbiome studies should be regularly contextualized within the existing published body of work, almost as mini meta-analyses of their own.
Now that microbiome datasets are more readily available and bioinformatics tools to process and analyze them are becoming very accessible, I hope that researchers make it a habit to ask: are these associations replicated in independent patient cohorts? And: are they specific to my disease of interest or are they part of a non-specific response to health and disease?

I also found the value-add of re-analyzing datasets especially relevant in microbiome research led by clinicians.
For example, the original IBD FMT trials that I re-analyzed in Chapter \ref{chap:donor-selection} did not thoroughly investigate potential donor effects on patient response in their original studies.
This is expected in part because donor heterogeneity was not usually a primary research question of interest, and also because the trials were not powered for such analyses.
However, now that multiple IBD FMT trials have been published with paired patient and donor microbiome sequencing data, hypotheses about what leads to improved patient response can be tested \textit{in silico} (as we did for butyrate producer abundance in Chapter \ref{chap:donor-selection}).
In Chapter \ref{chap:meta-analysis}, many of my datasets were pulled from studies led by clinical researchers who may not have had access to the bioinformatics and statistical expertise to fully interrogate disease associations within their datasets.
By making their data publicly available, their work continued to contribute new knowledge to the field.

Moving forward, I hope and expect that researchers continue to make their raw data publicly available and that re-analyses of such data become standard in the field.
Publicly available raw data allows researchers to ask and answer new questions, testing their hypotheses \textit{in silico} without the need for costly new studies.
New studies can also be compared with existing work to determine which of their findings hold across different studies and which are specific to their specific study.
However, using published data in new contexts comes with challenges.
Another major challenge is data availability, and specifically clinical metadata like patient disease diagnosis.
Through this work, I have come to realize that raw data without its associated metadata is in almost all cases useless.
Given these challenges, standards for sharing data which respect patient privacy, clinicians' efforts for patient recruitment, and the needs of computational biologists will need to be agreed upon and upheld as a community.

### Finding knowledge in information

A turning point in my thesis came when I read Gene Glass's 1976 paper coining the term `meta-analysis` \cite{glass-1976}.
In it, Glass argues for the underappreciated importance of consolidating and synthesizing information into knowledge, prizing work that aims to find meaning and draw conclusions from disparate existing studies.
This was a turning point in my thesis for two reasons.
First, it was the moment I became truly proud of my work, especially the meta-analysis in Chapter 3: I realized that it was not just some sort of microbiome ``stamp collection`` endeavor that anyone with basic knowledge of computational tools could do, but was instead difficult and valuable work that I had uniquely contributed to.
After reading this piece, my perspective on my thesis work changed: before, I sometimes felt that the inherent limitations of computational work meant that projects like mine were not quite as valuable as theses which develop novel experimental methods or generate new data directly testing biological hypotheses.
Now, I recognize that they are also invaluable work on their own merit.

Second, reading Glass's words helped me recognize a uniting theme in all of my work: finding the ``knowledge in the information.``
I realized that in each project presented in this thesis, I had not just mined the data to find statistical associations, but rather to interpret the associations I found and chase them all the way to their potential clinical or public health implications.
I hope that as we move forward in this exciting and vibrant field, microbiome researchers collectively become less satisfied with simply reporting new information, instead emphasizing and valuing efforts that synthesize existing knowledge and generate new insights that lead more directly to clinical impact.

# Old text




 which was completely associated

Many datasets which I failed to acquire were

3. in SRA but no metadata
1. weird data format
1. no replicate IDs
only 3/16 authors I had to email ended up getting me the full dataset I needed.



When data was not  available,

In order to successfully become a research parasite, you have to get really good at becoming a data detective.
The data detective has two main roles: find the data, and then interpret it.

Although many databases make finding publicly available data, identifying data the is suitable to your research question of interest is still quite challenging.
In my case, many studies of interest were performed by clinicians and published in journals without data sharing agreements.


The first step to re-analyzing data is to download and reprocess it yourself.
In my study, I identified

The most important lesson I learned from this work is that data without metadata is useless.






In my study, I performed an ad-hoc literature review to identify datasets


I also gained skills and perspectives that have since enabled to be a much more effective computational scientist and official "Junior Research Parasite."




I was awarded the "Junior Research Parasite" award for this work, and in the process also learned many invaluable lessons about being part of the open data and open science community.



And through this work, I've also come to understand many additional lessons.

, reproducible and open science, and

re-analyzing existting datasets adds substantial value to the field.

This is the work of "research parasites"

However, using published data in new contexts comes with challenges.
"Research parasites"

I received the Junior Research Parasite award earlier this year for a meta-analysis of 28 gut microbiome studies, where I downloaded and reprocessed raw sequencing data to look at patterns of associations between the gut microbiome and 10 different diseases (Duvallet et al. 2018).
When I embarked on this project, I thought it would be a straight-forward journey to use existing data to answer some low-hanging fruit scientific questions.
I've since learned that performing a meta-analysis is much more than a simple `stamp collection` endeavor that anyone with basic knowledge of computational tools could do, but is rather a unique and valuable contribution to the field.
And through this work, I've also come to understand many additional lessons.



One major challenge is data availability, and specifically clinical metadata like patient disease diagnosis.
Through this work, I have come to realize that raw data without its associated metadata is in almost all cases useless.

In fact, a core theme that emerged from my thesis work is that re-analyzing existting datasets adds substantial value to the field.

I realized that it was not just some sort of microbiome ``stamp collection`` endeavor that anyone with basic knowledge of computational tools could do, but was instead difficult and valuable work that I had uniquely contributed to.

Years later, I realized

A core theme that has emerged from my thesis work is that re-analyzing existing microbiome datasets can add substantial value to our field.
