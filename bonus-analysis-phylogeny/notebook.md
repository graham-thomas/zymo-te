# Using MUSCLE on ACE1 gene top 100 BLAST hits from NCBI

http://www.drive5.com/muscle/manual/

Searched ACE1 on NCBI, selected *H. sapien* and ran pblast.
    
    conda install -c bioconda muscle
    conda update muscle
    # create environment and activate
    conda create --name phylogeny muscle
    conda activate phylogeny
    # move data to data dir
    mv ~/Downloads/seqdump.txt data/seqdump.txt
    # Make an alignment and save to a file in FASTA format:
    muscle -in data/seqdump.txt -out seqdump.aligned.fa
    
Install iqtree.

    conda install -c bioconda iqtree

iqtree documentation; http://www.iqtree.org/doc/

Run iqtree with bootsrap 1000.

    iqtree -s seqdump.aligned.fa -B 1000

Install figtree.

    conda install figtree
    conda update figtree

View treefile in figtree.

    figtree seqdump.aligned.fa.treefile



