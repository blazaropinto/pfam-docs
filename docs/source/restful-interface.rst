.. _restful-interface:

*****************
RESTful interface
*****************

This is an introduction to the `"RESTful" <http://www.xfront.com/REST-Web-Services.html>`_ interface to the Pfam website. `REST <http://en.wikipedia.org/wiki/Representational_State_Transfer>`_ (or Representation State Transfer) refers to a style of building websites which makes it easy to interact programmatically with the services provided by the site. A programmatic interface, commonly called an `Application Programming Interface <http://en.wikipedia.org/wiki/Api>`_ (API) allows users to write scripts or programs to access data, rather than having to rely on a browser to view a site.

Basic concepts
==============

URLs
----

A RESTful service typically sends and receives data over `HTTP <http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol>`_, the same protocol that's used by websites and browsers. As such, the services provided through a RESTful interface are identified using URLs.

In the Pfam website we use the same basic URL to provide both the standard HTML representation of Pfam data and the alternative `XML <http://en.wikipedia.org/wiki/Xml>`_ representation. To see the data for a particular Pfam-A family, you would visit the following URL in your browser:

  /family/Piwi

To retrieve the data in XML format, just add an extra parameter, output=xml, to the URL:

  /family/Piwi?output=xml 

The response from the server will now be an XML document, rather than an HTML page. 

Sending requests
----------------

Using curl
^^^^^^^^^^

Although you can use a browser to retrieve family data in XML format, it's most useful to send requests and retrieve XML programmatically. The simplest way to do this is using a Unix command line tool such as curl: 

.. code-block:: bash

  curl -LH 'Expect:' -F output=xml '/family/Piwi'
  
  <?xml version="1.0" encoding="UTF-8"?>
  <!-- information on Pfam-A family PF02171 (Piwi), generated: 16:35:52 26-Oct-2009 -->
  <pfam xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns="https://pfam.xfam.org/"
        xsi:schemaLocation="https://pfam.xfam.org/
                            https://pfam.xfam.org/static/documents/schemas/pfam_family.xsd"
        release="24.0"
        release_date="2009-10-07">
    <entry entry_type="Pfam-A" accession="PF02171" id="Piwi">
      ...


**Note**: we have recently changed the web server that we use for serving the Pfam site. Due to a bug in the server itself, requests that come from curl are normally rejected. The current work-around is to add an extra parameter to the curl command line: -H 'Expect:'. This should avoid problems with requests being rejected.

Using a script
^^^^^^^^^^^^^^

Most programming languages have the ability to send HTTP requests and receive HTTP responses. A Perl script to retrieve data about a Pfam family might be as trivial as this::

  #!/usr/bin/perl
  
  use strict;
  use warnings;
  
  use LWP::UserAgent;
  
  my $ua = LWP::UserAgent->new;
  $ua->env_proxy;
  
  my $res = $ua->get( '/family/Piwi?output=xml' );
  
  if ( $res->is_success ) {
    print $res->content;
  }
  else {
    print STDERR $res->status_line, "\n";
  }


Retriveing data
===============

Although XML is just plain text and therefore human-readable, it's intended to be parsed into a data structure. Extending the Perl script above, we can add the ability to parse the XML using an external Perl module, `XML::LibXML <http://search.cpan.org/dist/XML-LibXML/>`_::

  #!/usr/bin/perl
  
  use strict;
  use warnings;
  
  use LWP::UserAgent;
  use XML::LibXML;
  
  my $ua = LWP::UserAgent->new;
  $ua->env_proxy;
  
  my $res = $ua->get( '/family/Piwi?output=xml' );
  
  die "error: failed to retrieve XML: " . $res->status_line . "\n"
    unless $res->is_success;
  
  my $xml = $res->content;
  
  my $xml_parser = XML::LibXML->new();
  my $dom = $xml_parser->parse_string( $xml );
  
  my $root = $dom->documentElement();
  my ( $entry ) = $root->getChildrenByTagName( 'entry' );
  
  print 'accession: ' . $entry->getAttribute( 'accession' ) . "\n";

This script now prints out the accession for the family "Piwi" (`PF02171 <http://pfam.xfam.org/family/piwi>`_). 

Available services
==================

The following is a list of the sections of the website which are currently available as RESTful services.

