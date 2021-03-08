# Tabs generation
Tabs are dynamically generated from the output. After uploading a single file the only tab available is "Annotation visualization and comparison". After uploading more two more tabs are generated :
1. "Biocircos plot"
2. "Summarize interception"

The default data choice for all dropdown selection menus is the first uploaded. 

The "Compare to DeepBGC" tab is available after DeepBGC data upload and if the more than one data was uploaded. (For example DeepBGC and Antismash).  

**Note: Comparison of DeepBGC data is available only to PRiSM, SEMPI or Antismash. So, if, for example, DeepBGC and RRE-Finder data was uploaded, the tab will be available, but plots will not be rendered**

# Data upload and manipulation
Data upload is done with the corresponding file upload menus. Detailed description of the input files is [here](Input_files_options.md). 

![upload_menu](/images/data_upload.png)

After the files are uploaded data will be extracted and added to the plots. It is possible, that a short period of unresponsiveness of BGCViz occurs after data upload. This indicates that data is being processed and plots are being rerendered. The longest period of unresponsiveness occurs after PRISM json file upload. It can last up to 3 min. 

**The supplementary PRISM data is available if the uploaded data was a json report, generated by the service. To include resistance and regulatory genes, identified by PRISM into the analysis, please tick the corresponding checkbox  in "Data manipulation options" menu**

**Note: Please use the right sequence length. It is crucial in rendering Biocircos plots. Rule of thumb: It is  better to input bigger length of a chromosome, than smaller. If the bigger length is used, then then just some gaps in the chromosomes on a circos plots can be spotted., otherwise, if the input length is smaller, then all the arcs and links will be shifted clockwise and the whole biocircos plot will have no sense. Default length is 10,000,000 bp**

The "Data manipulation options" menu option contains:
- Rename BGC with several products in the Antismash data to "hybrid"
- Rename BGC with several products in the PRISM data to "hybrid"
- Rename BGC with several products in the SEMPI data to "hybrid"
- Use PRISM additional data, which includes resistance and regulatory genes
- Chose ARTS core genes to plot

![data_mani](/images/data_mani.png)

The renaming options are used for better link and arcs coloring in the biocircos plot. PRISM additional data option adds the resistance and regulatory genes as a separate data input to the plots.

ARTS data controls are used for better understanding of the core genes duplication. If the ARTS core gene is intercepted with other BGC, then the one can plot only this core gene paralog to see the location of the duplicated gene and if it is intercepted with other clusters. **Note: ARTS core gene duplication data can have more than two genes. Therefore all paralogs will be visualized**. 


# Compare data with DeepBGC
This tab is generated after the upload of DeepBGC data if this data was not the only input. The tab consists of two plots and delivers a purpose to compare DeepBGC data with several filters to the chosen reference one. After the comparison, one can choose the optimal threshold of DeepBGC data, preserving the balance between novel and already annotated clusters. The choice between reference annotation for comparison is Antismash, SEMPI and PRISM.
The first plot in this tab visualizes several clusters, which are annotated solely by DeepBGC, only by chosen reference program, or by both.

![deep_da](/images/deep_anti_comp.png)

On the x-axis, there are different thresholds for a chosen DeepBGC score, on the y-axis - number of clusters (divided into three groups, described above), which are preserved on a given score threshold. Any additional thresholds can be also applied to this plot and will be written on the upper right corner 

The second plot can be thought of as a mirror of the first one. It contains the same data, but in form of rate, in place of counts.

![deep_rates](/images/deep_anti_rates.png)

The rates are:

- Novelty rate = "# of BGC annotated only by deepbgc"/("# clusters annotated with only by antismash" + "# clusters annotated with antismash and deepbgc"). This rate points to how many clusters are annotated only by DeepBGC.

- Annotation rate = "# of BGC annotated by antismash and deepbgc"/"total number of antismash annotated BGC". This rate points to how much DeepBGC annotated clusters alongside with antismash. 

- Skip rate = "# of BGC annotated only by antismash"/"total number of antismash clusters". This rate points of how many clusters DeepBGC missed, assuming, that antismash is a reference annotation 

All the data cleaning is used with the help of the sliders. The main data cleaning menu option looks like this:

![deep_filters](/images/deepbgc_filters.png)

The thresholds here are applied globally to all plots and the data cleaning options for DeepBGC are the columns of the .tsv output file, which are quite descriptive by themselves.

The second group of plot controls affect only the first barplot. They include:
- Choice of reference data (between SEMPI, PRISM and Antismash)
- Choice of the score, to be plotted on the x-axis. 
- Choice of a step for a barplot. 
- Choice of the starting point of a barplot

![deep_cpm](/images/deep_comparison.png)

**Tip: you can hide all not used controls with the "Hide..." checkbox**

# Annotation visualization and comparison
The plots on this tab can be thought to be "Genes on chromosome". Here are two plots available:
- The general "Genes on chromosome" plots, which contain all the annotations from all tools. On mouse hover over BGC, information, particular to the chosen tool, is shown.

![all_annot](/images/all_annotations.png)

