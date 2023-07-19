# Klebsiella analysis

The assemblies should be in your a directory called `assemblies` on the server.


## checking the quality of assemblies
We can use quast to check the quality of the assemblies. It will do a few things 
1. Calculate common quality metrics such as the N50 
2. Aligns to the reference and checks how much is covered
3. Predicts genes and uses a tool called busco to check how many core house keeping genes are found (should be close to 100%)

```
quast -b assemblies/*.fasta -o quast
```

## Run kleborate

Kleborate can be used to perform in-silico MLST typing to get the strain types. It also performs some basic checks to check the species of Klebsiella and does drug resistance predictions.

```
kleborate --all -a assemblies/*.fasta -o kleborate.txt --kaptive_k_outfile kaptivek.txt --kaptive_o_outfile kaptiveo.txt > kleborate.log
```

## Looking for resistance genes

Abricate uses blast to fund the presence of resistance genes using a database of known sequences.

```
abricate assemblies/*.fasta > abricate_results.txt
```




<script async defer src="https://scripts.simpleanalyticscdn.com/latest.js"></script>
<noscript><img src="https://queue.simpleanalyticscdn.com/noscript.gif" alt="" referrerpolicy="no-referrer-when-downgrade" /></noscript>