Pfam ID/accession conversion
----------------------------

This is a simple service to return the accession and ID for a Pfam family, given either the ID or accession as input. Any of the following URLs will return the same simple XML document:

  * /family/acc?id=Piwi&output=xml
  * /family/Piwi/acc?output=xml
  * /family/id?output=xml&acc=PF02171
  * /family/Piwi/id?output=xml
  * /family?entry=Piwi&output=xml

.. code-block:: bash

  curl -LH 'Expect:' -F output=xml '/family/Piwi/acc'
  
  <?xml version="1.0" encoding="UTF-8"?>
  <!-- information on Pfam-A family PF02171 (Piwi), generated: 16:37:09 26-Oct-2009 -->
  <pfam xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns="https://pfam.xfam.org/"
        xsi:schemaLocation="https://pfam.xfam.org/
                            https://pfam.xfam.org/static/documents/schemas/pfam_family.xsd"
        release="24.0"
        release_date="2009-10-07">
    <entry entry_type="Pfam-A" accession="PF02171" id="Piwi" />
  </pfam>%

You can see the XML schema for this XML document `here <http://pfam.xfam.org/static/documents/schemas/pfam_family.xsd>`_.

Note that, as a convenience, you can also omit the output=xml parameter and the response will contain only the ID or accession, as a plain text string: 

.. code-block:: bash

  shell% curl -LH 'Expect:' '/family/Piwi/acc'
  PF02171
  shell% curl -LH 'Expect:' '/family/PF02171/id'
  Piwi

Pfam-A annotations
------------------

You can retrieve a sub-set of the data in a Pfam-A family page as an XML document using any of the following styles of URL:

  * /family?id=Piwi&output=xml
  * /family?output=xml&acc=PF02171
  * /family?entry=Piwi&output=xml
  * /family/Piwi?output=xml

The last two styles, using the entry parameter or an extended URL, accept either accessions or identifiers. The accession/ID is case-insensitive in all cases. 

.. code-block:: bash

  curl -LH 'Expect:' -F output=xml '/family/Piwi'
  
  <?xml version="1.0" encoding="UTF-8"?>
  <!-- information on Pfam-A family PF02171 (Piwi), generated: 16:35:52 26-Oct-2009 -->
  <pfam xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns="https://pfam.xfam.org/"
        xsi:schemaLocation="https://pfam.xfam.org/
                            https://pfam.xfam.org/static/documents/schemas/pfam_family.xsd"
        release="24.0"
        release_date="2009-10-07">
    <entry entry_type="Pfam-A" accession="PF02171" id="Piwi">
      <description>
  <![CDATA[
  Piwi domain
  ]]>
      </description>
      <comment>
  <![CDATA[
  This domain is found in the protein Piwi and its relatives.  The function of this
  domain is the dsRNA guided hydrolysis of ssRNA. Determination of the crystal
  structure of Argonaute reveals that PIWI is an RNase H domain, and identifies
  Argonaute as Slicer, the enzyme that cleaves mRNA in the RNAi RISC complex [2].
  In addition, Mg+2 dependence and production of 3'-OH and 5' phosphate products
  are shared characteristics of RNaseH and RISC. The PIWI domain core has a tertiary
  structure belonging to the RNase H family of enzymes.  RNase H fold proteins all
  have a five-stranded mixed beta-sheet surrounded by helices. By analogy to
  RNase H enzymes which cleave single-stranded RNA guided by the DNA strand in an
  RNA/DNA hybrid, the PIWI domain can be inferred to cleave single-stranded RNA,
  for example mRNA, guided by double stranded siRNA.
  ]]>
      </comment>
      <curation_details>
        <status>CHANGED</status>
        <seed_source>Bateman A</seed_source>
        <num_archs>16</num_archs>
        <num_seqs>
          <seed>21</seed>
          <full>756</full>
        </num_seqs>
        <num_species>140</num_species>
        <num_structures>22</num_structures>
        <percentage_identity>30</percentage_identity>
        <av_length>277.50</av_length>
        <av_coverage>33.67</av_coverage>
        <type>Family</type>
      </curation_details>
      <hmm_details hmmer_version="3.0b2" model_version="10" model_length="304">
        <build_commands>hmmbuild  -o /dev/null HMM SEED</build_commands>
        <search_commands>hmmsearch -Z 9421015 -E 1000 HMM pfamseq</search_commands>
        <cutoffs>
          <gathering>
            <sequence>19.9</sequence>
            <domain>19.9</domain>
          </gathering>
          <trusted>
            <sequence>20.0</sequence>
            <domain>21.0</domain>
          </trusted>
          <noise>
            <sequence>18.6</sequence>
            <domain>19.5</domain>
          </noise>
        </cutoffs>
      </hmm_details>
    </entry>
  </pfam>%

