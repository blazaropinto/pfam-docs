.. _glossary:

********
Glossary
********
.. contents::
  :local:

Alignment coordinates
=====================

HMMER3 reports two sets of domain coordinates for each profile HMM match. The envelope coordinates delineate the region on the sequence where the match has been probabilistically determined to lie, whereas the alignment coordinates delineate the region over which HMMER is confident that the alignment of the sequence to the profile HMM is correct. Our full alignments contain the envelope coordinates from HMMER3.

Architecture
============

The collection of domains that are present on a protein.

Clan
====

A collection of related Pfam entries. The relationship may be defined by similarity of sequence, structure or profile-HMM.

Domain
======

A structural unit.

Domain score
============

The score of a single domain aligned to a profile HMM. Note that, for HMMER2, if there was more than one domain, the sequence score was the sum of all the domain scores for that Pfam entry. This is not quite true for HMMER3.

DUF
===

Domain of unknown function.

Envelope coordinates
====================

See Alignment coordinates.

Family
======

A collection of related protein regions.

Full alignment
==============

An alignment of the set of related sequences which score higher than the manually set threshold values for the profile HMMs of a particular Pfam entry.

Gathering threshold (GA)
========================

Also called the gathering cut-off, this value is the search threshold used to build the full alignment. The gathering threshold is assigned by a curator when the family is built. The GA is the minimum score a sequence must attain in order to belong to the full alignment of a Pfam entry. For each Pfam profile HMM we have two GA cutoff values, a sequence cutoff and a domain cutoff.

HMMER
=====

The suite of programs that Pfam uses to build and search profile HMMs. Since Pfam release 24.0 we have used HMMER version 3 to make Pfam. See the `HMMER <http://hmmer.janelia.org/>`_ site for more information.

Hidden Markov model (HMM)
=========================

A profile HMM is a probablistic model. In Pfam we use profile HMMs to transform the information contained within a multiple sequence alignment into a position-specific scoring system. We search our profile HMMs against the UniProt protein database to find homologous sequences.

Motif
=====

A short unit found outside globular domains.

Noise cutoff (NC)
=================

The bit scores of the highest scoring match not in the full alignment.

Pfam-A
======

A profile HMM based hand curated Pfam entry which is built using a small number of representative sequences. We manually set a threshold value for each profile-HMM and search our models against the UniProtKB database. All of the sequnces which score above the threshold for a Pfam entry are included in the entry's full alignment.

Pfam-B
======

A set of unannotated, computationally generated multiple sequence alignments. They are one of the sources we use for creating Pfam-A entries.

Posterior probability
=====================

HMMER reports a posterior probability for each residue that matches a 'match' or 'insert' state in the profile HMM. A high posterior probability shows that the alignment of the amino acid to the match/insert state is likely to be correct, whereas a low posterior probability indicates that there is alignment uncertainty. This is indicated on a scale with '*' being 10, the highest certainty, down to 1 being complete uncertainty. Within Pfam we display this information as a heat map view, where green residues indicate high posterior probability, and red ones indicate a lower posterior probability.

Repeat
======

A short unit which is unstable in isolation but forms a stable structure when multiple copies are present.

Seed alignment
==============

An alignment of a set of representative sequences for a Pfam entry. We use this alignment to construct the profile HMMs for the Pfam entry.

Sequence score
==============

The total score of a sequence aligned to a profile HMM. If there is more than one domain, the sequence score is the sum of all the domain scores for that Pfam entry. If there is only a single domain, the sequence and the domains score for the protein will be identical. We use the sequence score to determine whether a sequence belongs to the full alignment of a particular Pfam entry.

Trusted cutoff (TC)
===================

The bit scores of the lowest scoring match in the full alignment. 

