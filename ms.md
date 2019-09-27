Data detectives, radical self-love, and humility: a research parasite's perspective
Claire Duvallet, PhD

# Introduction

In sharp contrast with some unfounded fears that open data will lead to the rise of "research parasites," enabling re-analyses of existing datasets by making them publicly available adds substantial value to scientific research (NEJM paper).
Publicly available raw data allows researchers to ask and answer new questions, testing their hypotheses \textit{in silico} without the need for costly new studies.
In my PhD, I performed a meta-analysis of 28 gut microbiome studies, where I downloaded and reprocessed raw sequencing data to look at patterns of associations between the gut microbiome and 10 different diseases (Duvallet et al. 2018).
When I first embarked on this project, I thought it would be straight-forward  to use existing data to answer some low-hanging-fruit questions in my field.
But I soon learned that performing a meta-analysis is much more than a simple `stamp collection` endeavor that anyone with basic knowledge of computational tools could do, and is rather a unique and valuable contribution to the field (Glass 1976).
As the 2019 Junior Research Parasite, I was recognized for my work and given this opportunity to share some of the lessons I learned as a parasite here.

## Data

# 1. Research parasites are data detectives

The first step to becoming a research parasite is to learn become a data detective.
While public databases and search engines ease the process of finding data, identifying comprehensive datasets for specific research questions remains challenging.
In my meta-analysis, I relied on NCBI and Google Scholar literature searches, but also supplemented heavily with papers that I found from reviews and by following chains of references from individual studies.

I learned to carefully scrutinize papers and their supplementary materials to find links to raw data and metadata, information which was often scattered throughout the paper and supplement.
I eventually gained some intuition: if a ctrl-F for certain data-related keywords was not fruitful, I knew I should probably go ahead and email the authors.
But even that required some detective work to find up-to-date email addresses and, at times, contact information for the first author, who might be more inclined to reply to my email.
Through every step of the process, I learned to pay attention to strategic details and scour available information for any clues that might help me find what I needed.

# 2. Data without metadata is useless

Gathering all of the metadata required to reprocess and reanalyze a dataset is one of the most difficult parts of a research parasite's work.
As a parasite, I identified three broad types of dataset-related metadata: (1) metadata linking the raw data IDs (e.g. file names, SRA run IDs) to their corresponding sample IDs, (2) metadata containing technical processing information (e.g. sequencing barcodes, sample replicate number, sampling date, etc) and (3) biological or clinical metadata (e.g. disease status, tissue type, etc). [could make a figure/schematic here]
Without any one of these, it is impossible to do a re-analysis and the entire dataset is useless.
Here also, there are many tricks to learn, for example: looking at the raw sequencing data itself to infer the presence or absence of primers or barcodes, making educated guesses about disease status from patterns in the sample IDs, and learning to look in all the nooks and crannies of SRA or ENA sample descriptors.

# 3. Organize yourself for success

After the data has been acquired and re-processed, tracking everything that is done to each dataset is another underestimated task of its own.
Here, intentional file structures and project organization can help.
More specifically, source code should be separated from the data, and each step of the analysis process should produce intermediate files.
Clear project organization makes it easier to figure out what files are what, even after a long time away from the project, and to implement an automated pipeline workflow for your entire analysis.
It also provides encouragement to write parallel and modular scripts, an important trick for research parasites to adopt and which I learned the hard way.
In my meta-analysis, I had one script that performed quality control on all 28 of my datasets in one large for loop.
That meant that each time I found something wrong in my processing for one dataset, I had to re-run the data cleaning for _all_ my data -- a time-consuming process that was a huge pain.
Now, I don't make this mistake any more: in more recent projects, I make sure that each dataset gets its own cleaning step.

As a research parasite, it's a given that you'll definitely make mistakes and need to start your analysis over from scratch many times.
It's important that you set up your data processing and analysis workflows so that it's not a catastrophe each time this happens.

# 4. Approach documentation as leaving clues for future-you

In a way, README's are a research parasite's lab notebook.
Re-analyzing other people's data often takes a long and convoluted path to insight.
Thus, it's especially important that a research parasite's note-taking is flexible and adaptable for any type of analysis that might come up.
Plain-text files like README's solve this issue, and can easily track information about: how the data was downloaded and processed, including any strange things that happened and why certain decisions were made; how the scripts and data are organized, and where all the (raw) data lives; what the scripts do and how they all fit together; and how others can use or build upon what has done.
As a research parasite, it's important to recognize that the most likely beneficiary of thorough documentation is future-you, checking your work before submission, looking for code to do something you know you've already figured out, or going back to answer a question that woke you up in a cold sweat at 2 am.
This was another lesson learned the hard way for me: I remember going back to finalize some processing on datasets I'd downloaded over a year before, and not finding any clues from myself to remember what I did.
In almost all of these cases, it was faster to re-download the data from scratch than to time-travel into the past and remember what I had been thinking.

# 5. The life-changing magic of Makefiles and pipelining workflows

In my opinion, the most revolutionary parasitic tactic of all is pipelining workflows with Makefiles.
A Makefile contains all of the instructions to reproduce every part of an analysis: from downloading raw data, to processing and analyzing it, to even making each of the figures and tables in the eventual paper.
Pipelining workflows use software that reads the instructions in the Makefile to automatically re-run all parts of the analysis which depend on code or data that has been updated since the last time you ran it.
In my meta-analysis, I used generic GNU Make as my pipelining tool, though if I were to undertake another parasitic research project, I'd probably use a more modern and user-friendly pipelining tool like Snakemake (cite nature comment on pipelining, snakemake).

