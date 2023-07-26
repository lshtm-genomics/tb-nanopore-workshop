# Variant calling Oxford Nanopore sequencing data

## Intended learning outcomes

This practical session goes into how to perform variant calling on long-read sequencing data from ONT:

1. Learn the concepts behind variant calling
2. ONT data specific tools for variant calling
3. Visualising variants in genomic contexts 

## Background

Variants in genomic data refer to differences in the sequence of DNA or RNA between individuals or between a sample and a reference genome. These differences can manifest as single nucleotide polymorphisms (SNPs), insertions, deletions, or more complex structural variations. Given that you're familiar with sequencing technologies and mapping, let's delve straight into the concept of variant calling, emphasizing its application in Oxford Nanopore sequencing data.

### Variant Calling: A Bird’s-Eye View
Once you've sequenced your DNA sample and mapped the reads onto a reference genome, the next step is to identify where your sample differs from this reference. This process is known as variant calling. Conceptually, it's like comparing two texts and highlighting where they differ. In this genomic context, these differences — or variants — can be tiny, like a single changed letter (a SNP), or larger, like a whole sentence being added or removed (an insertion or deletion).

### Challenges with Oxford Nanopore Sequencing
Oxford Nanopore Technologies (ONT) provides a unique sequencing approach, producing long reads that can span thousands to tens of thousands of bases. This is a game-changer for detecting structural variants and sequencing challenging regions of the genome. However, there's a catch: these long reads come with a higher error rate compared to other sequencing technologies.

The errors introduced during ONT sequencing can be substitutions, insertions, or deletions. This can make variant calling more challenging because we need to differentiate between genuine variants and errors introduced by the sequencing process.

### Preventing False Variants: Strategies to Remember
Given the error-prone nature of Oxford Nanopore sequencing, strategies have been developed to distinguish real variants from sequencing errors:

1. Depth of Coverage: One of the simplest ways to differentiate between true variants and errors is by looking at the depth of coverage. A genuine variant will typically be observed in multiple reads covering the same position, while a sequencing error might only appear in one or a few reads. Sometime we set a hard cut-off, where for example, 70% of the bases at a position would have to support a variant call.

2. Statistical Modeling: Many modern variant callers employ statistical models to evaluate the likelihood that a detected variant is real. These models consider various factors, such as the quality score of the bases in the reads, the depth of coverage, and the expected error rate of the sequencing technology.

3. Using a Combination of Sequencing Technologies: If resources allow, combining the long-read data from ONT with short-read data from platforms like Illumina can provide a more comprehensive and accurate variant landscape. The short-read data, with its lower error rate, can validate variants detected by the long reads. This is called hybrid sequencing analysis, which is very powerful when both long-reads and high-fidelity is required.

4. Repeat & Validate: Especially for critical findings, consider re-sequencing the sample or using a different method (like PCR followed by Sanger sequencing) to validate the identified variants.

### In Conclusion
Variant calling in Oxford Nanopore sequencing data poses unique challenges due to its error-prone nature. But with careful data processing, the use of specialized tools designed for long reads, and strategies to discern real variants from errors, researchers can extract valuable genetic insights from their samples. As with any genomic analysis, it's always a good practice to stay updated with the latest tools and methodologies, and always cross-check critical results for the highest accuracy.