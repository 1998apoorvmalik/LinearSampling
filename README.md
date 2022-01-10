# LazySampling and LinearSampling: Fast Stochastic Sampling of RNA Secondary Structure with Applications to SARS-CoV-2

This repository contains the C++ source code for LazySampling and LinearSampling stochastic sampling algorithms/softwares for RNA secondary structures.

[LazySampling and LinerSampling: Fast Stochastic Sampling of RNA Secondary Structure with Applications to SARS-CoV-2](https://www.biorxiv.org/content/10.1101/2020.12.29.424617v2). bioRxiv 2020.12.29.424617; doi: https://doi.org/10.1101/2020.12.29.424617

He Zhang, Liang Zhang, Sizhen Li, David Mathews, Liang Huang*

\* corresponding authors

Web server: [http://linearfold.org/sampling](http://linearfold.org/sampling)

## Dependencies
gcc 4.8.5 or above; 
python2.7

## To Compile
```
make
```

## To Run
LinearSampling can be run with:
```
echo SEQUENCE | ./linearsampling [OPTIONS]

OR

cat SEQ_OR_FASTA_FILE | ./linearsampling [OPTIONS]
```
Both FASTA format and pure-sequence format are supported for input.

OPTIONS:
```
-k SAMPLE_SIZE
```
The sample size (default 10).
```
--beamsize BEAM_SIZE or -b BEAM_SIZE
```
The beam size (default 100). Use 0 for infinite beam (exact sampling).
```
--fasta
```
Specify that the input is in fasta format. (default FALSE)
```

--verbose
```
Prints out free energy of ensemble, sequence length, sample size and runtime information. (default False)
```
--sharpturn
```
Enable sharpturn. (default False)
```
--non_saving
```
Do not save any hyperedges during sampling, i.e., like RNAsubopt -p 1000. (default False)
```
--readforest FILE_NAME or -f FILE_NAME
```
Read a pre-calculated state forest from file


## Example: Run Predict
```
cat testseq | ./linearsampling -k 5
UGAGUUCUCGAUCUCUAAAAUCG
.(((........)))........
........((((.......))))
.(((........)))........
.(((........)))........
.(((........)))........
AAAACGGUCCUUAUCAGGACCAAACA
.....((((((....)))))).....
.....((((((....)))))).....
.....((((((....)))))).....
.....(((((......))))).....
.....((((((....)))))).....
AUUCUUGCUUCAACAGUGUUUGAACGGAAU
.(((.((..((((......)))).))))).
..(((...(((((......))))).)))..
(((((...(((((......))))).)))))
.(((.((.(((((......)))))))))).
(((((.(.(((((......)))))))))))
UCGGCCACAAACACACAAUCUACUGUUGGUCGA
(((((((.....(((........))))))))))
(((((((.....(((........))))))))))
(((((((...(((..........))))))))))
(((((((.......(((......))))))))))
(((((((...(((..........))))))))))
GUUUUUAUCUUACACACGCUUGUGUAAGAUAGUUA
.....(((((((((((....)))))))))))....
.....(((((((((((....)))))))))))....
....((((((((((((....))))))))))))...
....((((((((((((....))))))))))))...
.....(((((((((((....)))))))))))....

echo GGGCUCGUAGAUCAGCGGUAGAUCGCUUCCUUCGCAAGGAAGCCCUGGGUUCAAAUCCCAGCGAGUCCACCA | ./linearsampling --verbose
GGGCUCGUAGAUCAGCGGUAGAUCGCUUCCUUCGCAAGGAAGCCCUGGGUUCAAAUCCCAGCGAGUCCACCA
Partition Function Time: 0.00572 secs
Free Energy of Ensemble: -32.14 kcal/mol
(((((((..(((((....).))))((((((((...)))))))).(((((.......))))))))))))....
(((((((..((((.......))))((((((((...)))))))).(((((.......))))))))))))....
(((((((..((((.......))))(((((((.....))))))).(((((.......))))))))))))....
(((((((..((((.......))))((((((((...)))))))).(((((.......))))))))))))....
((((((((.((((.......))))((((((((...))))))))..((((.......))))))))))))....
(((((((..((((.......))))((((((((...)))))))).(((((.......))))))))))))....
(((((((..((((.......))))((((((((...)))))))).(((((.......))))))))))))....
(((((((..((((.......))))((((((((...)))))))).(((((.......))))))))))))....
((((((((.((((.......))))((((((((...))))))))..((((.......))))))))))))....
((((((((.((((.......))))((((((((...))))))))..((((.......))))))))))))....
Sequence_length: 72 recover time: 0.000000 secs Sample Number: 10 Sample Time: 0.000186 secs  uniq_nodes: 40 (11.33% of visits, 0.63% of all nodes)
Total Time: 0.008407 secs
```

## Example: Load A Pre-calculated State Forest
```
./linearsampling -f dumpforest_example
GUUUUUAUCUUACACACGCUUGUGUAAGAUAGUUA
forest of 89 nodes loaded in 0.0 secs.
.....((((((((((......))))))))))....
.....(((((((((((....)))))))))))....
.......(((((((((....))))))))..)....
.....(((((((((((....)))))))))))....
....((((((((((((....))))))))))))...
.....(((((((((((....)))))))))))....
(.((..((((((((((....)))))))))))).).
....((((((((((((....))))))))))))...
....((((((((((((....))))))))))))...
....((((((((((((....))))))))))))...
```

## Data
We list two sequences from RNAcentral that show the overflow issue of RNAsubopt.
The ID and description of the sequences are:

URS00007C400D lncRNA from 10 species

URS00009C28A8_9606 Homo sapiens long non-coding RNA NONHSAT136811.2

Please also find the sequences in data/ folder.
