.. _scores:

***********
Pfam scores
***********

E-values and Bit-scores
=======================

Pfam-A is based around hidden Markov model (HMM) searches, as provided by the HMMER3 package. In HMMER3, like BLAST, E-values (expectation values) are calculated. The E-value is the number of hits that would be expected to have a score equal to or better than this value by chance alone. A good E-value is much less than 1. A value of 1 is what would be expected just by chance. In principle, all you need to decide on the significance of a match is the E-value.

E-values are dependent on the size of the database searched, so we use a second system in-house for maintaining Pfam models, based on a bit score (see below), which is independent of the size of the database searched. For each Pfam family, we set a bit score gathering (GA) threshold by hand, such that all sequences scoring at or above this threshold appear in the full alignment. It works out that a bit score of 20 equates to an E-value of approximately 0.1, and a score 25 of to approximately 0.01. From the gathering threshold both a "trusted cutoff" (TC) and a "noise cutoff" (NC) are recorded automatically. The TC is the score for the next highest scoring match above the GA, and the NC is the score for the sequence next below the GA, i.e. the highest scoring sequence not included in the full alignment.

Sequence versus domain scores
=============================

There's an additional wrinkle in the scoring system. HMMER3 calculates two kinds of scores, the first for the sequence as a whole and the second for the domain(s) on that sequence. The "sequence score" is the total score of a sequence aligned to the model (the HMM); the "domain score" is the score for a single domain — these two scores are virtually identical where only one domain is present on a sequence. Where there are multiple occurrences of the domain on a sequence any individual match may be quite weak, but the sequence score is the sum of all the individual domain scores, since finding multiple instances of a domain increases our confidence that that sequence belongs to that protein family, i.e. truly matches the model.

Meaning of bit-score for non-mathematicians
===========================================

A bit score of 0 means that the likelihood of the match having been emitted by the model is equal to that of it having been emitted by the Null model (by chance). A bit score of 1 means that the match is twice as likely to have been emitted by the model than by the Null. A bit score of 2 means that the match is 4 times as likely to have been emitted by the model than by the Null. So, a bit score of 20 means that the match is 2 to the power 20 times as likely to have been emitted by the model than by the Null.


