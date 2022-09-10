---
title: "Diversity Tackled With R "
teaching: 40
exercises: 10
questions:
- "How can I use R to analyze diversity?"
objectives:
- "Plot alpha and beta diversity."
keypoints:
- "Phyloseq includes diversity analyses such as alpha and beta diversity calculation."
math: true
---

*Look at your fingers, controlled by the mind can do great things. But imagine if each one has a little brain of its own, with 
different ideas, desires, and fears ¡How wonderful things will be made out of an artist with such hands!* 
  -Ode to multidisciplinarity

## First plunge into diversity

Species diversity, in its most simple definition, is the number of species in a particular area and their relative abundance (evenness).
Once we know the taxonomic composition of our metagenomes, we can do diversity analyses. 
Here we will talk about the two most used diversity metrics, α diversity (within one metagenome) and β (across metagenomes).   

- α Diversity: Can be represented as the richness (*i.e.* number of different species in an environment) and abundance of the species in the area(*i.e.* the number of individuals of each species inside the environment). It can be measured by calculating a diversity index such as Shannon's, Simpson's, Chao1, etc. 

<a href="{{ page.root }}/fig/03-07-01.png">
  <img src="{{ page.root }}/fig/03-07-01.png" alt="Alpha diversity diagram: In lake A, we have three fishes, each one of a different species. On lake B, we have two fishes each one of a different species. And in lake C we have four fishes, each one of different species." />
</a>
<em> Figure 1. Alpha diversity is represented by fishes in a pond. Here, alpha diversity is represented in its simplest way: Richness. <em/>
 
- β Diversity: It is the difference (measured as distance) between two or more environments. 
It can be measured with metrics like Bray-Curtis dissimilarity, Jaccard distance, or UniFrac distance, to name a few. Each one 
of this distance, metrics are focused on a characteristic of the community (*e.g.* Unifrac distance measures the phylogenetic relationship
between the species of the community).

In the next example, we will look at the α and the β components of the diversity of a 
dataset of fishes in three lakes. The most simple way to calculate the β-diversity 
is to calculate the species that are distinct between two lakes (sites). Let's take 
Lake A and Lake B to do an example. The number of species in Lake A is 3, to this 
quantity we will suppress the number of these species that are shared with the Lake 
B: 2. So the number of unique species in Lake A compared to Lake B is (3-2):1. To 
this number we will sum the result of the same operations but now take Lake B as 
our site of reference. In the end, the β diversity between Lake A and Lake B is 
(3-2) + (3-2) = 2. This process can be repeated taking each pair of lakes as the 
focused sites.

<a href="{{ page.root }}/fig/03-07-02.png">
  <img src="{{ page.root }}/fig/03-07-02.png" alt=" Alpha and Beta diversity diagram: Each lake has a different number of species and each species has a different number of fish individuals. Both metrics are taken into account to measure alfa and beta diversity." />
</a>
<em> Figure 2. Alpha and Beta diversity represented by fishes in a pond.<em/>

