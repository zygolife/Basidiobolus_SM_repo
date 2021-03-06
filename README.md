# About this repo:

This repository includes all the files used to reconstruct the figures on Tabima et al. (In Prep) as well as the files not included in the submitted manuscript.

To reconstruct the figures download or clone this repository and execute the `Readme.Rmd` on Rstudio with the `knitr` and all the required packages installed. A rendered version of this document can be found on the `Readme.html` included in this repo

Most files are in `Rmd` format. This is both to create small, binary files to be executed rapidly in `R` and to replicate the figures as accurately as possible.

***

# List of files:

## Main Figures

* `Fig1/` (Abundance of secondary metabolite (SM) core genes in zygomycetes)
  - `Zygo_SM_count.csv`: CSV file summary counts of SM core genes in 69 species of zygomycetes.

* `Fig2/` (RNA expression of secondary metabolite (SM) core genes in *Basidiobolus meristosporus CBS 931.37*)
  - `count_RNA.Rds`: Rds file with TPS per gene model of *Basidiobolus meristosporus CBS 931.37*

* `Fig4/` (Phylogenetic origin of NRPS A-domains in *Basidiobolus* species)
  - `Colors_arrow_origin.Rds`: Rds file with color schemes for phylogenetic origin of A-domains of *Basidiobolus* NRPS proteins
  - `Colors_arrow.Rds`: Rds file with color schemes for backbone of figure
  - `domains_gene_length.Rds`: Rds file with domain lengths of A-domains of *Basidiobolus* NRPS proteins
  - `domains_species.Rds`: Rds files with coordinates of  A-domains of *Basidiobolus* NRPS proteins

* `Fig7/` (Horizontal gene transfer in *Basidiobolus* species)
  - `HGT_counts.txt`: Summary of number of protein with matches to Bacterial protein sequences from RefSeq.
  
* `Fig8/` (Measurements from siderophore assays of *Basidiobolus meristosporus CBS 931.37* and other treatments and control)
  - `Siderophore_Measurements.txt`: Data frame with raw easurements from the siderophore assays of *Basidiobolus meristosporus CBS 931.37* , other treatments and control
  
## Supplementary Figures

