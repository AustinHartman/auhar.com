---
title: "Are doublets detected via similarity to artificial doublets valid?"
layout: post
---

In this post I’m going to briefly explore the validity of a specific 
type of doublet detection method, by assessing the validity of putative 
doublets by a mode not explored in the method's [paper][scrublet-link]. The method 
of doublet detection I am curious about are doublets detected based 
on similarity to artificially generated doublets. Multiple variants of
this method have been published. For now, I am going to focus on one 
method called Scrublet. ([Scrublet][scrublet-link], [DoubletFinder][doubletfinder-link])

### Detecting doublets by doublet simulation:
This method is quite simple. Select random pairs of cell barcodes from
an experiment. Then generate an artificial profile from those cell
barcodes by combining the counts from one cell barcode and the count 
from the other. (Scrublet allows for subsampling of the UMIs from the
artificially generated doublets, but by default there is no UMI
subsampling. UMI subsampling may be useful since creating artificial
doublets without subsampling could introduce bias towards high UMI cell
barcodes.) This new profile represents a single simulated doublet. This
process is repeated enough times to span the possible combinations of
cell doublets. For example, if there are 5 clusters representing 5 unique
cell types, it would be important to generate artificial doublets
arising from each possible cluster pairing. That way, the artificial
doublets will iterate all possible combinations of doublets arising from
droplets with different cell types. Once artificial doublets are
generated the next step is to identify the cell barcodes which are most
similar to the artificial profiles. When viewing these doublets in a
low-dimensional projection, they usually appear as an intermediate
cluster between two clusters.

### Detecting doublets by TCR and BCR sequence presence:
This method assumes that the presence of a TCR and BCR sequence for a
given barcode is not biologically reasonable. Thus, if a TCR and BCR
library identify sequences each with the same barcode, then it indicates
something went wrong and such barcodes should be removed. These barcodes
are the barcodes which are found in the BCR filtered contigs and the
TCR filtered contigs.

### Dataset and results
Using [this][dataset-link] 10x Genomics melanoma public dataset I ran Scrublet using
standard parameters and a short script to detect doublets using the
validation method described above. The scrublet method detected 160
doublets while the validation method detected 168 doublets. The
intersection of these sets of barcodes was 117. I found this to be much
higher than I had expected, and I suppose that’s a good thing.

The image below reiterates the overlap between the two methods of doublet
detection. There seems to be one main region in the top left (cloud of red)
which both methods classify as full of doublets. Around UMAP 1 coordinate 7 and 
UMAP 2 coordinate 2 there are a couple small clusters with a few cell
barcodes sprinkled in between. Scrublet labels some of them as doublets
but the validation method does not. I think this brings up an important 
limitation in the validation method. Because doublets are detected based
on the presence of a TCR and BCR contig, only T cell and B cell can be
detected. This also raises important questions about what the expected 
upper limit for overlap between the two methods putative doublets is,
since it must be below one. According to [Biolegend][biolegend-cellfreq-link], the expected cell frequencies for PBMCs are
60-80% T cells and 5-15% B cells with natural killer cells, monocytes,
and dendritic cells making up the remaining population. Given melanoma
datasets are less common than PBMCs and possibly more variable, I'd like
to redo this analysis on a more common sample such as PBMCs. This would
allow further confidence in validation because when the underlying cell
frequencies are known, the hypothetical upper bound on putative doublet 
across methods can be better compared. 

![doublets](/assets/scrublet-vs-tcrbcr-doublets.png)

[scrublet-link]: https://doi.org/10.1016/j.cels.2018.11.005
[doubletfinder-link]: https://doi.org/10.1016/j.cels.2019.03.003
[dataset-link]: https://support.10xgenomics.com/single-cell-vdj/datasets/4.0.0/sc5p_v2_hs_melanoma_10k?
[biolegend-cellfreq-link]: https://www.biolegend.com/en-us/blog/expected-cell-frequencies
