.. _faq:

*********************************
Frequently Asked Questions (FAQs)
*********************************

.. contents::
  :local:

What is Pfam?
=============

Pfam is a collection of multiple sequence alignments and profile hidden Markov models (HMMs). Each Pfam profile HMM represents a protein family or domain. By searching a protein sequence against the Pfam library of profile HMMs, you can determine which domains it carries i.e. its domain architecture. Pfam can also be used to analyse proteomes and questions of more complex domain architectures.

For each Pfam accession we have a family page, which can be accessed in several ways: from the 'View a Pfam Family' search box on the HOME page, by clicking on any graphical image of a domain, by searching for a particular family using the 'Keyword Search' box on the top right hand corner of most website pages, or by pasting the family identifier or accession into the 'JUMP TO' box that is present on most pages in the site.

What is on a family page?
=========================

From the family page you can view the Pfam annotation for a family. We also provide access to many other sources of information, including annotation from the InterPro database, where available, cross-links to other databases and other tools for protein analysis. Since release 25.0 we have also started displaying relevant articles from `Wikipedia <https://en.wikipedia.org/wiki/Main_Page>`_ where available.


Via the tabs on the left-hand side of the page, you can view:

    * the domain architectures in which this family is found
    * the alignments for the family in various formats, including alignments of matches to UniProKB and representative proteomes, as well as in 'heat-map' format. All alignments can be downloaded
    * the phylogenetic and species distribution trees, either as a traditional, interactive tree or as a "sunburst" plot
    * the profile HMM logo
    * the structural information for each family where available

What is a clan?
===============

Some of the Pfam families are grouped into clans. Pfam defines a clan as a collection of families that have arisen from a single evolutionary origin. Evidence of their evolutionary relationship can be in the form of similarity in tertiary structures, or, when structures are not available, from common sequence motifs. The seed alignments for all families within a clan are aligned and the resulting alignment (called the clan alignment) can be accessed from a link on the clan page. Each clan page includes a clan alignment, a description of the clan and database links, where appropriate. The clan pages can be accessed by following a link from the family page, or alternatively they can be accessed by clicking on 'clans' under the 'browse' by menu on the top of any Pfam page.

What criteria do you use for putting families into clans?
=========================================================

We use a variety of measures. Where possible we do use structures to guide us and that is always the gold standard. In the absence of a structure we use:

  * profile comparisons such as HHsearch
  * the fact that a sequence significantly matches two profile HMMs in the same region of the sequence
  * a method called SCOOP, that looks for common matches in search results that may indicate a relationship

All of this information is used by one of our curators to make a decision about where families are related and we strive to find information in literature that support the relationship, e.g. common function.

Is possible to build Wise2 with HMMER3 support?
===============================================

The way we get round the problem with the difference in HMMER versions, is to convert the profile HMMs that are in HMMER3 format to HMMER2 format using the HMMER3 program "hmconvert" (with -2) flag. To make the searches feasible, we screen the DNA for potential domains using ncbi-blast and the Pfam-A.fasta as a target library. GeneWise is then used to calculate a subset of profile HMMs against the DNA. There is some down-weighting of the bits-per-position between H2 and H3 HMMs that the conversion does not account for, leading inevitably to some false negatives for some families/sequences. However, until GeneWise is patched to deal with HMMER3 models, this is the best course of action.

What happened to the Pfam_ls and Pfam_fs files?
===============================================

In the past, each Pfam family was represented by two profile-hidden Markov models (HMMs). One of these could match partially to a family and was called local or fs mode, the other required a sequence to match to the whole length of the profile HMM, and was called glocal or ls mode. With HMMER2, we found that the combination of the two models gave us the most sensitive searches. However, HMMER3 models are only available for searching in local (fs) mode. Because of the improvements in HMMER3, this single model is as sensitive as the two combined HMMER2 models. This means that we no longer provide two profile HMM libraries called 'HMM_ls' and 'HMM_fs'. Instead, a single library is available called 'Pfam-A.hmm'.

How can I search Pfam locally?
==============================

If you have a large number of sequences or you don't want to post your sequence across the web, you can search your sequence locally using the 'pfam_scan.pl' script.

In terms of HMMs and formats, Pfam is based around the `HMMER <http://hmmer.org/>`_  package. This will need to be installed on your local machine. You will need also to download the Pfam profile HMM libraries from the FTP site, as well as a few modules from CPAN, most notably Moose.

Full details on how to get 'pfam_scan.pl' up and running can be found on our `FTP site <ftp://ftp.ebi.ac.uk/pub/databases/Pfam/Tools/README>`_.

Why doesn't Pfam include my sequence?
=====================================

Pfam is built from a fixed release of UniProtKB. At each Pfam release we incorporate sequences from the latest release of UniProtKB. This means that, at any time, the sequences used by Pfam might be several months behind those in the most up-to-date versions of the sequence databases. If your sequence isn't in Pfam, you can still find out what domains it contains by pasting it into the sequence search box on the `search page <http://pfam.xfam.org/search>`_.

