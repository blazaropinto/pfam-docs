.. _getting-started:

***************
Getting Started
***************

Site organisation
=================

.. figure:: images/family.png
    :width: 400
    :align: center

The **family** page is the major page for accessing information contained within Pfam as it describes the Pfam family entries. Most referring sites link to this page. Alternatively, users can navigate to family pages by entering the Pfam identifier or accession number, either via the home page, the "Jump-to" boxes or the keyword search box, or by clicking on a domain name or graphic from anywhere on the website. As with all Pfam pages, there is the context-sensitive icon bar in the top right hand corner that provides a quick overview about the contents of the tabs. The tabs on the family page cover the following topics: functional annotation; domain organisation or architectures; alignments; HMM logo; trees; curation and models; species distribution; interactions; and structures.

Using the "Jump to" search
==========================


.. figure:: images/jumpTo.gif
    :width: 100
    :align: left

Many pages in the site include a small search box, entitled "Jump to...". The "Jump to..." box allows you to go immediately to the page for any entry in the Pfam site entry, including Pfam families, clans and UniProt sequence entries.

The "Jump to..." search understands accessions and IDs for most types of entry. For example, you can enter either a Pfam family accession, e.g. PF02171, or, if you find it easier to remember, a family ID, such as piwi. Note that the search is case insensitive.

Because some identifiers can be ambiguous, the "Jump to..." search may need to test several types of identifier to find the entry that you're looking for. For example, Pfam A family IDs (e.g. Kazal_1) and Pfam clan IDs (e.g. Kazal) aren't easily distinguished, so if you enter kazal, the search will first look for a family called kazal and, if it doesn't find one, will then look for a clan called kazal. If all of the guesses fail, you'll see an error message saying "Entry not found".

The order in which the search tries the various types of ID and accession is given below:

    * Pfam A accession, e.g. PF02171
    * Pfam A identifier, e.g. piwi
    * UniProt sequence ID, e.g. CANX_CHICK
    * NCBI "GI" number, e.g. 113594566
    * NCBI secondary accession, e.g. BAF18440.1
    * Pfam clan accession, e.g. CL0005
    * metaseq ID, e.g. JCVI_ORF_1096665732460
    * metaseq accession, e.g. JCVI_PEP_1096665732461
    * Pfam clan accession, e.g. CL0005
    * Pfam clan ID, e.g. Kazal
    * PDB entry, e.g. 2abl
    * Proteome species name, e.g. Homo sapiens

Keyword search
==============

.. figure:: images/kwSearch.gif
    :width: 100
    :align: left

Every page in the Pfam site includes a search box in the page header. You can use this to find Pfam-A families which match a particular keyword. The search includes several different areas of the Pfam database:

    * text fields in Pfam entries, e.g. family descriptions
    * UniProt sequence entry description and species fields
    * HEADER and TITLE fields from PDB entries
    * Gene Ontology IDs and terms
    * InterPro entry abstracts

Each Pfam-A entry is listed only once in the results table, although it might have been found in more than one area of the database.

Searching a protein sequence against Pfam
=========================================

Searching a protein sequence against the Pfam library of HMMs will enable you to find out the domain architecture of the protein. If your protein is present in the version of UniProt, NCBI Genpept or the metagenomic sequence set that we used to make the current release of Pfam, we have already calculated its domain architecture. You can access this by entering the sequence accession or ID in the 'view a sequence' box on the Pfam homepage.

If your sequence is not in the Pfam database, you could perform a single-sequence or a batch search by clicking on the 'Search' link at the top of the Pfam page.

Single protein search
---------------------

If your protein is not recognised by Pfam, you will need to paste the protein sequence into the search page. We will search your sequence against our HMMs and instantly display the matches for you.

Batch search
------------

If you have a large number of sequences to search (up to several thousand), you can use our batch upload facility. This allows you to upload a file of your sequences in FASTA format, and we will run them against our HMMs and email the results back to you, usually within 48 hours. We request that you put a maximum of 5000 sequences in each file.

Local protein searches
----------------------

If you have a very large number of protein searches to perform, or you do not wish to post your sequence across the web, it may be more convenient to run the Pfam searches locally using the 'pfam_scan.pl' script. To do this you will need the HMMER3 software, the Pfam HMM libraries and a couple of additional data files from the Pfam website. You will also need to download a few modules from CPAN, most notably Moose.

Full details on how to get 'pfam_scan.pl' up and running can be found on our `FTP site <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/Tools/README>`_.

Proteome analysis
-----------------

Pfam pre-calculates the domain compositions and architectures `UniprotKB reference proteomes <https://www.uniprot.org/help/reference_proteome>`_. To see the list of proteomes, click on the 'browse' link at the top of the Pfam website, and click on a letter of the alphabet in the 'proteomes' section. By clicking on a particular organism, you will be be able to view the proteome page for that organism. From here you can view the domain organisation and the domain composition for that proteome.

The taxonomy query allows quick identification of families/domains which are present in one species but are absent from another. It can also be used to find families/domains that are unique to a particular species (note this can be very slow).

Finding proteins with a specific set of domain combinations ('architectures')
=============================================================================

For a detailed study of domain architectures you can use `PfamAlyzer <http://pfam.xfam.org/search?tab=searchDomainBlock>`_. PfamAlyzer allows you to find proteins which contain a specific combination of domains and to specify particular species and the evolutionary distances allowed between domains.

Wikipedia annotation
====================

The Pfam consortium is now coordinating the annotation of Pfam families via Wikipedia. On the summary tab of some family pages, you'll find the text from a Wikipedia article that we feel provides a good description of the Pfam family. If a family has a Wikipedia article assigned to it, we now show the text of that article on the summary tab, in preference to the traditional Pfam annotation text.

If a family does not yet have a Wikipedia article assigned to it, there are several ways for you to help us add one. You can find much more information about the process in the :ref:`wikipedia` section. 

