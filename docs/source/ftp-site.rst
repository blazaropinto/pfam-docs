.. _ftp-site:

********
FTP Site
********

The Pfam `FTP site <ftp://ftp.ebi.ac.uk/pub/databases/Pfam>`_ is organised into the following structure: 

.. figure:: images/ftp-structure.png
    :width: 200
    :align: center

The most important directory is probably the current_release directory. This contains the flat-files for the current release. Some of these files may be very large (of the order of several hundred megabytes). Please check the sizes on the FTP site before trying to download them over a slow connection. The files, most of which are compressed using gzip, are:

`Pfam-A.dead.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.dead.gz>`_
    Listing of families that have been deleted from the database 
`Pfam-A.fasta.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.fasta.gz>`_
    A 90% non-redundant set of fasta formatted sequence for each Pfam-A family. The sequences are only the regions hit by the model and not full length protein sequences. 
`Pfam-A.full.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.full.gz>`_
    The full alignments of the curated families, searched against pfamseq/UniProtKB reference proteomes (prior to Pfam 29.0, this file contained matches against the whole of UniProtKB). 
`Pfam-A.full.uniprot.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.full.uniprot.gz>`_
    The full alignments of the curated families, searched against UniProtKB. 
`Pfam-A.full.metagenomics.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.full.metagenomics.gz>`_
    The full alignments of the curated families, searched against Metagenomic proteins. 
`Pfam-A.full.ncbi.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.full.ncbi.gz>`_
    The full alignments of the curated families, searched against NCBI GenPept proteins. 
`Pfam-A.hmm.dat.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.hmm.dat.gz>`_
    A data file that contains information about each Pfam-A family 
`Pfam-A.hmm.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.hmm.gz>`_
    The Pfam HMM library for Pfam-A families 
`Pfam-A.seed.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.seed.gz>`_
    The seed alignments of the curated families 
`Pfam-C.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-C.gz>`_
    A file that contains the information about clans and the Pfam-A membership 
`active_site.dat.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/active_site.dat.gz>`_
    Tar-ball of data required for the predictions of active sites by Pfam scan. 
`database.tar <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/database.tar>`_
    A tar-ball of the database_files directory. 
`database_files <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/database_files>`_
    Directory contains two files per table from the MySQL database. The .sql.gz file contains the table structure, the .txt.gz files contains the content of the table as a tab delimited file with field enclosed by a single quote ('). 
`diff.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/diff.gz>`_
    Stores the change status of entries between this release and last. 
`md5_checksums <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/md5_checksums>`_
    A file containing the MD5 checksum for each release file
`metaseq.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/metaseq.gz>`_
    Metagenomic sequence database used in this release 
`ncbi.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/ncbi.gz>`_
    NCBI GenPept sequence database used in this release. 
`pdbmap.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/pdbmap.gz>`_
    Mapping between PDB structures and Pfam domains. 
`pfamseq.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/pfamseq.gz>`_
    A fasta version of Pfam's underlying sequence database 
`relnotes.txt <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/relnotes.txt>`_
    Release notes 
`swisspfam.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/swisspfam.gz>`_
    ASCII representation of the domain structure of UniProt proteins according to Pfam 
`uniprot_sprot.dat.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/uniprot_sprot.dat.gz>`_
    Data files from UniProt containing SwissProt annotations. 
`uniprot_trembl.dat.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/uniprot_trembl.dat.gz>`_
    Data files from UniProt containing TrEMBL annotations. 
`userman.txt <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/userman.txt>`_
    File containing information about the flatfile format 
`Pfam-A.regions.tsv.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.regions.tsv.gz>`_
    A tab separated file containing UniProtKB reference proteome sequences and Pfam-A family information 
`Pfam-A.regions.uniprot.tsv.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.regions.uniprot.tsv.gz>`_
   A tab separated file containing UniProtKB sequences and Pfam-A family information
`Pfam-A.clans.tsv.gz <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/current_release/Pfam-A.clans.tsv.gz>`_
    A tab separated file containing Pfam-A family and clan information for all Pfam-A families 

The **papers** directory contains each NAR database issue article describing Pfam. For a detailed description of the latest changes to Pfam, please consult (and cite) these papers.

The **releases** directory contains all the flat files and database dumps (where appropriate) for all version of Pfam to-date. The files in more recent releases are the same as described for the current release, but in older releases the contents do change.

The **Tools** directory contains code for running pfam_scan.pl. The README file in this directory contains detailed information on how to install and run the script. Note that we have gone for a modular design for the script, enabling the functionally on the script to be easily incorporated into other Perl scripts. The ChangeLog file lists the versions and changes to the current version of pfam_scan.pl (and modules). There is also an archived version of pfam_scan.pl that works with HMMER2. This is no longer supported. There is also Perl code for predicting active sites found in the ActSitePred directory, the functionality of which has been rolled into the latest version of pfam_scan.pl

The top level directory contains the **sitesearch** folder, that contain a subset of information from Pfam in an XML file. This XML file, primarily for use by the EMBL-EBI Web Team, is indexed using lucene and used in the EMBL-EBI site search. This is updated at each release. 