* `SF1/` (NRPS A-domain phylogenetic tree)
  - `Bushley_names.txt`: Data frame of names from the NRPS reconstruction of [Bushley and Turgeon, 2010](https://www.ncbi.nlm.nih.gov/pubmed/20100353). Includes names of NRPS A-domains, Simplified names for NRPS A-domains and sub-family assignments.
  - `NRPS.tre`: Phylogenetic tree in NEWICK format from maximum likelihood reconstruction in RAxML using the predicted NRPS A-domains. Bootstrap supports from 1000 replicates are included as `node.labels`
  
* `SF3/` (PKS KS domain phylogenetic tree)
  - `PKS.tre`: Phylogenetic tree in NEWICK format from maximum likelihood reconstruction in RAxML using the predicted PKS KS domains. Bootstrap supports from 1000 replicates are included as `node.labels` 
  
* `SF4/` (Summary of PKS domains in fungal species)
  - `PKS_Fungi.Rds`: Rds file with PKS domain counts for all fungal species included in the manuscript.
  
* `SF5/` (Summary of PKS domains in zygomycetes species)
  - `PKS_counts.txt`: Data frame with PKS domain counts for 69 zygomycete species included in the manuscript.

* `SF6/` (TC phylogenetic tree)
  - `TC.tre`: Phylogenetic tree in NEWICK format from maximum likelihood reconstruction in RAxML using the predicted TC core genes. Bootstrap supports from 1000 replicates are included as `node.labels` 
  
* `SF7/` (HGT assay figures)
  - `GFF_chrom.jcf7180000797043.Rds`: Rds file with GFF from scaffold jcf7180000797043 from *Basidiobolus heterosporus*.
  - `GFF_chrom.jcf7180000803233.Rds`: Rds file with GFF from scaffold jcf7180000803233 from *Basidiobolus heterosporus*.
  - `jcf7180000797043_HGTplot.rds`: Rds file/Data frame with HGT assignments and coverage for gene models harbored in scaffold jcf7180000797043 of *Basidiobolus heterosporus*
  - `jcf7180000803233_HGTplot.rds`: Rds file/Data frame with HGT assignments and coverage for gene models harbored in scaffold jcf7180000803233 of *Basidiobolus heterosporus*
  - `jcf7180000797043_Zscores.Rds`: Rds file/Data frame with Z-scores for each position of scaffold jcf7180000797043 of *Basidiobolus heterosporus*
  - `jcf7180000803233_Zscores.Rds`: Rds file/Data frame with Z-scores for each position of scaffold jcf7180000803233 of *Basidiobolus heterosporus*

* `SF8/` (Intron number in HGT and fungal genes)
  - `intron_number.Rds`: Data frame with Pnumber of introns from genes in *Basidiobolus meristosporus CBS 931.37* classified as product of HGT.

* `SF9/` (5-mer assay in HGT and fungal genes)
  - `pentameres_simple.Rds`: Rds file/data frame with the two main principal components for the 5-mer assay of *Basidiobolus meristosporus CBS 931.37*.
  
* `SF10/` (Codon usage assay in HGT and fungal genes)
  - `pentameres_simple.Rds`: Rds file/data frame with the two main principal components for the codon usage assay of *Basidiobolus meristosporus CBS 931.37*.
  
## Additional files:

* `JGI_code_taxonomy.csv`: List of species and taxonomy indicators from JGI *Mycocosm*
* `PKS_multidomain.hmm`: Multidomain HMMER profile of PKS domains:
  - [KS (PFAM - PF001009)](http://pfam.xfam.org/family/PF00109)
  - [AT (SMART - SM00827)](http://smart.embl-heidelberg.de/smart/do_annotation.pl?BLAST=DUMMY&DOMAIN=SM00827) 
  - [KR (SMART - SM00822)](http://smart.embl-heidelberg.de/smart/do_annotation.pl?DOMAIN=PKS_KR)
  - [DH (SMART - SM00826)](http://smart.embl-heidelberg.de/smart/do_annotation.pl?BLAST=DUMMY&DOMAIN=SM00826)
  - [PP (SMART - SM00823)](http://smart.embl-heidelberg.de/smart/do_annotation.pl?ACC=SM000823&BLAST=DUMMY)

***

# Required packages

```
library(ggplot2)
library(ggrepel)
library(ggpubr)
library(ggtree)
library(gridExtra)
library(phangorn)
library(phytools)
library(tidyverse)
library(reshape2)
```

# Main Figures

> Figures 3, 5 and 6 were constructed manually.

## Figure 1. Summary of SM

```
zygo.all <- read.csv("Fig1/Zygo_SM_count.csv", header = T, stringsAsFactors = F)
zygo.all$SM_normalized <- zygo.all$SM/zygo.all$X..gene.models
zygo.all.m <- melt(zygo.all, id.vars = c("JGI.Identifier","Isolate.Species","Order","Phylum"))
zygo.all.m$gene_fam <- "Secondary_Metabolyte"
zygo.all.m$gene_fam[zygo.all.m$variable %in% c("Genome.size..Mb.")] <- "Genome_size"
zygo.all.m$gene_fam[zygo.all.m$variable %in% c("X..gene.models")] <- "Number_of_genes"
zygo.all.m$gene_fam [zygo.all.m$variable %in% c("SM_normalized")] <- "Proportion of SM per total genes"

# Plot
ggplot(zygo.all.m) + geom_bar(aes(x=Isolate.Species, y=value, fill=variable), stat="identity") + 
  facet_grid(gene_fam ~ Order + Phylum, scales = "free", space = "free_x") + 
  scale_fill_viridis_d() + 
  theme_classic() + 
  theme(axis.text.x = element_text(angle = 90, hjust = 1))
```


## Figure 2. RNA expression

```
count.RNA <- readRDS("Fig2/count_RNA.Rds")

# Plot
ggplot(count.RNA, aes(x=counts.trans)) + geom_histogram(bins = 50) + 
      geom_point(data = count.RNA[!is.na(count.RNA$family),],aes(x=counts.trans, y=yval, colour=family, label = V1)) +    
      geom_text_repel(data = count.RNA[!is.na(count.RNA$family),],aes(x=counts.trans, y=yval, colour=family, label = V1)) +
  scale_x_continuous(breaks = c(0, 0.1, 1, 10, 100, 1000, 10000), trans = scales::log2_trans()) + theme_classic()  + xlab("Transcripts per million (TPM)") + ylab("Count") + scale_colour_viridis_d()
```

## Figure 4: A-domains 

### Reconstructing the domains

```
cols <- readRDS(file = "Fig4/Colors_arrow.Rds")
cols.origin <- readRDS(file = "Fig4/Colors_arrow_origin.Rds")
domains.species <- readRDS("Fig4/domains_species.Rds")
dom.gene.lenght <- readRDS("Fig4/domains_gene_length.Rds")

bashet.nrps <- ggplot(domains.species[[1]], aes(x=1)) + geom_segment(data = dom.gene.lenght[[1]], aes(x=0,xend=end,y=position, yend=position)) + geom_segment(aes(x=start,xend=finish,  y=position, yend=position, color=Class), arrow=arrow(length=unit(0.15,"cm"),  type = "closed"), size=2)  + theme_classic() + facet_grid(Gene ~ ., scales = "free")  + xlab("Position") + ylab("NRPS gene") + scale_color_manual(values = cols[names(cols) %in% unique(domains.species[[1]]$Class)]) + theme(axis.text.y=element_blank(),axis.ticks=element_blank(),legend.position = "bottom",strip.text.y = element_text(angle = 0), axis.line.y = element_blank()) + guides(fill=FALSE)

basmer.jgi.nrps <- ggplot(domains.species[[2]], aes(x=1)) + geom_segment(data = dom.gene.lenght[[2]], aes(x=0,xend=end,y=position, yend=position)) + geom_segment(aes(x=start,xend=finish,  y=position, yend=position, color=Class), arrow=arrow(length=unit(0.15,"cm"),  type = "closed"), size=2)  + theme_classic() + facet_grid(Gene ~ ., scales = "free")  + xlab("Position") + ylab("NRPS gene") + scale_color_manual(values = cols[names(cols) %in% unique(domains.species[[2]]$Class)]) + theme(axis.text.y=element_blank(),axis.ticks=element_blank(),legend.position = "bottom",strip.text.y = element_text(angle = 0), axis.line.y = element_blank()) + guides(fill=FALSE)

basmer.b9252.nrps <- ggplot(domains.species[[3]], aes(x=1)) + geom_segment(data = dom.gene.lenght[[3]], aes(x=0,xend=end,y=position, yend=position)) + geom_segment(aes(x=start,xend=finish,  y=position, yend=position, color=Class), arrow=arrow(length=unit(0.15,"cm"),  type = "closed"), size=2)  + theme_classic() + facet_grid(Gene ~ ., scales = "free")  + xlab("Position") + ylab("NRPS gene") + scale_color_manual(values = cols[names(cols) %in% unique(domains.species[[3]]$Class)]) + theme(axis.text.y=element_blank(),axis.ticks=element_blank(),legend.position = "bottom",strip.text.y = element_text(angle = 0), axis.line.y = element_blank()) + guides(fill=FALSE)

# Plot
grid.arrange(bashet.nrps, basmer.jgi.nrps, basmer.b9252.nrps)
```

## Figure 7: HGT counts

```
HGT.counts <- read.table("Fig7/HGT_counts.txt", sep = "\t", header = T)

HGT.counts$Origin <- factor(HGT.counts$Origin, levels = c("a-proteobacteria","b-proteobacteria","d-proteobacteria","e-proteobacteria","g-proteobacteria","proteobacteria","firmicutes","actinobacteria","high GC Gram+","enterobacteria","planctomycetes","CFB group bacteria","GNS bacteria","verrucomicrobia","fusobacteria","cyanobacteria","chlamydias","mycoplasmas","aquificales","bacteria","euryarchaeotes","archaea"))
HGT.counts.prop <- HGT.counts
HGT.counts.prop$bashet <- HGT.counts$bashet/9331
HGT.counts.prop$basmer_B9252 <- HGT.counts$basmer_B9252/13273
HGT.counts.prop$basmer_HGT <- HGT.counts$basmer_HGT/16111

HGT.counts[order(HGT.counts$Origin, HGT.counts$Origin),]
HGT.counts.prop[order(HGT.counts.prop$Origin, HGT.counts$Origin),]

HGT.counts.m <- melt(HGT.counts.prop)

# Plot
ggplot(HGT.counts.m, aes(x=variable,y=value,fill=Origin)) + geom_bar(stat='identity', position = 'fill') + scale_fill_manual(values = c("#FFAAAA","#E37B7B","#D46A6A","#801515","#550000","#2B0000","#ED8229","#03D5D5","#198E8E","#674A33","#E9038F","#FFFF04","#ED5DBA","#72335B","#7F0855","#08AF13","#AA5704","#73239F","#1CA06E","#221617","#736058","#4E4E4E")) + theme_bw() + xlab("Taxon") + ylab("Normalized proportion of genes with HGT evidence ") + theme_classic()
```

## Figure 8: Siderophore assay

```
side.meas <- read.table("Fig8/Siderophore_Measurements.txt", sep = "\t", stringsAsFactors = F, header = T)

# Plot
ggbarplot(data = side.meas, x = "Label", y="Area", fill="Label", add = "mean_se") + scale_fill_viridis_d(begin=0.9, end = 0.1) + theme(legend.position = "none")
```

# Supplementary figures

> Sup. Figs 2 and 11 were constructed by hand

## Sup. Figure 1: NRPS tree

```
zygo_tree <- read.tree("SF1/NRPS.tre")

# Reading assignments from Bushley 2010
table.names <- read.table("SF1/Bushley_names.txt", sep = "\t", header = T, stringsAsFactors = F)

# Assigning names
alin.names.org <- data.frame(names=zygo_tree$tip.label, group=table.names$Group[match(zygo_tree$tip.label,table.names$name.or.i.)], stringsAsFactors = F)

# Names_step1
names.step1 <- strsplit(alin.names.org$names, split = "_") %>% lapply(function (x) paste(x[1], x[2])) %>% unlist 
names.step1[grep(names.step1, pattern = "/")] <- grep(names.step1, pattern = "/", value = T) %>% strsplit(split = " ") %>% lapply(function (x) x[1]) %>% unlist
names.step1 <-  gsub(names.step1, pattern = " 1$", replacement = "_1") %>% gsub(pattern = " 2$", replacement = "_2") %>% gsub(perl = T, pattern = " \\d+$", replacement = "_JGI")
names_NRPS <- data.frame(tip.label= zygo_tree$tip.label, file= names.step1, stringsAsFactors = F)

# Separating by genus
names_NRPS$file <- strsplit(names_NRPS$file, split = " ", fixed = T) %>% lapply(function (x) x[1]) %>% unlist %>% gsub(pattern = "jgi\\|", replacement = "") %>% strsplit(split = "|", fixed = T) %>% lapply(function (x) x[1]) %>% unlist 

names_NRPS$genus <- names_NRPS$file

# JGI names
all.jgi <- read.csv('JGI_code_taxonomy.csv')
head(all.jgi)
all.jgi$genus <- strsplit(as.character(all.jgi$Species), split = " ", fixed = T) %>% lapply(function (x) x[1])

# Merging the names
zygo.tree <- merge(names_NRPS, all.jgi,by = 'file', no.dups = T, sort = F)
zygo.tree <- zygo.tree[c(2,4)]
fungi.tree <- merge(names_NRPS, all.jgi,by = 'genus', no.dups = T, sort = F)
fungi.tree <- fungi.tree[c(2,4)]
fungi.tree <- fungi.tree[!duplicated(fungi.tree),]

fungi.all <- rbind(fungi.tree, zygo.tree)
fungi.all <- fungi.all[grep(names_NRPS$tip.label, pattern = "Basme2finSC",invert = T),]
fungi.all <- rbind(fungi.all, data.frame("tip.label" = grep(names_NRPS$tip.label, pattern = "N161|Basme2finSC", value = T), "Phylum_name" = "BasMer"))
fungi.all <- rbind(fungi.all, data.frame("tip.label" = grep(names_NRPS$tip.label, pattern = "N168", value = T), "Phylum_name" = "BasHet"))

# Plotting the tree
zygo_fort <- fortify(zygo_tree)
zygo_fort$bootstrap <- NA
zygo_fort$bootstrap[!zygo_fort$isTip] <- as.numeric(zygo_tree$node.label)
zygo_fort$bootstrap[zygo_fort$bootstrap < 70] <- NA

ggtree(zygo_fort, size=0.3) %<+% fungi.all + geom_tiplab(size=1, aes(color=Phylum_name)) + geom_text(aes(label=bootstrap), vjust=-.5, hjust=-.5, size=1) + theme(legend.position = "bottom") 
```

Figure was finalized by hand in Adobe Illustrator 2020 to color the missing tip labels, improve legibility and legend, and extend root.

## Sup. Figure 3: PKS tree

```
zygo_tree <- read.tree("SF3/PKS.tre")

# Assigning names
alin.names.org <- data.frame(names=zygo_tree$tip.label, stringsAsFactors = F)

# Names_step1
names.step1 <- strsplit(alin.names.org$names, split = "_") %>% lapply(function (x) paste(x[1], x[2])) %>% unlist 
names.step1[grep(names.step1, pattern = "/")] <- grep(names.step1, pattern = "/", value = T) %>% strsplit(split = " ") %>% lapply(function (x) x[1]) %>% unlist
names.step1 <-  gsub(names.step1, pattern = " 1$", replacement = "_1") %>% gsub(pattern = " 2$", replacement = "_2") %>% gsub(perl = T, pattern = " \\d+$", replacement = "_JGI")
names_NRPS <- data.frame(tip.label= zygo_tree$tip.label, file= names.step1, stringsAsFactors = F)

# Separating by genus
names_NRPS$file <- strsplit(names_NRPS$file, split = " ", fixed = T) %>% lapply(function (x) x[1]) %>% unlist %>% gsub(pattern = "jgi\\|", replacement = "") %>% strsplit(split = "|", fixed = T) %>% lapply(function (x) x[1]) %>% unlist 

names_NRPS$genus <- names_NRPS$file

# JGI names
all.jgi <- read.csv('JGI_code_taxonomy.csv')
all.jgi$genus <- strsplit(as.character(all.jgi$Species), split = " ", fixed = T) %>% lapply(function (x) x[1])

# Merging the names
zygo.tree <- merge(names_NRPS, all.jgi,by = 'file', no.dups = T, sort = F)
zygo.tree <- zygo.tree[c(2,4)]
fungi.tree <- merge(names_NRPS, all.jgi,by = 'genus', no.dups = T, sort = F)
fungi.tree <- fungi.tree[c(2,4)]

fungi.all <- rbind(zygo.tree, fungi.tree)
fungi.all <- fungi.all[grep(names_NRPS$tip.label, pattern = "Basme2finSC",invert = T),]
fungi.all <- rbind(fungi.all, data.frame("tip.label" = grep(names_NRPS$tip.label, pattern = "N161|Basme2finSC", value = T), "Phylum_name" = "BasMer"))
fungi.all <- rbind(fungi.all, data.frame("tip.label" = grep(names_NRPS$tip.label, pattern = "N168", value = T), "Phylum_name" = "BasHet"))

# Plotting the tree
zygo_fort <- fortify(zygo_tree)
zygo_fort$bootstrap <- NA
zygo_fort$bootstrap[!zygo_fort$isTip] <- as.numeric(zygo_tree$node.label)
zygo_fort$bootstrap[zygo_fort$bootstrap < 70] <- NA

ggtree(zygo_fort, size=0.3) %<+% fungi.all + geom_tiplab(size=1, aes(color=Phylum_name)) + geom_text(aes(label=bootstrap), vjust=-.5, hjust=-.5, size=1) + theme(legend.position = "bottom") 
```

Figure was finalized by hand in Adobe Illustrator 2020 to color the missing tip labels, improve legibility and legend,and extend root.

## Sup. Figure 4: Fungal PKS

```
dom.df.m <- readRDS("SF4/PKS_Fungi.Rds")

# Plot
ggplot(dom.df.m, aes(x=variable, fill=value, y=AA)) +
  geom_tile(colour="black", show.legend = F) +
  theme_classic() +
  facet_grid(Phylum.name + Species ~ ., scale = "free", space = "free") +
  scale_x_discrete(position = "top") +
  xlab("Domain") + 
  theme(strip.text.y = element_text(size=9, face = "bold", angle = 360),strip.background = element_rect(size=0), axis.text.x = element_text(angle = 90, hjust = 1))
```


## Sup. Figure 5: Zygo PKS

```
dom.df <- read.table("SF5/PKS_counts.txt", sep = "\t", header = T, comment.char = '')

# Plot
dom.df.m <- melt(dom.df)
ggplot(dom.df.m, aes(x=variable, fill=value, y=AA)) +
  geom_tile(colour="black", show.legend = F) +
  theme_classic() +
  facet_grid(source + Order + Species ~ ., scale = "free", space = "free") +
  scale_x_discrete(position = "top") +
  xlab("Domain") + 
  theme(strip.text.y = element_text(size=1, face = "bold", angle = 360),strip.background = element_rect(size=0), axis.text.x = element_text(angle = 90, hjust = 1)) +
  scale_fill_viridis_c(begin = 0.8, end = 0.8, na.value = "grey90")
```

## Sup. Figure 6: TC tree

```
zygo_tree <- read.tree("SF6/TC.tree")

# Assigning names
alin.names.org <- data.frame(names=zygo_tree$tip.label, stringsAsFactors = F)

# Names_step1
names.step1 <- strsplit(alin.names.org$names, split = "_") %>% lapply(function (x) paste(x[1], x[2])) %>% unlist 
names.step1[grep(names.step1, pattern = "/")] <- grep(names.step1, pattern = "/", value = T) %>% strsplit(split = " ") %>% lapply(function (x) x[1]) %>% unlist
names.step1 <-  gsub(names.step1, pattern = " 1$", replacement = "_1") %>% gsub(pattern = " 2$", replacement = "_2") %>% gsub(perl = T, pattern = " \\d+$", replacement = "_JGI")
names_TC <- data.frame(tip.label= zygo_tree$tip.label, file= names.step1, stringsAsFactors = F)

# Separating by genus
names_TC$file <- strsplit(names_TC$file, split = " ", fixed = T) %>% lapply(function (x) x[1]) %>% unlist %>% gsub(pattern = "jgi\\|", replacement = "") %>% strsplit(split = "|", fixed = T) %>% lapply(function (x) x[1]) %>% unlist 

names_TC$genus <- names_TC$file

# JGI names
all.jgi <- read.csv('JGI_code_taxonomy.csv')
all.jgi$genus <- strsplit(as.character(all.jgi$Species), split = " ", fixed = T) %>% lapply(function (x) x[1])

# Merging the names
zygo.tree <- merge(names_TC, all.jgi,by = 'file', no.dups = T, sort = F)
zygo.tree <- zygo.tree[c(2,4)]
fungi.tree <- merge(names_TC, all.jgi,by = 'genus', no.dups = T, sort = F)
fungi.tree <- fungi.tree[c(2,4)]

fungi.all <- rbind(zygo.tree, fungi.tree)
fungi.all <- fungi.all[grep(names_TC$tip.label, pattern = "Basme2finSC",invert = T),]
fungi.all <- rbind(fungi.all, data.frame("tip.label" = grep(names_TC$tip.label, pattern = "N161|Basme2finSC", value = T), "Phylum_name" = "BasMer"))
fungi.all <- rbind(fungi.all, data.frame("tip.label" = grep(names_TC$tip.label, pattern = "N168", value = T), "Phylum_name" = "BasHet"))

# Plotting the tree
zygo_fort <- fortify(zygo_tree)
zygo_fort$bootstrap <- NA
zygo_fort$bootstrap[!zygo_fort$isTip] <- as.numeric(zygo_tree$node.label)
zygo_fort$bootstrap[zygo_fort$bootstrap < 70] <- NA

ggtree(zygo_fort, size=0.3) %<+% fungi.all + geom_tiplab(size=1, aes(color=Phylum_name)) + geom_text(aes(label=bootstrap), vjust=-.5, hjust=-.5, size=1) + theme(legend.position = "bottom") 
```

Figure was finalized by hand in Adobe Illustrator 2020 to color the missing tip labels, improve legibility and legend,and extend root.

## Sup. Figure 7: HGT assay

- Negative:

```
jcf7180000803233 <- readRDS(file = "SF7/jcf7180000803233_HGTplot.Rds")
chom.sub.all <- readRDS(file = "SF7/jcf7180000803233_Zscores.Rds")
GFF.chrom <- readRDS(file = "SF7/GFF_chrom.jcf7180000803233.Rds")

# Coverage plot
cov.plot <-ggplot(data = jcf7180000803233, aes(x=Pos, y=Cov)) + 
  geom_line() + 
  geom_segment(data = GFF.chrom, aes(x=Start, xend=End, y=-1, yend=-1, color=Origin),arrow=arrow(length=unit(0.1,"inches"),  type = "closed"), size = 1, lineend = "butt", linejoin = "mitre") + 
  scale_y_continuous(breaks=seq(0,1500,100)) + 
  theme_classic() + 
  theme(legend.position = "bottom")

# Z-score plot
zscore.plot <- ggplot(data=chom.sub.all, aes(x=Pos, y=zscore)) + 
  geom_point(size=0.5) + 
  geom_hline(yintercept=c(-1, 1), color="forestgreen") + 
  geom_hline(yintercept=c(-2, 2), color="red") + 
  geom_segment(data = GFF.chrom, aes(x=Start, xend=End, y=-1, yend=-1, color=Origin), size = 3) + 
  theme_bw()

# Plot
ggarrange(cov.plot, zscore.plot ,nrow = 2, labels = c("Coverage", "Zscore"))
```

- Positive

```
jcf7180000797043 <- readRDS(file = "SF7/jcf7180000797043_HGTplot.Rds")
chom.sub.all <- readRDS(file = "SF7/jcf7180000797043_Zscores.Rds")
GFF.chrom <- readRDS(file = "SF7/GFF_chrom.jcf7180000797043.Rds")

# Coverage plot
cov.plot <-ggplot(data = jcf7180000797043, aes(x=Pos, y=Cov)) + 
  geom_line() + 
  geom_segment(data = GFF.chrom, aes(x=Start, xend=End, y=-1, yend=-1, color=Origin),arrow=arrow(length=unit(0.1,"inches"),  type = "closed"), size = 1, lineend = "butt", linejoin = "mitre") + 
  scale_y_continuous(breaks=seq(0,1500,100)) + 
  theme_classic() + 
  theme(legend.position = "bottom")

# Z-score plot
zscore.plot <- ggplot(data=chom.sub.all, aes(x=Pos, y=zscore)) + 
  geom_point(size=0.5) + 
  geom_hline(yintercept=c(-1, 1), color="forestgreen") + 
  geom_hline(yintercept=c(-2, 2), color="red") + 
  geom_segment(data = GFF.chrom, aes(x=Start, xend=End, y=-1, yend=-1, color=Origin), size = 3) + 
  theme_bw()

# Plot
ggarrange(cov.plot, zscore.plot ,nrow = 2, labels = c("Coverage", "Zscore"))
```

Figure was finalized by hand in Adobe Illustrator 2020 

## Sup. Figures 8: Intron Number

```
intron.df <- readRDS("SF8/intron_number.Rds")

# Plot
ggviolin(intron.df, x="origin.x",y="num_introns", fill="origin.x", add = "boxplot", add.params = list(fill = "white"), draw_quantiles = T) + 
  scale_fill_viridis_d(begin = 0.5) + 
  xlab("Presumptive origin") +
  ylab("Number of introns")
```

## Sup. Figure 9: Pentamers (Local)

```
pca.penta <- readRDS(file = "SF9/pentameres_simple.Rds")
pca.penta.bg <- pca.penta[,c(1:3)]

# Plot
penta.p <- ggplot(pca.penta, aes(x=PC1, y=PC2, color=label)) + 
  geom_point(data=pca.penta.bg, color="grey90", alpha = .9) + 
  geom_point() +
  theme_bw() +
  facet_grid(rows = vars(label), cols=vars(origin)) + 
  scale_color_viridis_d(option = "magma", begin = 0, end = 0.8) +
  guides(fill=FALSE, color=FALSE)

penta.p
```


## Sup. Figure 10. Codon Usage

```
pca.df <- readRDS(file = "SF10/codon_usage_simple.Rds")
pca.df.bg <- pca.df[,c(1:3)]

# Plot
codon.p <- ggplot(pca.df, aes(x=PC1, y=PC2, color=label)) + 
  geom_point(data=pca.df.bg, color="grey90", alpha = .9) + 
  geom_point() +
  theme_bw() +
  facet_grid(rows = vars(label), cols=vars(origin)) + 
  scale_color_viridis_d(option = "magma", begin = 0, end = 0.8) +
  guides(fill=FALSE, color=FALSE)

codon.p
```