You can see the `XML schema <http://en.wikipedia.org/wiki/Xml_schema>`_ for this XML document `here <http://pfam.xfam.org/static/documents/schemas/pfam_family.xsd>`_.

Some Pfam families are removed or merged into others, in which case they become "dead" families. If you try to retrieve annotation information about a dead family, you'll get a simple XML document that only includes information on the replacement (if any) for the family: 

.. code-block:: bash

  curl -LH 'Expect:' -F output=xml '/family/PF06700'
  
  <?xml version="1.0" encoding="UTF-8"?>
  <!-- information on dead Pfam-A family PF06700 (2oxo_fer_oxidoB), generated: 16:34:44 26-Oct-2009 -->
  <dead_pfam xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xmlns="https://pfam.xfam.org/"
             xsi:schemaLocation="https://pfam.xfam.org/
                                 https://pfam.xfam.org/static/documents/schemas/pfam_family.xsd"
             release="24.0"
             release_date="2009-10-07">
    <entry accession="PF06700"
           id="2oxo_fer_oxidoB">
      <forward_to>PF02775</forward_to>
      <comment>Merged into TPP binding domain</comment>
    </entry>
  </dead_pfam>

You can see the XML schema for this XML document `here <http://pfam.xfam.org/static/documents/schemas/dead_family.xsd>`_. 

Pfam-A family list
------------------

You can retrieve a list of all Pfam-A families in the latest Pfam release, either as an XML document or as a tab-delimited text file. Both formats contain the Pfam-A accession, Pfam-A identifier and description:

  /families?output=xml
  /families?output=text

You can also view the list in a web browser by removing the output=xml parameter from the URL. 

.. code-block:: bash

  curl -LH 'Expect:' -F output=xml '/families'
  
  <?xml version="1.0" encoding="UTF-8"?>
  <!-- all Pfam-A families, generated: 16:12:54 26-Oct-2009 -->
  <pfam xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns="https://pfam.xfam.org/"
        xsi:schemaLocation="https://pfam.xfam.org/
                            https://pfam.xfam.org/static/documents/schemas/pfam_families.xsd"
        release="24.0"
        release_date="2009-10-07">
    <entry entry_type="Pfam-A" accession="PF00001" id="7tm_1">
      <description>
  <![CDATA[
  7 transmembrane receptor (rhodopsin family)
  ]]>
      </description>
    </entry>
    ...

You can see the XML schema for this XML document `here <http://pfam.xfam.org/static/documents/schemas/pfam_families.xsd>`_.

Protein sequence data
---------------------

You can retrieve a sub-set of the data in a protein page as an XML document using any of the following styles of URL:

  * /protein?id=CANX_CHICK&output=xml
  * /protein?output=xml&acc=P00789
  * /protein?entry=P00789&output=xml
  * /protein/P00789?output=xml

As for Pfam-A families, arguments are all case-insensitive and the entry parameter accepts either ID or accession.  