If you want to read more about diversity, we recommend to you this [paper](https://link.springer.com/article/10.1007/s00442-010-1812-0) on 
the concept of diversity.

## α diversity  

|-------------------+-----------------------------------------------------------------------------------------------------------------|   
| Diversity Indices |                             Description                                                                         |   
|-------------------+-----------------------------------------------------------------------------------------------------------------|   
|      Shannon (H)  | Estimation of species richness and species evenness. More weight on richness.                                   |   
|-------------------+-----------------------------------------------------------------------------------------------------------------|   
|    Simpson's (D)  |Estimation of species richness and species evenness. More weigth on evenness.                                    |                              
|-------------------+-----------------------------------------------------------------------------------------------------------------|   
|     Chao1         | Abundance based on species represented by a single individual (singletons) and two individuals (doubletons).    |            
|-------------------+-----------------------------------------------------------------------------------------------------------------|   
 

- Shannon (H): 

| Variable             |  Definition   |     
:-------------------------:|:-------------------------:  
$ H = - \sum_{i=1}^{S} p_{i} \ln{p_{i}} $ | Definition
$ S $ | Number of OTUs 
$ p_{i} $ | The proportion of the community represented by OTU i

<!-- <img src="https://render.githubusercontent.com/render/math?math=H=-\sum_{i=1}^{S}p_i\:ln{p_i}"> | Definition
<img src="https://render.githubusercontent.com/render/math?math=S"> | Number of OTUs  
<img src="https://render.githubusercontent.com/render/math?math=p_i">|  The proportion of the community represented by OTU i    -->

- Simpson's (D) 

| Variable             |  Definition |   
:-------------------------:|:-------------------------:  
$ D = \frac{1}{\sum_{i=1}^{S} p_{i}^{2}} $ | Definition
$ S $ | Total number of the species in the community
$ p_{i} $ | Proportion of community represented by OTU i
  
  
<!-- <img src="https://render.githubusercontent.com/render/math?math=D=\frac{1}{\sum_{i=1}^{S}p_i^2}">| Definition   
<img src="https://render.githubusercontent.com/render/math?math=S"> | Total number of the species in the community   
<img src="https://render.githubusercontent.com/render/math?math=p_i" align="middle"> | Proportion of community represented by OTU i     -->
  
- Chao1  

| Variable             |  Definition |   
:-------------------------:|:-------------------------:  
$ S_{chao1} = S_{Obs} + \frac{F_{1} \times (F_{1} - 1)}{2 \times (F_{2} + 1)} $ | Count of singletons and doubletons respectively
$ F_{1}, F_{2} $ | Count of singletons and doubletons respectively
$ S_{chao1}=S_{Obs} $ | The number of observed species
  
  
<!-- <img src="../fig/equation.svg">| Definition  
<img src="https://render.githubusercontent.com/render/math?math=F_1,F_2">|Count of singletons and doubletons respectively    
<img src="https://render.githubusercontent.com/render/math?math=S_{chao1}=S_{Obs}">| The number of observed species   -->

 <!-- comment we use https://viereck.ch/latex-to-svg/ to convert from latex to SVG because Chao equation did not render correctly with GitHub math!-->

### β diversity  
Diversity β measures how different two or more communities are, either in their composition (richness)
or in the abundance of the organisms that compose it (abundance). 
- Bray-Curtis dissimilarity: The difference in richness and abundance across environments (samples). Weight on abundance. Measures the differences 
from 0 (equal communities) to 1 (different communities)
- Jaccard distance: Based on presence/absence of species (diversity). 
It goes from 0 (same species in the community) to 1 (no species in common)
- UniFrac: Measures the phylogenetic distance; how alike the trees in each community are. 
There are two types, without weights (diversity) and with weights (diversity and abundance)  

There are different ways to plot and show the results of such analysis. Among others, PCA, PCoA, or NMDS analysis are widely used.

> ## Exercise 1: 
> In the next picture there are two lakes with different fish species:
> <a href="{{ page.root }}/fig/03-07-01e.png">
>   <img src="{{ page.root }}/fig/03-07-01e.png" alt="In lake A, we have four different species, two of these species have 3 specimens each one. This lake also has two specimens of another species and only one specimen of the other specie. We got nine fish in total. On the other hand, lake B has only three different species, the most populated specie has five specimens and we have only one specimen of the other two species. We got seven species total in lake B " />
> </a>
> Which of the options below is true for the alpha diversity in lake A, lake B, and beta diversity between lakes A and B, respectively?
> 1. 4, 3, 1
> 2. 4, 3, 5
> 3. 9, 7, 16
>
> Please, paste your result on the collaborative document provided by instructors. 
> *Hic Sunt Leones!* (*Here be Lions!*)  
>
>> ## Solution
>> Answer: 4, 3, 5
> {: .solution}
{: .challenge}

## Plot alpha diversity 

We want to know how is the bacterial diversity, so we will prune all of the 
non-bacterial organisms that we have in our `merged_metagenomes` Phyloseq object. To do this we will make a subset 
of all bacterial groups and save them.
~~~
> merged_metagenomes <- subset_taxa(merged_metagenomes, Kingdom == "Bacteria")
~~~
{: .language-r}

Now let's look at some statistics of our metagenomes:

~~~
> merged_metagenomes
~~~
{: .language-r}
~~~
phyloseq-class experiment-level object
otu_table()   OTU Table:         [ 4024 taxa and 3 samples ]
tax_table()   Taxonomy Table:    [ 4024 taxa by 7 taxonomic ranks ]
~~~ 
{: .output}
~~~
> sample_sums(merged_metagenomes)
~~~
{: .language-r}
~~~
  JC1A   JP4D   JP41 
 18412 149590  76589 
~~~ 
{: .output}

~~~
> summary(merged_metagenomes@otu_table@.Data)
~~~
{: .language-r}
~~~
      JC1A              JP4D              JP41        
 Min.   :  0.000   Min.   :   0.00   Min.   :   0.00  
 1st Qu.:  0.000   1st Qu.:   3.00   1st Qu.:   1.00  
 Median :  0.000   Median :   7.00   Median :   5.00  
 Mean   :  4.575   Mean   :  37.17   Mean   :  19.03  
 3rd Qu.:  2.000   3rd Qu.:  21.00   3rd Qu.:  14.00  
 Max.   :399.000   Max.   :6551.00   Max.   :1994.00  
~~~ 
{: .output}

By the output of the `sample_sums()` command we can see how many reads there are
in the library. Also, the Max, Min, and Mean output on `summary()` can give us an
idea of the evenness. Nevertheless, to have a more visual representation of the
diversity inside the samples (i.e. α diversity) we can now look at a 
graph created using Phyloseq:

~~~
> plot_richness(physeq = merged_metagenomes, 
              measures = c("Observed","Chao1","Shannon")) 
~~~
{: .language-r}

<a href="{{ page.root }}/fig/03-07-05.png">
  <img src="{{ page.root }}/fig/03-07-05.png" alt="A figure divided in three 
  sections. Each of these sections represents a different alpha diversity index. 
  Inside this section, each point represents the value assigned on this index to 
  the three different samples. We can see how the different indexes give 
  different values to the same sample." />
</a>
<em> Figure 3. Alpha diversity indexes for both samples. <em/>

Each of these metrics can give an insight into the distribution of the OTUs inside 
our samples. For example, the Chao1 diversity index gives more weight to singletons
and doubletons observed in our samples, while Shannon is an entropy index 
remarking the impossibility of taking two reads out of the metagenome "bag" 
and that these two will belong to the same OTU.


> ## Exercise 2: 
> While using the help provided explore these options available for the function in `plot_richness()`:
> 1. `nrow`
> 2. `sortby`
> 3. `title`
>
> Use these options to generate new figures that show you 
> other ways to present the data.
>
>> ## Solution
>> The code and the plot using the three options will look as follows:
>> The "title" option adds a title to the figure.
>> ~~~
>> > plot_richness(physeq = merged_metagenomes, 
>>              title = "Alpha diversity indexes for both samples in Cuatro Cienegas",
>>              measures = c("Observed","Chao1","Shannon"))
>> ~~~
>> {: .language-r}
>> 
>> <a href="{{ page.root }}/fig//TitleFlag.png">
>> <img src="{{ page.root }}/fig//TitleFlag.png" alt="Alpha diversity indexes for both samples with title" />
>> </a>
>> 
>> The "nrow" option arranges the graphics horizontally.
>> ~~~
>> > plot_richness(physeq = merged_metagenomes, 
>>              title = "Alpha diversity indexes for both samples in Cuatro Cienegas",
>>              measures = c("Observed","Chao1","Shannon"),
>>              nrow=3)
>> ~~~
>> {: .language-r}
>>  
>> <a href="{{ page.root }}/fig//NrowFlag.png">
>> <img src="{{ page.root }}/fig//NrowFlag.png" alt="Alpha diversity indexes for both samples horizontal with title" />
>> </a>
>> 
>> The "sortby" option orders the samples from least to greatest diversity depending on the parameter. In this case, it is ordered by "Shannon" and tells us that the JP4D sample has the lowest diversity and the JP41 sample the highest.
>> ~~~
>> > plot_richness(physeq = merged_metagenomes, 
>>              title = "Alpha diversity indexes for both samples in Cuatro Cienegas",
>>              measures = c("Observed","Chao1","Shannon"),
>>              sortby = "Shannon") 
>> ~~~
>> {: .language-r}
>> 
>> <a href="{{ page.root }}/fig//SortbyFlag.png">
>> <img src="{{ page.root }}/fig//SortbyFlag.png" alt="Alpha diversity indexes for both samples with title sort by Shannon" />
>> </a>
>>
>>
>>  Considering the above mentioned, together with the 3 graphs, we can say that the samples JP41 and JP4D present a high diversity with respect to the JC1A, but that the diversity of the sample JP41 is mainly given by singletons or doubletons, instead, the diversity of JP4D is given by species in much greater abundance. Although because the values of H (Shannon) above 3 are considered to have a lot of diversity.
>> 
>  {: .solution}
{: .challenge}  
  
  
> ## Discussion
>
> How much can the α diversity be changed by eliminating the singletons
> and doubletons?
{: .discussion}
  

## Absolute and relative abundances

From the read counts that we just saw it is evident that there is a great difference in the number of total 
sequenced reads in each sample. Before we further process our data, take a look if we have any 
non-identified reads. Marked as blank (i.e "") on the different taxonomic levels:

~~~
> summary(merged_metagenomes@tax_table@.Data== "")
~~~
{: .language-r}
~~~
  Kingdom          Phylum          Class           Order           Family          Genus          Species       
 Mode :logical   Mode :logical   Mode :logical   Mode :logical   Mode :logical   Mode :logical   Mode :logical  
 FALSE:4024      FALSE:4024      FALSE:3886      FALSE:4015      FALSE:3967      FALSE:3866      FALSE:3540     
                                 TRUE :138       TRUE :9         TRUE :57        TRUE :158       TRUE :484      
~~~
{: .output}
With the command above, we can see that there are blanks on different taxonomic levels. Although we could
expect to see some blanks at the species, or even at the genus level, we will get rid of the ones at 
the genus level to proceed with the analysis:

~~~
> merged_metagenomes <- subset_taxa(merged_metagenomes, Genus != "")
> summary(merged_metagenomes@tax_table@.Data== "")
~~~
{: .language-r}
~~~
  Kingdom          Phylum          Class           Order           Family          Genus          Species       
 Mode :logical   Mode :logical   Mode :logical   Mode :logical   Mode :logical   Mode :logical   Mode :logical  
 FALSE:3866      FALSE:3866      FALSE:3739      FALSE:3860      FALSE:3858      FALSE:3866      FALSE:3527     
                                 TRUE :127       TRUE :6         TRUE :8                         TRUE :339 
~~~
{: .output}


Next, since our metagenomes have different sizes, it is imperative to convert the number 
of assigned reads (i.e. absolute abundance) into percentages (i.e. relative abundances) to be able to compare them. 

Right now our OTU table looks like this:
~~~
> head(merged_metagenomes@otu_table@.Data)
~~~
{: .language-r}
~~~
        JC1A JP4D JP41
1060      32  420   84
1063     316 5733 1212
2033869  135 1232  146
1850250  114  846  538
1061      42 1004  355
265       42  975  205
~~~
{: .output}

To make this transformation to percentages we will take advantage of a function of Phyloseq.
~~~
> percentages <- transform_sample_counts(merged_metagenomes, function(x) x*100 / sum(x) )
> head(percentages@otu_table@.Data)
~~~
{: .language-r}

~~~
             JC1A      JP4D      JP41
1060    0.1877383 0.3065134 0.1179709
1063    1.8539161 4.1839080 1.7021516
2033869 0.7920211 0.8991060 0.2050447
1850250 0.6688178 0.6174056 0.7555755
1061    0.2464066 0.7327130 0.4985675
265     0.2464066 0.7115490 0.2879052
~~~
{: .output}


## Beta diversity

As we mentioned before, the beta diversity is a measure of how alike or different are our samples(overlap between 
discretely defined sets of species or operational taxonomic units).
In order to measure this, we need to calculate an index that suits the objectives of our research. By this code,
we can display all the possible distance metrics that Phyloseq can use:
~~~
> distanceMethodList
~~~
{: .language-r}
~~~
$UniFrac
[1] "unifrac"  "wunifrac"

$DPCoA
[1] "dpcoa"

$JSD
[1] "jsd"

$vegdist
 [1] "manhattan"  "euclidean"  "canberra"   "bray"       "kulczynski" "jaccard"    "gower"     
 [8] "altGower"   "morisita"   "horn"       "mountford"  "raup"       "binomial"   "chao"      
[15] "cao"       

$betadiver
 [1] "w"   "-1"  "c"   "wb"  "r"   "I"   "e"   "t"   "me"  "j"   "sor" "m"   "-2"  "co"  "cc"  "g"  
[17] "-3"  "l"   "19"  "hk"  "rlb" "sim" "gl"  "z"  

$dist
[1] "maximum"   "binary"    "minkowski"

$designdist
[1] "ANY"
~~~
{: .output}
Describing all these possible distance-metrics is beyond the scope 
of this lesson, but here we show which are the ones that need a 
phylogenetic relationship between the species-OTUs present in our samples:

* Unifrac
* Weight-Unifrac
* DPCoA  
  
We do not have a phylogenetic tree or phylogenetic relationships. 
So we can not use any of those three. We will use [Bray-curtis](http://www.pelagicos.net/MARS6300/readings/Bray_&_Curtis_1957.pdf), 
since is one of the most robust and widely use distance metrics to 
calculate beta diversity.

**Let's keep this up!** We already have all that we need to begin the beta diversity analysis. We will use 
the Phyloseq command `ordinate` to generate a new object where the distances between our samples will be 
allocated after they are calculated. For this command, we need to specify which method we will use to generate
a matrix. In this example, we will use Non-Metric Multidimensional Scaling or [NMDS](https://academic.oup.com/bioinformatics/article/21/6/730/199398). NMDS attempts to represent 
the pairwise dissimilarity between objects in a low-dimensional space, in this case, a two-dimensional plot.
~~~
> meta_ord <- ordinate(physeq = percentages, method = "NMDS", 
                     distance = "bray")
~~~
{: .language-r}

If you get some warning messages after running this script, fear not. This is because we only have three samples
, this makes the algorithm display a warning concerning the lack of difficulty in generating the distance 
matrix. 

By now, we just need the command `plot_ordination()`, to see the results from our beta diversity analysis:
~~~
> plot_ordination(physeq = percentages, ordination = meta_ord)
~~~
{: .language-r}  

<a href="{{ page.root }}/fig/03-08-03.png">
  <img src="{{ page.root }}/fig/03-08-03.png" alt="NMDS plot where each of the 
  points represents the combined abundance of all its OTUs. As is depicted,  
  each of the samples occupy its own space in the plot without forming any 
  clusters. This is because each sample is different enough to be considered 
  its own point in the NMDS space." />
</a>
<em> Figure 4. Beta diversity with NMDS of "three" samples. <em/>
  
                             
{% include links.md %}