Even though learning to write a Makefile was a lot of work, it was absolutely worth it and made my life much easier.
Makefiles are, by definition, a documentation of all the steps taken for an analysis.
They quite literally answer the question: "wait, how did I do that again?"
More than once while my paper was under review, I panicked and wondered if I'd messed up a processing or analysis step.
With my Makefile, it was easy to go back and find out where I'd done that step and check if everything was doomed as I'd feared.
It never was, and what would have been a harrowing half-day of frantically going back through my spaghetti code usually got quieted down after only a few minutes of poking through my Makefile.

Importantly, having a functional Makefile also made the review process for my paper so much easier.
I knew exactly which files to update or which scripts to re-run when reviewers asked for minor changes to existing analyses.
Adding new analyses based on my data was also easy, because I could just plug in a new script into my Makefile, using intermediate data or analysis files that I'd already created from other steps in my workflow.
And most importantly, my Makefile updated all of the figures and tables automatically as soon as their inputs changed, saving me many hours of tedious detail-checking.

# 6. Computational best practices as an act of radical self-love

Documentation and pipelining are two manifestations of an important philosophy that is crucial to the research parasite's success: implementing best practices in computational research is an act of radical self-love.
Acting in self-love means approaching all decisions not for current-you, but instead for the person who will bear the consequences of my decisions: future-you, long after you've forgotten anything you've thought today.
It isn't possible to enumerate all of the possible best practices or even to identify which ones are practical to implement as PhD students, but I found that as long as I made decisions for future-me rather than only current-me, my life became much easier.

# 7. Democratized software catalyzes data generation by non-specialists

I learned two final important lessons about being a research parasite through my parasitic PhD projects.

The first is that a future where secondary analyses are the norm will be sped along by the development of easy-to-use software that encourages non-computational specialists to generate new datasets.
In the microbiome field, we've seen a recent development of incredibly accessible bioinformatics tools that democratize access to computational analyses (cite qiime2).
I hypothesize that these easy-to-use analysis tools have contributed to an increase in non-specialists generating microbiome sequencing data.
Many microbiome-related clinical trials are beginning to include microbiome analyses as secondary endpoints or to raise the impact of a study.
These analyses would be inaccessible without the easy-to-use software being developed by other parts of the community.
Interestingly, these studies rarely dive into the full potential of their data because they are focused on their primary clinical endpoints.
That leaves a lot of room for research parasites to come in and ask different questions of those datasets, which I think is a great byproduct of developing accessible software suites.

# 8. Practice humility and broaden your perspective

Finally, the biggest lesson I learned from my life as a parasitic PhD student was humility.
As a research parasite, it's easy to get self-righteous and angry whenever the data or metadata isn't easily accessible, but at the end of the day it's more productive to practice perspective-shifting and recognize that everyone is coming from somewhere different.
Especially as junior PhD students, it's easy to forget that what we see as data points or additional N's to our analyses, clinicians see as real people who gave their time and samples to advance research, and in some cases, as patients who are often suffering.

Humility and empathy is also important to recognize that while we stand on our soapboxes advocating for open and reproducible science, it's actually really difficult to do well.
An easy example is data sharing: parasites might like to grumble at how hard it is to find and download raw data, but depositing data is itself a complicated process.
Data generation is a collaborative, lengthy process, and the person depositing the data is rarely if ever involved in every step of the data generation.
Even after downloading and processing 28 datasets, I myself was incredibly confused when I needed to deposit data for a different project that I worked on, and I'm sure I missed some important information that will make a future parasite grumble herself.
Thus, not only do we need to require data sharing, but we also need to make it easier, more accessible, and more amenable to improvements and feedback.
And as we're doing our parasitic research, we need to keep in mind that we are just one small part of an entire ecosystem, and that as parasites, we depend on our hosts to survive.

# Conclusions

Thanks to people leading the way to recognize and value this sort of work.

# References

https://swcarpentry.github.io/good-enough-practices-in-scientific-computing/

https://www.nature.com/articles/d41586-019-02619-z

https://www.tidyverse.org/articles/2017/12/workflow-vs-script/

## Or... make it a checklist? Lessons learned:

1. Research parasites are data detectives
2. Data without metadata is useless
3. Organization your files sets you up for success
4. README's are a research parasite's lab notebook
5. The life-changing magic of pipelining
6. Computational work as an act of radical self-love
7. Democratized software catalyzes data generation by non-specialists
8. Practice humility and perspective: without your host, you die



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



In clinical trials, microbiome data analyses are usually secondary endpoints which

because they reduce the cost of including microbiome data in a study.
In many cases, the microbiome data is a secondary endpoints,
For example, many clinical trials are starting to include microbiome analyses as secondary endpoints.



The interesting thing is that many of these researchers generate incredibly rich datasets and then use their data to answer only a few simple questions which are directly related to their primary research question.
For example, clinical trials usually focus on clinical endpoints but are beginning to include microbiome data to spice up their study.
Accessible analysis tools changes the cost-benefit analysis for the extra spice: now that learning to process and analyze the data is easier, it's worth adding in that extra little bit to increase the interestingness of the study.

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
