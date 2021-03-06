# Is it working? The Application of the Linked Art Data Model on the databases "Deutsch-Französische Kunstvermittlung"

Author: Anne Klammt

Vers. 1.0

Date 15/06/2022

## Context
From 2000 to 2006, two closely interwoven Franco-German projects aimed at understanding and presenting the mutual perception of art production in France and Germany from the late 19th century to the postwar period. The projects "Franco-German Art Mediation 1870-1945" and "Franco-German Art Mediation 1945-1960" focused on periodicals and were part of the then very productive research on cultural transfer. Funded by the VW Foundation, the Getty Grant and the Fritz Thyssen Foundation, the two projects were carried out jointly by the DFK Paris and the Art History Institute of the Free University of Berlin (more on the [website of the DFK Paris](https://dfk-paris.org/de/page/deutsch-franzoesische_kunstvermittlung_1870%E2%80%931940_und_1945%E2%80%931960-2389.html)).

One deliverable of both projects was a collection of tagged and often annotated contemporary articles and book chapters in the form of a database. This was realized in a quadripartite relational database, comprising for both projects one database on French criticism of German art and one on German criticism of French art. Beginning in 2004, they were migrated to a database hosted by DFK Paris and made available online for searching the records. In 2019, the MySQL database was no longer maintainable from a technical point of view and the data were migrated again and presented in a completely new graphical user interface through the website. In 2021, DFK Paris launched a curation activity aimed at improving the user interface, semantically enriching the data, and making it easier for developers to use the datasets.

The data curation resulted in a prototype that applies the [Linked Art Data Model](https://linked.art) as a tool to transport the provenance of the information for each record individually. Here, the databases are considered as information objects that have gone through events such as their creation before 2004 and their curation in 2021 to 2022. The conception of the prototype is part of the research on data repurposing in art history at DFK Paris ([Datacuration project on the website](https://dfk-paris.org/en/research-project/datenkuration-am-beispiel-der-datenbank-deutsch-franz%C3%B6sische-kunstvermittlung-1871)).

## Short introduction to the Linked Art Data Model and its applicability

The Linked Art Data Model (LADM) is a proposal to make data from cultural heritage collections interoperable and usable as Linked Open Data. As a community-driven project, it openly follows the approach of the IIIF initiative and in the same way promotes JSON as a widely accepted format for documents by the developer community. The LADM is an application of the CIDOC CRM ontology and thus a sibling to the LIDO-XML exchange standard.

As LIDOX XML serves as an intelligent solution for the interoperability of specialized collection data and central nodes such as Europeana, it offers a combination of rigor in terms of data structure and certain information defined as mandatory, as well as flexibility within its main sections. The LADM aims at reusability of the data in new applications and therefore allows individual structure of the data, but focuses on a common grammar and label set. The "grammar" is CIDOC-CRM, and the label set is mostly Getty AAT. These features of LADM serve to support the main goal of data curation at DFK Paris, which is to reuse legacy data without stripping them of their original research context. 

Nevertheless, the application of LADM to databases is not without problems, and it is even unclear whether it is applicable at all from a theoretical point of view, since it is intended for collection data. At the heart of the LADM approach is a (usually) digitized collection object such as a digital surrogate of a coin, painting, or whatever artefact. In the case of DFK Paris databases, we instead focus on an digital information object. Like a poem, however, a database is an expression that is represented textually. So like the subject of a painting, the object is intangible, and what we host on our server is a representation. So even if it is possible from a technical point of view, it is questionable whether the application of LADM is appropriate.

## Subject and structure of the document

This document addresses how to apply the LADM to the legacy data created in the projects nearly two decades ago and profoundly changed by their semantic enrichment in 2021-2022. It is roughly structured along information sequences that are observed and separated in the records that form the information objects within the three-part database. Each part of the document begins with a brief characterization of the assumed information sequence and continues with a representation of its implementation as JSON. All these snippets are closed so that they can be copied into a JSON editor, for example, without evoking error messages.

The text is introduced by a description of the meaning of the term "record" in the context of the DFKV data collection. The final summary provides a brief overview of the overall structure and open questions.

## Application

### definition of "data record" in the project

A data record in the databases of the "Deutsch-französische Kunstvermittlung"-projects represents a digital information object, that collects structured and semi-structured data. A data record consists firstly of the reference to one or more sources with bibliographic informations (always) and a quotation (often) and secondly of keywords (mostly), a description (often) and the categorization of the source-type (sometimes). Thirdly rights statements and activities are documenting the creation, curation and terms of usage of the data record. There is no entity like a person, a book or a date that forms the spine of the record, but a record represents the information, that a researcher collected and tagged one or more written sources, s/he evaluated as relevant for the project (s. for more information [link to project at website DFK](https://dfk-paris.org/de/page/deutsch-franz%C3%B6sische-kunstvermittlung-1871%E2%80%931940-und-1945%E2%80%931960-2389.html)). Each data record was part of one of the three former databases, which were technically aligned as early 2004 to one database that consists of approximately 6000 data records.
     
### Prerequisites for applying linked.art , context of the data set and identifier

The prerequisites for applying the LADLM on the level of the data record are that each data record has an URI and all the properties and classes used have to be referred to linked.art. Finally the type of the entire entity - the data record - has to be declared and its context indicated.
Although the URI carries the ID of the record in the database, we want to state separately the ID als information for the identification of the data record.


		{"@context": "https://linked.art/ns/v1/linked-art.json", 
		"id": "https://dfk-paris.org/example/datarecord/10056", 
		"_label": "datarecord ID 10056",
		"identified_by" : [{
		    "type": "Identifier",
     		"_label": "ID database DFKV",
      		"classified_as": [{
        		   "id": "http://vocab.getty.edu/aat/300314626",  
          		 "type": "Type",
          		 "_label": "Identification Number"}],  
     	 "content" : "ID_10056" }]}
 
### The dataset as part of a database and the events acting on it 

The dataset is<code>part_of</code> a database <code>produced_by</code> a group of researchers led by Thomas W. Gaehtgens. Additional attributes make it possible to add information about the time period of production and even the location. In the case of the three databases, the latter is helpful additional information for contextualizing the object.

To express this, we can apply the role of workshops provided by LADM, because workshop refers to a group of artists who produced an object without each member being actively involved. Whether a group is directly led by one person or loosely inspired no longer matters for modeling purposes.   
Similarly, we refer to data curation as an activity<code>curated_by</code>another group.

Neither does "curation" exist as an activity in LADM, nor is there the property "curated by". We newly introduce these two terms here because they are of central importance to us. LADM is not ignorant of the role of curators, so already the assignment of objects (dating, style, authorship) can be recorded as their activity, and also their role in assembling collections of objects can be expressed. Accordingly, our proposal can be seen as a further simplification.


	{"@context": "https://linked.art/ns/v1/linked-art.json", 
	 "part_of" : [{
         "type" : "Digital Object", 
         "_label" : "bibliographic database", 
         "classified_as": [{
     		 "id": "http://vocab.getty.edu/page/aat/300044188",
     		 "type": "Type",
     		 "_label": "bibliographic database"}],
         "identified_by" : [{"type" : "Name",
            "content" : "Deutsch-französische Kunstvermittlung 1870-1940, Paris"}],
         "access_point": [{
      		 "id": "https://dfk-paris.org/de/page/deutsch-franzoesische-kunstvermittlung-1870_1940-und-1945_1960-datenbank-2391.html",
      		 "type": "DigitalObject"}],
    	    "produced_by": {
    	       "type": "Production",
    	       "timespan": {
              "type": "TimeSpan",
              "begin_of_the_begin": "1999-10-01T",
              "end_of_the_end": "2004-01-20T"},
      "carried_out_by": [{
        "type": "Group",
        "_label": "research subproject: Deutsch-französische Kunstvermittlung 1870-1940, Paris",
        "formed_by": {
          "type": "Formation",
          "influenced_by": [{
              "type": "Person",
              "_label": "Thomas W. Gaehtgens"}]}}],
          "took_place_at": [{
             "type": "Place",
             "_label": "DFK Paris"}]},
       "curated_by": {
          "type": "data curation",
          "timespan": {
              "type": "TimeSpan",
              "begin_of_the_begin": "2021-03-01T",
              "end_of_the_end": "2022-05-31T"},
         "carried_out_by": [{
                "type": "Group",
           "_label": "research project: Datenkuration am Beispiel der Datenbank Deutsch-Französische Kunstvermittlung 1870–1940 und 1945–1960",
           "formed_by": {
             "type": "Formation",
          "influenced_by": [{
              "type": "Person",
              "_label": "Anne Klammt"}]}}]}}]}

### content

Each data record of the bibliographic database presents at least one text in an journal (this dues to at least three third of the records) or refers to a book. As bibliographic information each data record offers information about the authors/s, the title, the journals name, volume and pagination as well as the date of publication. In the case of books the publishing house and its seat is indicated. In some cases the entry just refers to a passage within a longer article and therefore three dots followed by the first words of the passage are used as title (example: ). In few cases a data entry refers to a series of subsequently published densely related articles. In the data model those entries have several parts and more than one "time span".

The activities of the data curation in 2021 to 2022 focussed on the semantic enrichment of the journals and the authors (as part of all the persons mentioned in the databases). Almot all of the 314 journals and the majority of the authors are referenced the name authority files of the Bibliothèque national de France (BnF), the German national Library (DNB), a VIAF-number or at least an entry in Wikidata.  For some of the authors exist more than one variant of the name due to alias names and the practices of the researchers while feeding the databases in the early 2000er years. Thus the model entails also  equivalents.

#### data entries referring to articles in journals

The LADM proposes a quite easy way to refer to articles, but it does not explicitly address the title of the journal and the volume (it must be emphasized, that providing bibliographic information is not part of the scope of the LADM). For our purposes, however, this is an disadvantage as the articles, in lack of an individual identifier like a DOI, can't be identified by their title alone. Therefore we understand an article to be an application of "<code>member_of</code>" as it is a member of a journal - like a painting may be a member of a collection. An alternative would be to term the article as <code>part</code>. We used "part" for the information in which rubric the article was published.

We again chose "part" for the indication of the volume and the pagination. This surely is a less favourable solution, but in the databases "deutsch-französische Kunstvermittlung" both information used to be modelled as one string. A split of them was envisaged, but since the information is not sufficiently normalized, we dropped it.


		{"@context": "https://linked.art/ns/v1/linked-art.json",
		"id": "https://dfk-paris.org/example/datarecord/10056",
	    "type": "DigitalObject",
		"_label": "datarecord ID 10056",
		"refer_to" : [{
		   "type" : "LinguisticObject",
           "_label" : "source, what the record is about",
           "classified_as": [{
      		    "id": "http://vocab.getty.edu/aat/300048715",
      		    "type": "Type",
                "_label": "Article"},{
                "id": "http://vocab.getty.edu/aat/300435443",
                "type": "Type",
                "_label": "Type of Work"}],
           "identified_by": [{
               "type": "Name",
               "content": "Schwankungen der Bilderpreise"}],
       	 "created_by": {
    	         "type": "Creation", 
    		    "_label": "Creation of the Article Content", 
    	     "timespan": {
            "type": "TimeSpan",
            "begin_of_the_begin": "1955-10M",
            "end_of_the_end": "1955-10M"},    		    
    		 "carried_out_by": [{
        	    "id": "http://vocab.getty.edu/ulan/500115588",      		
            "type": "Person", 
        	    "_label": "Le Corbusier",
            "identified_by": [{
                 "type" : "Identifier",
                 "_label" : "DFK-ID for person name",
                 "classified_as": [{
                    "id" : "http://vocab.getty.edu/aat/300314626",
                    "type" : "Type",
                    "_label" : "Identification Number"}], 
                 "content" : "DFK11647338338"}],
             "equivalent":[{
                "id": "http://vocab.getty.edu/page/ulan/500027041"},{
                 "id":"https://www.wikidata.org/wiki/Q4724"},{
                 "type" : "Name",
                 "_label": "alias name", 
                 "classified_as": [{
                    "id" : "http://vocab.getty.edu/page/aat/300026963",
                    "type" : "Name",
                    "_label" : "aliases"}],
                 "content" : "Jeanneret, CH. E."}]}]},
          "member_of" :  [{
            "type" : "LinguisticObject",
            "_label" : "source of the text",
            "classified_as":[{
      		    "id": "http://vocab.getty.edu/aat/300048715",
      		    "type": "Type",
                "_label": "Work"}],
            "identified_by" : [{
         	    "type" : "Name",
                "_label" : "Kunstchronik"},{
                "type" : "Type",
                "_label" : "intern ID for journal",
                "classified_as": [{
                   "id" : "http://vocab.getty.edu/page/aat/300404626",
                   "type" : "Type",
                   "_label" : "Identification Number"}],
                "content" : "journal_id 1439"},{
                "type" : "Type",
                "_label" : "name authority file",
                "classified_as": [{
                   "id" : "http://vocab.getty.edu/page/aat/300026963",
                   "type" : "Type",
                   "_label" : "name authority file"}],
                "content" : "https://catalogue.bnf.fr/ark:/12148/cb32804498n"}],
            "part":[{
      			"type": "LinguisticObject",
      			"_label": "Volume & Pagination",
                "classified_as": [{
                   "id": "http://vocab.getty.edu/aat/300311699",
                   "type": "Type",
                   "_label": "Chapter"}],
                  "content" : "10.1955.11-12, p. 1407-1420"}]}],
          "part_of":[{
            "type" : "LinguisticObject",
            "_label" : "part of the journal",
            "classified_as":[{
      		    "id": "http://vocab.getty.edu/aat/300048715",
      		    "type": "Type",
                "_label": "Work"}],
            "identified_by" : [{
         	    "type" : "Name",
                "_label" : "Rubric",
                "classified_as": [{
                   "id" : "http://vocab.getty.edu/page/aat/300196121",
                   "type" : "Type",
                   "_label" : "Rubric"}],
              "content" : "Lettres"}]}]}]}
 
### Data entries referring to books

Things are less complex for books as the LADM offers the presentation of the key information in a way, that is coherent to the structure in the databases at stake. As in the LADM a chapter is essentially a <code>part</code> of the book, we also can refer to the text as a part.


	{"@context": "https://linked.art/ns/v1/linked-art.json",
		"id": "https://dfk-paris.org/example/datarecord/10056",
	    "type": "DigitalObject",
		"_label": "datarecord ID 10056",
		"refer_to" : [{
		   "type" : "LinguisticObject",
           "_label" : "source; what the record is about",
           "classified_as": [{
      		    "id": "http://vocab.getty.edu/aat/300060417",
      		    "type": "Type",
                "_label": "Monograph"}],
           "identified_by": [{
               "type": "Name",
               "content": "Schwankungen der Bilderpreise"}],
          "part": [{
            "type": "LinguisticObject",
            "_label": "Chapter",
            "classified_as": [{
              "id": "http://vocab.getty.edu/aat/300311699",
              "type": "Type",
              "_label": "Chapter"}],
              "referred_to_by":[{
                "type": "LinguisticObject",
                "classified_as": [{
                   "id": "http://vocab.getty.edu/aat/300435440",
                   "type": "Type",
                   "_label": "Pagination Statement",
                  "content": "1407-1420" }]}]}]},{
       	  "created_by": {
    	         "type": "Creation",
    		    "_label": "Creation of the Books Content", 
    		    "timespan": {
                 "type": "TimeSpan",
                 "begin_of_the_begin": "1955-10M",
                 "end_of_the_end": "1955-10M"},  
            "carried_out_by": [{
        	         "id": "http://vocab.getty.edu/ulan/500115588",      		
                 "type": "Person", 
        	         "_label": "Author",
                 "identified_by": [{
                     "type" : "Identifier",
                     "_label" : "DFK-ID for person name",
                     "classified_as": [{
                        "id" : "http://vocab.getty.edu/aat/300314626",
                        "type" : "Type",
                        "_label" : "Identification Number"}], 
                      "content" : "DFK11647338338"},{
                    "type" : "Name",
         		   "_label" : "persons name",
         		   "content" : "Le Corbusier"},{
                   "type" : "Identifier",
                   "_label": "name authority file", 
                   "classified_as": [{
                      "id" : "http://vocab.getty.edu/page/aat/300026963",
                      "type" : "Type",
                      "_label" : "name authority file"}],
                   "content" : "http://vocab.getty.edu/page/ulan/500027041"},{
                   "type" : "Identifier",
                   "_label": "name authority file", 
                   "referred_to_by": [{
                      "id" : "http://vocab.getty.edu/page/aat/300163404",
                      "type" : "Type",
                      "_label" : "reference source"}],
                   "content" : "https://www.wikidata.org/wiki/Q4724"},{
                   "type" : "Name",
                   "_label": "alias name", 
                   "classified_as": [{
                      "id" : "http://vocab.getty.edu/page/aat/300026963",
                      "type" : "Name",
                      "_label" : "aliases"}],
                   "content" : "Jeanneret, CH. E."}]}]},
                   "used_for": [{
      				 "type": "Activity",
      				 "classified_as": [{
          	   			"id": "http://vocab.getty.edu/aat/300054686",
              			 "type": "Type",
               			"_label": "Publishing"}],
           		  "carried_out_by": [{
               			"type": "Group",
            		 		"_label": "Publishing House" }]}]}]}


### Link to IIIF

Data curation in 2021 resulted in the establishment of links to digital surrogates of articles cited in the database. The LADM integrates IIIF in two ways. The first focuses on the digital surrogate itself, i.e., the IIIF-image. The second deals with the IIIF-manifest as a collection of digital objects that together form the digital surrogate. The latter fits our database because our interest is in the digital surrogate of the entire article rather than the individual scans. Moreover, there is no interest in different access points; our only objectivel is to provide the link to the manifest. Therefore, the way to include it in our model is to state that an IIIF-manifest is <code>subject</code> of the article in question. 


	{ "@context": "https://linked.art/ns/v1/linked-art.json", 
	"id": "https://dfk-paris.org/example/datarecord/10056", 
	"type": "DigitalObject", 
	"_label": "datarecord ID 10056",
    "subject_of": [{
    		"id": "https://digi.ub.uni-heidelberg.de/diglit/iiif/cicerone1926/canvas/0127.json", 
    		"type": "DigitalObject", 
    		"conforms_to": [{
          	     "id": "http://iiif.io/api/presentation", 
          	     "type": "InformationObject"}], 
                 "format": "application/ld+json;profile=\"http://iiif.io/api/presentation/3/context.json\""}]}


### Quotation

A substantial part of all the records carries quotes from the articles they refer to. This quotes differ in length and are chosen along the individual interests of the researchers. 


	{ "@context": "https://linked.art/ns/v1/linked-art.json", 
	"id": "https://dfk-paris.org/example/datarecord/10056", 
	"type": "DigitalObject", 
	"_label": "datarecord ID 10056",
	"refer_to" : [{
     	 "type": "LinguisticObject",
     	 "_label": "source, what the record is about",
       "referred_to_by" : [{
     	 "type": "LinguisticObject",
     	 "_label": "quotation from the article",
      		"classified_as": [	{
          	"id": "http://vocab.getty.edu/page/aat/300026941",
         	 "type": "Type",
          	"_label": "Quotation"	}],
           "content" : "mehr eine duftige Gabe von einem Verehrer dem großen Meister dargebracht, als ein kühl und sachlich abwägendes, aus der notwendigen zeitlichen und ästhetischen Ferne gesehenes und konzipiertes Werk"; "viele Abbildungen teilweise verunglückt"}]}]}


### Synopsis

Many but not all data records entail an interpretative description of the source(s) in respect to the research question and differ in terms of their form and detail. As that they are not the same as classical abstracts, therefore we prefer to label them as "synopsis", but model them along the propositions of the LADM for abstracts. As sometimes a data record refers to more than one article, the description can't be modelled as a reference to one of the articles. Therefore it is directed to the data entry and not to the text. Dependent on the researcher and not so much to the source(s) the description is held in French or in German. 

The Linked Art Data Model proposes the assignment of an authorship for abstracts. This is an appealing possibility, that would go very well with especially the databases of the "Deutsch-französische Kunstvermittlung", but for deflating the model, the mapping does not make use of it. 


	{ "@context": "https://linked.art/ns/v1/linked-art.json", 
	"id": "https://dfk-paris.org/example/datarecord/10056", 
	"type": "DigitalObject", 
	"_label": "datarecord ID 10056",
	"referred_to_by" : [{
		"type": "LinguisticObject",
       	"_label": "Synopsis by researchers of the article(s)",
       	"classified_as": [{
       		"id": "http://vocab.getty.edu/aat/300026675", 
      		"type": "Type", 
      		"_label": "Synopsis", 
	      	"classified_as": [{
         	 	"id": "http://vocab.getty.edu/aat/300418049", 
          		"type": "Type", 
          		"_label": "Brief Text"}],
          	"language": [{
                 "id": "http://vocab.getty.edu/page/aat/300388306",
                 "type": "Language",
                 "_label": "French"}],	
         	"content":	"Le mouvement pur ne pouvait être représenté, d'une façon gratuite, que par l'art abstrait. (...) Les travaux du Bauhaus comptent parmi les plus intéressantes manifestations de notre époque, d'abord par la qualité des hommes qui y ont travaillé : à côté de Walter Gropius et de Lyonel Feininger, nous retrouvons de grands artistes abstraits, Klee, Kandinsky, Moholy-Nagy ; puis par les idées qui s'y sont développées. Dans l'ordre de l'objet pratique, – le Bauhaus était une sorte d'école-atelier d'art appliqué – une rigoureuse et harmonieuse fonctionnalité. Dans l'ordre esthétique, une volonté de revenir à des formes pures, essentielles, et volontiers abstraites. 26 Kurt Schwitters, qui y exposait sa théorie de Merz : par ces titres, déjà, on voit que les courants les plus importants de l'abstraction nourrissaient les idéaux et les réalisations du Bauhaus. Et comme le Bauhaus possédait une scène d'expérience pour ses recherches dans l'ordre du théâtre et de la chorégraphie, il s'y est créé tout naturellement une forme de ballet abstrait, extrêmement remarquable."}]} ]}


### Text type classification

Some of the sources were classified by the researchers as "text types" based on the (functional) nature of the text, such as obituaries or announcements. Some of the text types in this category were used only by one research team, and some were used by several of the teams. The definition of the types is not given and does not refer to thesauri or to bibliographic information of the sources. Some of the types have a label in French and German, others offer only German.


	{"@context": "https://linked.art/ns/v1/linked-art.json", 
	  "id": "https://dfk-paris.org/example/datarecord/10056", 
	  "type": "DigitalObject", 
	  "_label": "datarecord ID 10056",
	  "referred_to_by" : [{
         "type": "LinguisticObject",
	     "_label": "Textart",
	     "classified_as": [{
    	   "id": "http://vocab.getty.edu/page/aat/300435444", 
    	   "type": "Type", 
    	   "_label": "classification"}],
        "content" : "Nachruf",
      	"language": [{
          	"id": "http://vocab.getty.edu/page/aat/300389318", 
          	"type": "Language", 
          	"_label": "Standard German"}]}]}


### Keywords

Most of the data records are tagged with keywords created by the researchers to designate the main topics of the texts they collected. The creation of the thesauri took them a lot of effort and was discussed and changed throughout the projects without ever achieving satisfactory results. The keywords were profoundly altered by the migration of the data in 2004. Therefore, these keywords are referred to as "topics" now. Some of the keywords have a label in French and in German. Like stated for the synopsis we align the topics to the data entry and not to the text(s).  


	{"@context": "https://linked.art/ns/v1/linked-art.json", 
	  "id": "https://dfk-paris.org/example/datarecord/10056", 
	  "type": "DigitalObject", 
	  "_label": "datarecord ID 10056",
	  "referred_to_by" : [{
         "type": "LinguisticObject",
	     "_label": "Topics",
	     "classified_as": [{
    	   "id": "http://vocab.getty.edu/aat/300311841", 
    	   "type": "Linguistic Object", 
    	   "_label": "topic"}],
        "content" : "Zeichnung",
      	"language": [{
          	"id": "http://vocab.getty.edu/page/aat/300389318", 
          	"type": "Language", 
          "_label": "Standard German"}]},{
          "equivalent": [{
             "id": "http://vocab.getty.edu/aat/300311841",
      		 "type": "Linguistic Object",
             "_label": "topic"}],
            "content" : "Dessin",
            "language": [{
          	"id": "http://vocab.getty.edu/page/aat/300388306", 
          	"type": "Language", 
          "_label": "French (language)"}]}]}


### Persons mentioned by the texts

One of the most important features of the databases is the indexing of people mentioned in the texts. Almost every data entry contains a list of persons. There is no further designation of their role, and so a person may appear as the main character of the article (for example, in an obituary) or as someone who serves as a reference point for the art critics writing the article. 
 
During the curation activity (2021-2022), individuals were referred to authority files (Getty ULAN, GND, VIAF.org) or to entries in Wikidata wherever possible. As a result of the technical capabilities and skills of the researchers at the time, there are approximately 550 individuals who appear in the data with at least two slightly different name variants. All of these variants have been kept as "equivalents" because they often reflect the spelling in the sources, i.e. they have evidential value. 


	{ "@context": "https://linked.art/ns/v1/linked-art.json", 
	"id": "https://dfk-paris.org/example/datarecord/10056", 
	"type": "DigitalObject", 
	"_label": "datarecord ID 10056",
	"refers_to" : [{
		"type": "LinguisticObject",
	   	"_label": "persons mentioned",
	   	"classified_as": [{
	    	   "id": "http://vocab.getty.edu/page/aat/300404668", 
	   	   "type": "Type", 
	    	   "_label": "indexing information" }],
	    "part" : [{
	       "type" : "Name",
	       "_label" : "Person Name (Family name, given-name",
	       "content" : "Millet, Jean-François",             
	       "equivalent": [{
	      		"id": "http://vocab.getty.edu/page/ulan/500012529"},{
	            "id" : "https://www.wikidata.org/wiki/Q148458"}]},{
	       "type" : "Name",
	       "_label" : "Person Name (Family name, given-name",
	       "content" : "Courbet, Gustave",             
	       "equivalent":[{
	      		"id": "http://vocab.getty.edu/page/ulan/500012529"}]}]}]}


### Entire model

The montage of all the parts is stored as separate file and can be also visualized at the JSON-LD playground.


### Summary

The LADM allows to describe the main characteristics in the datasets in a sufficient way. Nevertheless, we needed to extend the model to include the activity <code>curation</code> and then <code>curated_by</code>. Further, modelling articles as members of a journal is as a workaround not entirely convincing. Finally, we would have preferred to include lists of indexed people and keywords in a way that is comparable to the description of <code>visual items</code> in LADM: they enable to indicate that what they show is <code>about</code> something. This concept is coherent to the use of keywords in the databases, we deal with. It also would align well with the indexed persons as their relation to the context of the text shows as stated earlier some variation. But for obituaries or biographical notes an derivate of the concept of <code>representation</code> might also fit. Again these concepts are for the moment only meant for visual items. 

Notwithstanding these shortcomings, the use of LADM shows great potential for advancing interoperability of legacy data in art history. 

It is from our own experience simple enough to be applied by researchers with only a basic understanding of LOD, and allows them to put their data into a format and form that is adapted to the needs of developers. This is a much more far-reaching approach to reusability than simply converting data to JSON format. The intent is that the developer will not be processing this data on behalf of the researcher looking at the data, but will be doing so themselves and for their own interests. Using the LADM enables the user to understand the data without having to read documentation that too often focuses on content issues.