-  The second plot visualizes the data from uploaded apps, which is intercepted to the app of a choice. Default reference app is the first uploaded and all the clusters are plotted for it.
**Note: if there is no interception available between the uploaded apps and reference one, then this plot will remain empty. The good example is the choice of SEMPI data as a reference. Then the RRE-Finder data is absent from the plot (usually) because no interceptions are made between them **

![anot_inter](/images/intercepted_annotations.png)

The second plot has pretty simple controls, which consist of only one option -> the choice of reference data.

![genes_on_chr](/images/genes_on_chromosome.png)

The type, which is used to color the BGCs, is a subject of change through renaming and combining data as hybrids. More is [here](BGCViz_renaming_and_coloring_options.md)

**These visualisations are also affected by renaming, improve visualization options and data manipulation options**

# Biocircos plot
The biocircos tab is become available after uploading two or more datasets. By default, the links (lines that connect different chromosomes) and arcs (the boxes under the chromosomes, that corresponds to the BGC) are grey. This plot is also affected by the chromosome length, which is a mandatory input. 
- The first plot is a circos plot. It is reactive, which means, the one can make it bigger or smaller with the help of mouse wheel scroll. 

![biocircos](/images/biocircos.png)

On the cursor hover onto a link, the cluster IDs and their types will be shown, as well as, linked software names. The type here is unaffected by renaming and is shown as is. On the cursor hover onto arcs, the type of the cluster and their coordinates is shown.

- The second plot is just a legend for applied colors for biocircos plot. These are a subject to change through [coloring dataframe](BGCViz_renaming_and_coloring_options.md). At default, all data is visualized in grey color.

![biocircos_legend](/images/biocircos_legend.png)

The controls of biocircos plots are under improve visualization menu

![color_biocircos](/images/improve_viz.png)

After uploading data, these are available right away, however, there is small use in them prior to renaming. The coloring is based on the groups, which are stated in a legend. If the no color is specified for a chosen BGC type, then the base color is used. Therefore before renaming, when the coloring options are ticked, the majority of the links and arcs will remain grey.

The coloring options for the links includes three modes. These modes illustrate different logic of dealing with the linking clusters of different types (because one color for a single link must be specified). The modes of coloring:
1. Hierarchical-based -> the colors are assigned based on the tool hierarchy. The hierarchy is specified in the coloring dataframe (more is [here](BGCViz_renaming_and_coloring_options.md)).If the link connects two clusters with different types, then the color will be assigned based on the BGC type of the higher in the hierarchy tool. Example: Link joining the pks cluster from Antismash and ripp cluster from RRE-Finder. Then the link will be colored as a pks one because Antismash is the first in the hierarchy.
2. Purity-based -> colors only the links, which connects BGCs with the same type. All other links are colored with the base color. Example: the link connecting pks from Antismash and ripp from RRE-Finder will be colored as grey (base color). The link, connecting the same Antismash cluster with the pks one from PRISM, will be colored in corresponding to the legend color (as the types are the same).
3. Reference column-based -> one should choose the reference data. Then all the links, which connects the chosen data with other ones,  will be colored according to other data types. All other links, which do not connect the chosen data BGCs, are colored with the base color. Example: Antismash is chosen as reference data. Then the link from RRE-Finder ripp cluster to the Antismash pks one will be colored according to the ripp color. The link from the same RRE-Finder ripp cluster to the DeepBGC pks one will be colored in base color because it is not connections any BGCs from Antismash. **This mode is useful for a diversity of BGC types analysis within one app annotation data. It allows quick visual comparison between arcs color (the type in reference data) and the link color (which types are annotated for the same cluster)**

**The abovementioned coloring modes are used only for link coloring. Arc colors remain unchanged and correspond to the BGC type of the data they belong to**

# Summarize interception
This tab is being shown after more than two datasets are uploaded.  To logic behind this tab is to summarize the links between different BGCs. To support than purpose a barplot and a table is generated:
1. Barplot, which counts to how much other BGCs the chosen one is linked. On the x-axis, the BGCs are plotted and on the y-axis the link count. This plot is useful for basic prioritization of BGCsm which are annotated by a chosen app.

![summarize](/images/summarize_plot.png)

2. "Group by" table. This table shows the intercepted clusters of a chosen data with the other tools. Therefore this table is similar to the second plot on the  Annotation visualization and comparison tab, but the data is in form of a table.

![group_by_t](/images/group_by_table.png)

The options for data summary includes:
- Option to choose the program, by which the interception will be summarized. 
- Checkbox to visualize all the BGC for a chosen data. By default, only BGC, which are intercepted with any other ones are printed in the first column of the table. But if the purpose of analysis in to emphasise the  BGCs, that are only found by the chosen tool, then all the clusters will be printed, if the checkbox is ticked.

![summarize_opt](/images/summarize_options.png)

**Note: The second plot on the "Annotation visualization and comparison" tab is similar to this table. They can be used interchangeably.**

# Improve vizualization options
These options are dynamically updated upon different data types upload. They include:
- Add thickness to RRE-Finder results
- Add thickness to PRISM results (regulatory and resistance genes)
- Add thickness to ARTS results 
- Coloring option for biocircos, which are described above

The rationale behind adding the thickness is that arcs on biocircos plot and genes in the "Annotation visualization and comparison" tab plots for these results are roughly visible. These options are just adding some length to the results, therefore making them visible. These options DO NOT affect the interception results.