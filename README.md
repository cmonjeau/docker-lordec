### Lordec description ###

LoRDEC is a program to correct sequencing errors in long reads from 3rd generation sequencing with high error rate, and is especially intended for PacBio reads. It uses a hybrid strategy, meaning that it uses two sets of reads: the reference read set, whose error rate is assumed to be small, and the PacBio read set, which is then corrected using the reference set. Typically, the reference set contains Illumina reads.

### Import the dockerfile ###

git clone https://github.com/cmonjeau/docker-lordec.git

### Build the dockerfile ###

docker build -t cmonjeau/lordec .

### Print Lordec programs help ###

docker run -it --rm cmonjeau/lordec lordec-stat

docker run -it --rm cmonjeau/lordec lordec-correct

docker run -it --rm cmonjeau/lordec lordec-trim

docker run -it --rm cmonjeau/lordec lordec-trim-split

docker run -it --rm cmonjeau/lordec lordec-build-SR-graph

### Run Lordec programs with data (inside /home/user/Lordec directory)

docker run -it --rm cmonjeau/lordec

docker run -it --rm -v /home/user/Lordec:/data cmonjeau/lordec lordec-stat -i /data/pac-10Kl.fa -2 /data/rcc745-10K.fq -k 31 -s 1 -S /data/results/stat_file

docker run -it --rm -v /home/user/Lordec:/data cmonjeau/lordec lordec-correct -i /data/pac-10Kl.fa -2 /data/rcc745-10K.fq -k 31 -s 1 -o /data/results/output_reads.fq

docker run -it --rm -v /home/user/Lordec:/data cmonjeau/lordec lordec-trim -i /data/pac-10Kl.fa -o /data/results/output_trim.fa

docker run -it --rm -v /home/user/Lordec:/data cmonjeau/lordec lordec-trim-split -i /data/pac-10Kl.fa -o /data/results/output_trim.fa

docker run -it --rm -v /home/user/Lordec:/data cmonjeau/lordec lordec-build-SR-graph -2 /data/rcc745-10K.fq -k 31 -s 1 -g /data/results/output_graph

### Run Lordec using Godocker (http://www.genouest.org/godocker/)

Create a new job with these parameters:

"Container image" : cmonjeau/lordec

"Command" :

```

#!/bin/bash

# command line examples (adapt with your data)

lordec-stat -i $GODOCKER_HOME/data/pac-10Kl.fa -2 $GODOCKER_HOME/data/rcc745-10K.fq -k 31 -s 1 -S $GODOCKER_HOME/data/results/stat_file

lordec-correct -i $GODOCKER_HOME/data/pac-10Kl.fa -2 $GODOCKER_HOME/data/rcc745-10K.fq -k 31 -s 1 -o $GODOCKER_HOME/data/results/output_reads.fq

lordec-trim -i $GODOCKER_HOME/data/pac-10Kl.fa -o $GODOCKER_HOME/data/results/output_trim.fa

lordec-trim-split -i $GODOCKER_HOME/data/pac-10Kl.fa -o $GODOCKER_HOME/data/results/output_trim.fa

lordec-build-SR-graph -2 $GODOCKER_HOME/data/rcc745-10K.fq -k 31 -s 1 -g $GODOCKER_HOME/data/results/output_graph


```

"Mount volumes" : home(rw)