.. code-block:: bash

  curl -LH 'Expect:' -F output=xml '/protein/P00789'
  
  <?xml version="1.0" encoding="UTF-8"?>
  <!-- information on UniProt entry P00789 (CANX_CHICK), generated: 16:28:26 26-Oct-2009 -->
  <pfam xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns="https://pfam.xfam.org/"
        xsi:schemaLocation="https://pfam.xfam.org/
                            https://pfam.xfam.org/static/documents/schemas/protein.xsd"
        release="24.0"
        release_date="2009-10-07">
    <entry entry_type="sequence" db="uniprot" db_release="57.6" accession="P00789" id="CANX_CHICK">
      <description>
  <![CDATA[
  Calpain-1 catalytic subunit EC=3.4.22.52
  ]]>
      </description>
      <taxonomy tax_id="9031" species_name="Gallus gallus (Chicken)">
        Eukaryota; Metazoa; Chordata; Craniata; Vertebrata; Euteleostomi; Archosauria;
        Dinosauria; Saurischia; Theropoda; Coelurosauria; Aves; Neognathae; Galliformes;
        Phasianidae; Phasianinae; Gallus.
      </taxonomy>
      <sequence length="705" md5="934014b14ecb71623fa5898c7f81862a" crc64="ABCDDC56298E48AA" version="2">
        MMPFGGIAARLQRDRLRAEGVGEHNNAVKYLNQDYEALKQECIESGTLFRDPQFPAGPTALGFKELGPYSSKTR
        GVEWKRPSELVDDPQFIVGGATRTDICQGALGDCWLLAAIGSLTLNEELLHRVVPHGQSFQEDYAGIFHFQIWQ
        FGEWVDVVVDDLLPTKDGELLFVHSAECTEFWSALLEKAYAKLNGCYESLSGGSTTEGFEDFTGGVAEMYDLKR
        APRNMGHIIRKALERGSLLGCSIDITSAFDMEAVTFKKLVKGHAYSVTAFKDVNYRGQQEQLIRIRNPWGQVEW
        TGAWSDGSSEWDNIDPSDREELQLKMEDGEFWMSFRDFMREFSRLEICNLTPDALTKDELSRWHTQVFEGTWRR
        GSTAGGCRNNPATFWINPQFKIKLLEEDDDPGDDEVACSFLVALMQKHRRRERRVGGDMHTIGFAVYEVPEEAQ
        GSQNVHLKKDFFLRNQSRARSETFINLREVSNQIRLPPGEYIVVPSTFEPHKEADFILRVFTEKQSDTAELDEE
        ISADLADEEEITEDDIEDGFKNMFQQLAGEDMEISVFELKTILNRVIARHKDLKTDGFSLDSCRNMVNLMDKDG
        SARLGLVEFQILWNKIRSWLTIFRQYDLDKSGTMSSYEMRMALESAGFKLNNKLHQVVVARYADAETGVDFDNF
        VCCLVKLETMFRFFHSMDRDGTGTAVMNLAEWLLLTMCG
      </sequence>
      <matches>
        <match accession="PF00648" id="Peptidase_C2" type="Pfam-A">
          <location start="48" end="347" ali_start="48" ali_end="347" hmm_start="1" hmm_end="298" evalue="2.6e-148" bitscore="502.00" />
        </match>
        <match accession="PF01067" id="Calpain_III" type="Pfam-A">
          <location start="358" end="513" ali_start="358" ali_end="512" hmm_start="1" hmm_end="144" evalue="3.5e-57" bitscore="201.20" />
        </match>
      </matches>
    </entry>
  </pfam>

You can see the XML schema for this XML document `here <http://pfam.xfam.org/static/documents/schemas/protein.xsd>`_. 

Sequence searches
-----------------

The Pfam website includes a `form <http://pfam.xfam.org/search>`_ that allows users to upload a protein sequence and see a list of the Pfam domains that are found on their search sequence. We've now implemented a RESTful interface to this search tool, making it possible to run single-sequence Pfam searches programmatically.

Running a search is a two step process:

    1. submit the search sequence and specify search parameters
    2. retrieve search results in XML format

The reason for separating the operation into two steps rather than performing a search in a single operation is that the time taken to perform a sequence search will vary according to the length of the sequence searched. Most web clients, browsers or scripts, will simply time-out if a response is not received within a short time period, usually less than a minute. By submitting a search, waiting and then retrieving results as a separate operation, we avoid the risk of a client reaching a time-out before the results are returned.

The following example uses simple command-line tools to submit the search and retrieve results, but the whole process is easily transferred to a single script or program. 

Save your sequence to file
^^^^^^^^^^^^^^^^^^^^^^^^^^

It is usually most convenient to save your sequence into a plain text file, something like this: 

