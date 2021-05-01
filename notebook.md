# Methods from paper
- download zymoseptoria genome and annotation files.
- Repeats were identified de novo using RECON and RepeatScout.
- The output from these two programs was used to generate custom repeat libraries, which were subsequently used to mask the *M. graminicola* genome using RepeatMasker. 
- Manually curated repeats specific to fungi were obtained from RepBase Update. 
- Repeats were also identified using another k-mer approach, TALLYMER.
- Frequencies of repetitive sequences were plotted along the chromosomes using Gnuplot.

## Download RECON source code to local host

    cd ~/src/
    wget http://eddylab.org/software/recon/RECON1.05.tar.gz
    tar -xzvf RECON1.05.tar.gz

## Run through demo
Update perl script with path to binaries.
- issue encountered; bin/ directory empty. Have emailed developer for assistance.

Same as below, have discovered I can install recon through conda/mamba


## Download RepeatScout
from https://github.com/mmcco/RepeatScout/blob/master/README
Installation requirements;
already have perl-5.5 or better
Downloaded nseg to ~/src/ from ftp://ftp.ncbi.nih.gov/pub/seg/nseg/ on 2021-04-30
Downloaded trf.v4.09 to ~/src/ from https://tandem.bu.edu/trf/trf.download.html on 2021-04-30
**states** *download the source code tarball RepeatScout-#.#.#.tar.gz 
     from http://repeatscout.bioprojects.org however the web address no longer exists*

## RepeatScout - Work around
RepeatScout is available as a bioconda package
    
    conda install -c bioconda repeatscout
    conda create --name=repeatscout repeatscout
    conda activate repeatscout

installed dependencies so  removed nseg and trf from ~/src/

Found good implementation guide at https://openwetware.org/wiki/Wikiomics:Repeat_finding
run
    
    cd /zymo-te/analysis/
    conda activate repeatscout
    build_lmer_table -sequence ../data/seqs/zymoseptoria_tritici/Zymoseptoria_tritici.MG2.dna.toplevel.fa -freq output_lmer.frequency
    RepeatScout -sequence ../data/seqs/zymoseptoria_tritici/Zymoseptoria_tritici.MG2.dna.toplevel.fa -output output_repeats.fas  -freq output_lmer.frequency

## Download RepeatMasker
https://www.repeatmasker.org/RepeatMasker/
This webpage shows prerequisites;

    - Unix system with perl 5.8.0 or higher installed
    - Python 3 and the h5py python library.
    - Sequence Search Engine
    RepeatMasker uses a sequence search engine to perform it's search for repeats. Currently Cross_Match, RMBlast and WUBlast/ABBlast are supported. You will need to obtain one or the other of these and install them on your system.

        - For Cross_Match go to http://www.phrap.org You will want to select "Phred/Phrap/Consed" as Cross_Match is part of the Phrap package.
        - For RMBlast ( NCBI Blast modified for use with RepeatMasker/RepeatModeler ) please go to our download page: http://www.repeatmasker.org/RMBlast.html
        - For HMMER please download the v3.2.1 version here: http://hmmer.org/
        - For ABBlast/WUBlast go to [ NOTE: Rights to BLAST 2.0 (WU-BLAST) have been acquired by Advanced Biocomputing, LLC. http://blast.advbiocomp.com/licensing/ RepeatMasker 3.2.8 and above fully support both variants ]

    - TRF - Tandem Repeat Finder, G. Benson et al.
You can obtain a free copy at http://tandem.bu.edu/trf/trf.html. RepeatMasker was developed using TRF version 4.0.9

    - Repeat Database
RepeatMasker can be used with custom libraries, or with Dfam out of the box. Dfam is an open database of transposable element (TE) profile HMM models and consensus sequences. The current release (Dfam 3.2) contains 6,900 TE families spanning five organisms: human, mouse, zebrafish, fruit fly, nematode, and a growing number of additional species. To supplement this databases we recommend obtaining the RepeatMasker edition of RepBase.
To update the Dfam libraries contained in this release go to http://www.dfam.org.

Have requested license for phrap. Two week turn around.
Downloaded hmmer.v3.3.2 to ~/src/ from http://hmmer.org/ on 2021-04-30
Downloaded rmblast.v2.11.0 to ~/src/ from http://www.repeatmasker.org/RMBlast.html on 2021-04-30
Tried downloading repbase however, requires subscription fee even for individual academics.

    University of Exeter not registered.
    
Downloaded RepeatMasker-4.1.2-p1 to ~/src/ from https://www.repeatmasker.org/RepeatMasker/ on 2021-04-30 

Have since learned conda/mamba package managers are better tools for the job

    mamba create --name=repeatmasker repeatmasker
therefore remove previously installed dependencies from ~/src/