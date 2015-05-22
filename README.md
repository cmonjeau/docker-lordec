### Lordec description ###

LoRDEC is a program to correct sequencing errors in long reads from 3rd generation sequencing with high error rate, and is especially intended for PacBio reads. It uses a hybrid strategy, meaning that it uses two sets of reads: the reference read set, whose error rate is assumed to be small, and the PacBio read set, which is then corrected using the reference set. Typically, the reference set contains Illumina reads.

### Import the dockerfile ###

git clone https://github.com/cmonjeau/docker-lordec.git

### Build the dockerfile ###

docker build -t cmonjeau/takeabreak .

### Print Lordec programs help ###

docker run -it --rm cmonjeau/takeabreak lordec-stat
docker run -it --rm cmonjeau/takeabreak	lordec-correct
docker run -it --rm cmonjeau/takeabreak	lordec-trim
docker run -it --rm cmonjeau/takeabreak	lordec-trim-split
docker run -it --rm cmonjeau/takeabreak	lordec-build-SR-graph

### Run Lordec programs with data (inside /home/user/Lordec directory)

docker run -it --rm cmonjeau/lordec
docker run -it --rm -v /home/user/Lordec:/data cmonjeau/lordec lordec-stat -i /data/pac-10Kl.fa -2 /data/rcc745-10K.fq -k 31 -s 1 -S /data/results/stat_file
docker run -it --rm -v /home/user/Lordec:/data cmonjeau/lordec lordec-correct -i /data/pac-10Kl.fa -2 /data/rcc745-10K.fq -k 31 -s 1 -o /data/results/output_reads.fq
docker run -it --rm -v /home/user/Lordec:/data cmonjeau/lordec lordec-trim -i /data/pac-10Kl.fa -o /data/results/output_trim.fa
docker run -it --rm -v /home/user/Lordec:/data cmonjeau/lordec lordec-trim-split -i /data/pac-10Kl.fa -o /data/results/output_trim.fa
docker run -it --rm -v /home/user/Lordec:/data cmonjeau/lordec lordec-build-SR-graph -2 /data/rcc745-10K.fq -k 31 -s 1 -g /data/results/output_graph