.. code-block:: bash

  MMASTENNEKDNFMRDTASRSKKSRRRSLWIAAGAVPTAIALSLSLASPA
  AVAQSSFGSSDIIDSGVLDSITRGLTDYLTPRDEALPAGEVTYPAIEGLP
  AGVRVNSAEYVTSHHVVLSIQSAAMPERPIKVQLLLPRDWYSSPDRDFPE
  IWALDGLRAIEKQSGWTIETNIEQFFADKNAIVVLPVGGESSFYTDWNEP
  NNGKNYQWETFLTEELAPILDKGFRSNGERAITGISMGGTAAVNIATHNP
  EMFNFVGSFSGYLDTTSNGMPAAIGAALADAGGYNVNAMWGPAGSERWLE
  NDPKRNVDQLRGKQVYVSAGSGADDYGQDGSVATGPANAAGVGLELISRM
  TSQTFVDAANGAGVNVIANFRPSGVHAWPYWQFEMTQAWPYMADSLGMSR
  EDRGADCVALGAIADATADGSLGSCLNNEYLVANGVGRAQDFTNGRAYWS
  PNTGAFGLFGRINARYSELGGPDSWLGFPKTRELSTPDGRGRYVHFENGS
  IYWSAATGPWEIPGDMFTAWGTQGYEAGGLGYPVGPAKDFNGGLAQEFQG
  GYVLRTPQNRAYWVRGAISAKYMEPGVATTLGFPTGNERLIPGGAFQEFT
  NGNIYWSASTGAHYILRGGIFDAWGAKGYEQGEYGWPTTDQTSIAAGGET
  ITFQNGTIRQVNGRIEESR

The sequence should contain only valid sequence characters, i.e. letters, excluding "J" and "O". You can break the sequence across multiple lines to make it easier to handle. 

Submit the search
^^^^^^^^^^^^^^^^^

.. code-block:: bash

  curl -LH 'Expect:' -F seq='<test.seq' -F output=xml 'https://pfam.xfam.org/search/sequence'
  
  <?xml version="1.0" encoding="UTF-8"?>
  <jobs xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns="https://pfam.xfam.org/"
        xsi:schemaLocation="https://pfam.xfam.org/
                            https://pfam.xfam.org/static/documents/schemas/submission.xsd">
    <job job_id="adabec68-703f-48c4-bec7-07f1ab965fbb">
      <opened>2010-03-26 11:25:57</opened>
      <result_url>https://pfam.xfam.org/search/sequence/resultset/adabec68-703f-48c4-bec7-07f1ab965fbb?output=xml</result_url>
    </job>
  </jobs>

You can see the XML schema for this XML document `here <http://pfam.xfam.org/static/documents/schemas/submission.xsd>`_.

When using curl the value of the parameter "seq" needs to be quoted so that its value is taken correctly from the file "test.seq". The second parameter can also be added directly to the URL, as a regular CGI-style parameter, if you prefer.

The search service accepts the following parameters (you can see a more complete description of these settings `here <http://pfam.xfam.org/search>`_): 

.. csv-table:: Accepted sequence search parameters
  :header: "Parameter", "Description", "Accepted values", "Default", "Notes"
  :widths: 10, 20, 20, 10, 30

  "evalue", "use this E-value cut-off", "valid float < 10.0", "none", "the default is to have no E-value and to use the gathering threshold. See note below. If an E-value is given, it will be used, regardless of the value of ga"
  "ga", "use gathering threshold", "0 | 1", "1", "the default is to have no E-value and to use the gathering threshold. See note below. If an E-value is given, it will be used, regardless of the value of ga"
  "seq", "protein sequence", "valid sequence characters", "none", "**required**"

**Note**: this documentation previously suggested that searches submitted through the RESTful interface used an E-value cut-off of 1.0 by default. This is incorrect. RESTful searches use the gathering threshold and not an E-value of 1.0. This is the opposite of the behaviour of the searches run through the web interface. We apologise for the inconsistency.

Wait for the search to complete
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Although you can check for results immediately, if you poll before your job has completed, you won't receive an XML document. Instead, the HTTP response to your request will have its status set appropriately and the body of the response will contain only string giving the status. You should ideally check the HTTP status of the response, rather than relying on the body of the response.

These are the possible status codes for the response: 

