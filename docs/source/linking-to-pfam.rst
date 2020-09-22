.. _linking-to-pfam:

***************************
Linking to the Pfam website
***************************

Linking to family pages
=======================

You can refer to Pfam families either by accession or ID. You can also refer to a family by "entry", although this is a convenience that should be used only if you're not sure if what you have is an accession or an ID.

Pfam accession numbers are more stable between releases than IDs and we strongly recommend that you link by accession number.

Here are some examples of linking to Pfam families:

Directly, using either accession or ID:
    `/family/PF00002 <http://pfam.xfam.org/family/PF00002>`_ or
    `/family/7tm_2 <http://pfam.xfam.org/family/7tm_2>`_ 
Using a parameter, by accession:
    `/family?acc=PF00002 <http://pfam.xfam.org/family?acc=PF00002>`_ 
Using a parameter, by ID:
    `/family?id=7tm_2 <http://pfam.xfam.org/family?id=7tm_2>`_ 
Using the "entry" parameter with either accession or ID:
    `/family?entry=PF00002 <http://pfam.xfam.org/family?entry=PF00002>`_ or
    `/family?entry=7tm_2 <http://pfam.xfam.org/family?entry=7tm_2>`_ 

Linking to protein sequence pages
=================================

As for Pfam family pages, you can refer to protein sequence pages by accession, ID or entry. Protein IDs are unstable and do change between releases, so, again, we strongly recommend that you use protein accessions where possible.

Here are some examples of linking to protein sequence pages at EBI:

Directly:
    `/protein/P15498 <http://pfam.xfam.org/protein/P15498>`_ or\n
    `/protein/VAV_HUMAN <http://pfam.xfam.org/protein/VAV_HUMAN>`_
By accession:
    `/protein?acc=P15498 <http://pfam.xfam.org/protein?acc=P15498>`_
By ID:
    `/protein?id=VAV_HUMAN <http://pfam.xfam.org/protein?id=VAV_HUMAN>`_
Using "entry":
    `/protein?entry=P15498 <http://pfam.xfam.org/protein?entry=P15498>`_ or\n
    `/protein?entry=VAV_HUMAN <http://pfam.xfam.org/protein?entry=VAV_HUMAN>`_ 

Linking to the "jump to" search
===============================

The Pfam website features a search tool that tries to guess the type of any accession or ID that it is given. For example, if given "VAV_HUMAN", the search returns the URL for the protein sequence page for the VAV_HUMAN entry. If given "1w9h", the search returns the URL for the PDB entry (structure) 1w9h.

You can use the "jump to" search if you need to link to Pfam but can't be sure what type of accession or ID you will be using in your link. By default, the search returns the URL that it has found, as a simple, plain text HTTP response. Adding the parameter redirect=1 will make the "jump to" tool redirect to the URL that it finds or, if it couldn't find an appropriate URL, to the Pfam homepage.

Return URL:
    `/search/jump?entry=P15498 <http://pfam.xfam.org/search/jump?entry=P15498>`_
Redirect:
    `/search/jump?entry=P15498&redirect=1 <http://pfam.xfam.org/search/jump?entry=P15498&redirect=1>`_

Note that, although it may be convenient to link to Pfam using this search tool, there is no error reporting for your users if the search fails to find an appropriate URL in the Pfam site. It is much safer to link directly to the correct section of the site. Please contact us if you need help with building specific links.

