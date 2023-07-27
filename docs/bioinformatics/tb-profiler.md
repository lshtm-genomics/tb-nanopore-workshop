# TB-profiler

In the previous sessions you have performed mapping, variant calling and annotation to find drug resistance variants in Mtb data. We also looked at the quality of the data through coverage- and depth-based metrics. A lot of commands and manual work were used to get to this final result. To make this process easier we have developed a tool called tb-profiler to automate this process and provide an end-to-end pipeline for TB resistance prediction from sequence data. The pipeline searches for small variants and big deletions associated with drug resistance and will also report the strain type (lineage). 

## Profiling

Let's activate the tb-profiler environment and create a folder for our results:

```
cd ~/data/example_data
mkdir tb-profiler
cd tb-profiler
```

Now we can run tb-profiler using the following command for sample1:

```
tb-profiler profile -1 ../sample1.fastq.gz --platform nanopore --prefix sample1 --txt
```

Let's break down this command:

1. `profile`: this tells the tool to use the profile function, which runs the whole pipeline 
2. `-1 ../sample1.fastq.gz`: used to provide the fastq files
3. `--platform nanopore`: tells the pipeline that we are using ONT data, the default for this parameter is Illumina
4. `--prefix sample1`: this argument allows you to provide a prefix to the resulting output files
5. `--txt`: specified that we want the reuslt file in text format

The results will be put into the results folder. Have a look at the text output using less:

```
less results/sample1.results.txt
```

There are a few sections in the output report:

* Summary: provides a brief summary of the the drug resistance and strain type.
* Resistance report: For each drug lists any variants found and the proportion at which they occured in the raw data. Multiple variants across different genes can arise for the same drug.
* Resistance variants report: similar to the section above but each line represents one variant and more information such as the genome position and variant type is provided.
* Other variants report: lists all variants in drug resistance candidate genes that are not associated with resistance.

!!! question "Exercise"
    Run the profiling for the other samples. Can you see any differences?

## Combining reports

The results from numerous runs can be collated into one table using the following command:

```
tb-profiler collate
```

This will automatically create a number of colled result files from all the individual result files in the result directory. You should now see several files that have been created in your current directory. Open up the main summary file using:

```
libreoffice --calc tbprofiler.txt
```

This will open an open source alternative to excel called libreoffice. When the file is opened you should one line for each sample. The columns give you information about:

* Lineage and sublineage information (strain types)
* QC metrics such as median depth and number of reads mapping
* Number of variants found
* Columns representing the drugs and mutations found

## Customising outputs

By default a .json formatted output file is produced in a directory called results. This file contains information including mutations found, lineage as well as some QC metrics. This format is perfect to load into script for downstream processing but it isn't very human-readable. For a more human-readlable format you can use the --csv and --txt flags to generate outputs in csv and text format too. These files will contain several tables listing similar information to the json format. For advanced users, it is possible to customise this format by providing a template file. It is also possible produce a nice-looking docx formatted report that can be viewed in Word or converted into pdf. The advantage of this is that it can contain images, text formatting, etc. To create this report, a template file must be provided. As with the text custom format, the docx template should have jinja variables defined that will be filled in with sample data when a report is generated. 

First lets download a template:

```
wget https://github.com/jodyphelan/tb-profiler-templates/raw/main/docx/brti_template.docx
```

Now we can use tb-profiler to use fill in this template with the information from sample1:

```
tb-profiler reformat results/sample1.json --docx --docx_template brti_template.docx
```

You should now have a word file called **sample1.results.docx** in your directory. Find and open this file  using the file explorer or open it directly with:

```
libreoffice sample1.results.docx
```

!!! question
    Do you see the same information as with the text report?

!!! question
    Try to modify the original template file (brti_template.docx) and rerun the `tb-profiler reformat` step. Did it work?

!!! question "Exercise"
    Are there any discrepancies between the drug resistance predictions based on WGS from tb-profiler and the phenotypic [DST results](/bioinformatics/data)?