Why is there apparent redundancy of UniProtKB IDs in the full-length FASTA sequence file?
=========================================================================================

A given Pfam family may match a single protein sequence multiple times, if the domain/family is a repeating unit, for example, or when the profile HMM matches only to short stretches of the sequence but matches several times. In such cases the FASTA file with the full length sequences will contain multiple copies of the same sequence.

How many accurate alignments do you have?
=========================================

Release 33.1 has 18259 families. Over 75.1% of the proteins in SWISSPROT 2019_08 and TrEMBL 2019_08 have at least one match to a Pfam-A family.

How can I submit a new domain?
==============================

If you know of a domain that is not present in Pfam, you can submit it to the `Pfam helpdesk <pfam-help@ebi.ac.uk>`_ and we will endeavour to build a Pfam entry for it. We ask that you supply us with a multiple sequence alignment of the domain (please send the alignment file as a text file (e.g. .txt) and not in the format of a specific application such as Microsoft Word (e.g. a .doc) file), and associated literature evidence if available.

Can I search my protein against Pfam?
=====================================

Of course! Please use this `search form <http://pfam.xfam.org/search?tab=searchProteinBlock#tabview=tab1>`_.

Why do I get slightly different results when I search my sequence against Pfam versus when I look up a sequence on the Pfam website?
====================================================================================================================================

When a sequence region has overlapping matches to more than one family within the same clan, we only show one of those matches. If the sequence region is also in the seed alignment for a family, only the match to that family is shown. Otherwise we show the family that corresponds to the match with the lowest E-value.

There are cases where a sequence region is in the seed alignment of a Pfam family (family A), but it does not have a significant match to that family’s profile HMM. Occasionally, the same sequence region has a significant match to another family (family B) in the same clan. In this situation, the Pfam website will not show the match to family B as it is present in the seed alignment of family A. The sequence search will however show the match to family B as the seed alignment information is unknown. This scenario, where the sequence search shows a match that the Pfam website does not, is very rare (affecting less than 0.01% of all matches in the Pfam database).

What is the difference between the '-' and '.' characters in your full alignments?
==================================================================================

The '-' and '.' characters both represent gap characters. However they do tell you some extra information about how the profile HMM has generated the alignment. The '-' symbols are where the alignment of the sequence has used a delete state in the profile HMM to jump past a match state. This means that the sequence is missing a column that the profile HMM was expecting to be there. The '.' character is used to pad gaps where one sequence in the alignment has sequence from the profile HMMs insert state. See the alignment below where both characters are used. The profile HMM states emitting each column are shown. Note that residues emitted from the Insert (I) state are in lower case.

.. figure:: images/alignment.png
      :align: center

What do the SS lines in the alignment mean?
===========================================

These lines are structural information. The SS stands for secondary structure, and this is taken from `DSSP <http://swift.cmbi.ru.nl/gv/dssp/>`_. The following list gives the definitions for each code letter:

    * C: random Coil
    * H: alpha-helix
    * G: 3(10) helix
    * I: pi-helix
    * E: hydrogen bonded beta-strand (extended strand)
    * B: residue in isolated beta-bridge
    * T: h-bonded turn (3-turn, 4-turn, or 5-turn)
    * S: bend (five-residue bend centered at residue i)

Why don't you have domain YYYY in Pfam!
=======================================

We are very keen to be alerted to new domains. If you can provide us with a multiple sequence alignment then we will try hard to incorporate it into the database. If you know of a domain, but don't have a multiple sequence alignment, we still want to know, for simple families just one sequence is enough. Again contact the `Pfam helpdesk <pfam-help@ebi.ac.uk>`_.

Are there other databases which do this?
========================================

To a certain extent yes, there are a number of "second generation" databases which are trying to organise protein space into evolutionarily conserved regions. Examples include:

  `PROSITE <https://prosite.expasy.org>`_
       This originally was based around regular expression patterns but now also includes profiles.
  `PRINTS <http://www.bioinf.man.ac.uk/dbbrowser/PRINTS>`_
       This is based around protein "finger-prints" of a series of small conserved motifs making up a domain.
  `SMART <http://smart.embl-heidelberg.de>`_
       This is a database concentrating on extracellular modules and signaling domains.
  `InterPro <http://www.ebi.ac.uk/interpro>`_
       Combines information from Pfam, Prints, SMART, Prosite and PRODOM.
  `CDD <https://www.ncbi.nlm.nih.gov/Structure/cdd/cdd.shtml>`_
       The Conserved Domain Database is derived from Pfam and SMART databases.

So which database is better?
============================

As with everything, it depends on your problem: we would certainly suggest using more than one method. Pfam is likely to provide more interpretable results, with crisp definitions of domains in a protein. 