.. csv-table:: Search response status codes
  :header: "HTTP status code", "Status description", "Response body", "Notes"
  :widths: 10, 20, 20, 50

  202, "Accepted", "PEND / RUN", "The job has been accepted by the search system and is either pending (waiting to be started) or running. After a short delay, your script should check for results again"
  502, "Bad gateway", "FAIL", "There was a problem scheduling or running the job. The job has failed and will not produce results. There is no need to check the status again"
  503, "Service unavailable", "HOLD", "Your job was accepted but is on hold. This status will not be assigned by the search system, but by an administrator. There is probably a problem with the job and you should contact the help desk for assistance with it"
  410, "Gone", "DEL", "Your job was deleted from the search system. This status will not be assigned by the search system, but by an administrator. There was probably a problem with the job and you should contact the help desk for assistance with it"
  500, "Internal server error", "Error message", "There was some problem with running your job, but it does not fall into any of the other categories. The body of the response will contain an error message from the server. Contact the help desk for assistance with the problem"

When writing a script to submit searches and retrieve results, please add a short delay between the submission and the first attempt to retrieve results. Most search jobs are returned within four to five seconds of submission, depending greatly on the length of the sequence to be searched.

Retrieve results
^^^^^^^^^^^^^^^^

The XML that was returned from the first query includes one or more URLs from which you can now retrieve results, given in the <result_url>. You can now poll these URLs to retrieve XML documents with the search hits. 

.. code-block:: bash

  curl -LH 'Expect:' 'https://pfam.xfam.org/search/sequence/resultset/adabec68-703f-48c4-bec7-07f1ab965fbb?output=xml'
  
  <?xml version="1.0" encoding="UTF-8"?>
  <pfam xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xmlns="https://pfam.xfam.org/"
        xsi:schemaLocation="https://pfam.xfam.org/
                            https://pfam.xfam.org/static/documents/schemas/results.xsd"
        release="24.0"
        release_date="2009-10-07">
    <results job_id="adabec68-703f-48c4-bec7-07f1ab965fbb">
      <matches>
        <protein length="669">
          <database id="pfam" release="24.0" release_date="2009-10-07">
            <match accession="PF08310.4" id="LGFP" type="Pfam-A" class="Repeat">
              <location start="422" end="475" ali_start="422" ali_end="473"
                hmm_start="1" hmm_end="52" evalue="5.9e-10" bitscore="38.3" evidence="hmmer v3.0b2" significant="1" />
              <location start="476" end="529" ali_start="476" ali_end="528"
                hmm_start="1" hmm_end="53" evalue="4.8e-23" bitscore="80.2" evidence="hmmer v3.0b2" significant="1" />
              <location start="530" end="580" ali_start="530" ali_end="578"
                hmm_start="1" hmm_end="51" evalue="3e-06" bitscore="26.4" evidence="hmmer v3.0b2" significant="1" />
              <location start="581" end="633" ali_start="581" ali_end="633"
                hmm_start="1" hmm_end="54" evalue="1e-19" bitscore="69.5" evidence="hmmer v3.0b2" significant="1" />
            </match>
            <match accession="PF00756.13" id="Esterase" type="Pfam-A" class="Family">
              <location start="122" end="392" ali_start="122" ali_end="390"
                hmm_start="1" hmm_end="250" evalue="3.1e-62" bitscore="209.9" evidence="hmmer v3.0b2" significant="1" />
            </match>
          </database>
        </protein>
      </matches>
    </results>
  </pfam>

You can see the XML schema for this XML document `here <http://pfam.xfam.org/static/documents/schemas/results.xsd>`_.

Since the search is performed by the same server as searches in the Pfam website, you can view your results in a web page by modifying the URL slightly:

  /search/sequence/resultset/adabec68-703f-48c4-bec7-07f1ab965fbb

Note that old search results are generally cleared out after some time, so if you wait too long before trying to view your hits in the website, you may find that they are already gone. 

Retrieve domain graphics description
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When you run a sequence search via the browser, the results page includes a Pfam domain graphic, showing the locations of any matching Pfam families on your search sequence. When running a search via the RESTful interface, you can't retrieve the domain graphic directly, since it's generated using a javascript class in the browser. However, you can retrieve the `JSON <http://en.wikipedia.org/wiki/Json>`_ string that describes the graphic:

  /search/sequence/graphic/adabec68-703f-48c4-bec7-07f1ab965fbb

Check the :ref:`guide-to-graphics` for details on how you can use the JSON string locally. 

