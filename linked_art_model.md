# No HumanmadeObject - the Application of the Linked Art Data Model on the database "Deutsch-Französische Kunstvermittlung"

The franco-german project ""Deutsch-Französische Kunstvermittlung" was carried out from 2000-2003 and aimed to understand and represent the reciprocal perception of the art production from the view point of art critics. One of its by-products was the collection of tagged and often commented contemporaries articles and book chapters within a three-partite relational database (french art critic 1871-195, german art critic 1871-1940 and finally french and german art critic 1945-1960). The database was not openly usable until 2019, than the former research director Thorsten Wübbena published the data via GUI on the website of the DFK Paris.

In 2021 the DFK Paris started a curation activity, that aims to optimize the GUI, enrich the data semantically and to facilitate the use of individual data records for developers. The curation forms part of the research on data reuse in the art history of the DFK Paris.

This document deals with the question of applying the [Linked Art Data Model](https://linked.art). It is roughly structured along informational sequences I observed and separated in the data records that forms the informational objects within the three-partite database. Each part starts with a short characterization of the assumed informational sequence and continues with an expression of the applied linked.art classes and properties in human language. With the latter I follow the approach of the linked.art descriptions of examples. 

The text is introduced by an description of what a data record is in the context of the DFKV data collection. The summary offers a short overview of the main parts of the mapping.

## the data record

A data record represents a digital information object, that collects structured and semi-structured data. A data record consists firstly of the reference to one or more sources with bibliographic informations (always) and a quotation (often) and secondly of keywords (always), a description (often) and the categorization of the source-type (sometimes). Thirdly rights statements and activities are documenting the creation, curation and terms of usage of the data record. There is no entity like a person, a book or a date that forms the spine of the record, but a record represents the information, that the researchers collected and tagged one or more sources as material for their research within one of the three subprojects of the project "Deutsch-französische Kunstvermittlung" (s. for more information [link to project at website DFK](https://dfk-paris.org/de/page/deutsch-franz%C3%B6sische-kunstvermittlung-1871%E2%80%931940-und-1945%E2%80%931960-2389.html)). 

Each data record is part of a data collection within a database which is one part of the general collection/the general database that consists of three parts. All of them are in regard to the data model concordant.
     
### prerequisites for applying linked.art and context of the data set

The prerequisites for applying linked.art on the level of the data record are that, each data record has a URI and all the properties and classes used have to be referred to linked.art. Finally the type of the entire entity - the data record - has to be declared and its context indicated. 

* <code>@context</code> : "https://linked.art/ns/v1/linked-art.json", 
* <code>id</code> : "https://something_like/data/dfk-paris.org/DFKV_10056" 
* is of <code>type</code> : <ode>DigitalObject</code>
* has a <code>_label</code> "data record ID 10056"

* is <code>identified_by</code> an intern ID
  * <code>identifier</code>
    * is <code>classified_as</code> : [
        
        {
          <code>id</code>: "http://vocab.getty.edu/aat/300314626",  
          of <code>type</code>: "Type",
          has <code>_label</code>: "Identification Number"
        }
      ],  
  * with <code>content</code> : "ID_10056"





		{
 		 "@context": "https://linked.art/ns/v1/linked-art.json", 
 		 "id": "https://dfk-paris.org/example/datarecord/10056", 
  		 "type": "DigitalObject", 
  		 "_label": "datarecord ID 10056",
  		 "identified_by" : [
   		  {"type": "Identifier",
     		"_label": "ID database DFKV",
      		"classified_as": [
        		{
         		"id": "http://vocab.getty.edu/aat/300314626",  
          		"type": "Type",
          		"_label": "Identification Number"
      		    }
      				],  
     		"content" : "ID_10056"  
	       }    
 		 ] 
		}
 
 
* the data record is a <code>part_of</code> an <code>Digital Object</code>, that is <code>identified_by</code> <code>content</code> : "Deutsch-französische Kunstvermittlung 1870-1940, Paris"
     
* this dataset is by itself <code>part_of</code> : an "Digital Object", that is <code>identified_by</code> * <code>id</code> : "ulan_nr_for_name" with the <code>_label</code> : "name" and <code>content</code> : "Deutsch-französische Kunstvermittlung 1870-1940 und 1945-1960"




		"part_of" : [
        {"type" : "Digital Object", 
         "_label" : "database", 
         "identified_by" : [
           {"type" : "Identifier",
            "_label" : "name dataset",
            "classified_as" : [
              {"id" : "https://ulan_nr_for_name",
               "type" : "name",
               "_label" : "name of dataset"
         }
            ], "content" : "Deutsch-französische Kunstvermittlung 1870-1940, Paris"
           }
         ],
	         "part_of" : 
	       [
        {"type" : "Digital Object", 
         "_label" : "database", 
         "identified_by" : 
         [
           {"type" : "Identifier",
            "_label" : "name dataset",
            "classified_as" : [
              {"id" : "https://ulan_nr_for_name",
               "type" : "name",
               "_label" : "name of database"
              }
            ], 
            "content" : "Deutsch-französische Kunstvermittlung 1871-1940 und 1945-1960"
          	       }
        	      ]
       			 }
 	     		]
	   		   }
		      ] 


 
*JSON-LD Playground https://tinyurl.com/yzn6obsk*
    
### source(s)

* the datarecord <code>refers_to</code> "article 1"
  * "article 1" is <code>identified_by</code> an identifier 
  * article 1 is a linguistic object 
  * article 1 has a <code>label</code>
  * is <code>classified_as</code> aat:300048715, <code>type:</code> Type. <code>_label</code> article
*   * the article has in our database a "volume_id", that entails pagination and volume number. **It is not yet modelled, how to show the values!**. See for pagination in the linked.art model [https://linked.art/model/document/#pages](https://linked.art/model/document/#pages) 
  * the article is <code>part_of</code> a journal, that has a <code>title</code> and an <code> journal_id</code>   

--

	{
		"@context": "https://linked.art/ns/v1/linked-art.json", 
		"id": "https://dfk-paris.org/example/datarecord/10056", 
		  "type": "DigitalObject", 
		  "_label": "datarecord ID 10056",
		  "refer_to" : [
    {"type" : "LinguisticObject",
     "_label" : "source, what the record is about",
     "classified_as": [
    	{
      		"id": "http://vocab.getty.edu/aat/300048715", 
      		"type": "Type", 
            "_label": "Article"
    	},
        {
          "id": "http://vocab.getty.edu/aat/300435443", 
          "type": "Type", 
          "_label": "Type of Work"
        }
        ],
       "identified_by": [
    	{
         "type": "Name", 
         "content": "Schwankungen der Bilderpreise"
        }, 
    	{
          "type": "Identifier",
     	  "_label": "ID sources in DFKV",
          "classified_as": [
        	{
          	"id": "http://vocab.getty.edu/aat/300314626",  
          	"type": "Type",
          	"_label": "Identification Number"
        	}
      ],  
     "content" : "Volume_ID 7861"  
       }
      ],
 
     "part_of" :  [
       {"type" : "LinguisticObject",
        "_label" : "source of the article",
        "classified_as": 
        [
    	  {
      		"id": "http://vocab.getty.edu/aat/300048715", 
      		"type": "Type", 
            "_label": "Work"
    	  }
       
        ],
        "identified_by" : 
         [
          
          {"type" : "Name",
           "_label" : "Kunstchronik"},
          {
           "type" : "Type",
           "_label" : "intern ID for journal",
            "classified_as": [
              {"id" : "http://vocab.getty.edu/aat/300314626",
               "type" : "Type",
               "_label" : "Identification Number"}], 
            "content" : "journal_id 1439"} 
         ]
       }         
      ]   
     }
    ]
    }
 
*JSON-LD Playground : [tinyurl.com/27bew5u9](tinyurl.com/27bew5u9) *


  * is <code>created_by</code> Person 
	  - the person has an intern <code>identification number</code> and a <code>role</code> ("author")
	  - some of the persons have a name, that is referenced with ULAN or Wikidata
	  - OR some of the intern IDs are <code>equivalent_to</code>
 
 --
 
	 {
	 "@context": "https://linked.art/ns/v1/linked-art.json",
	...//..
	 "created_by": 
	 {
    "type": "Creation", 
    "_label": "Creation of the Article Content", 
    "carried_out_by": [
      {
        "type": "Person", 
        "_label": "Author",
        "identified_by": 
        [
          {"type" : "Identifier",
           "_label" : "intern ID for person name",
           "classified_as": [
            {"id" : "http://vocab.getty.edu/aat/300314626",
             "type" : "Type",
             "_label" : "Identification Number"}], 
           "content" : "239"},
        {"type" : "Name",
         "_label" : "Personen Name",
         "content" : "Frimel, Dr. Th. v."
         
        }
      ],
        "equivalent": 
         [
         {
      		"id": "http://vocab.getty.edu/ulan/500115588", 
      		"type": "Person", 
      		"_label": "Vincent Van Gogh"
          },
           {"assigned_by": 
        	[
        	 {
               "type": "AttributeAssignment"   
      	    }
           ]
          }
         ]		
     }
    ]
    }
    }

*JSON-LD Playground: https://tinyurl.com/562rv3tx*

#### Link to IIIF

  * the article is <code>digitally_shown_by</code>
    * <code>DigitalObject</code>
     * <code>classified_as</code> AAT Type Digital Image
     * has <code>access_point</code>id: IIIFimage, <code>Type DigitalObject</code>
 
     * is <code>digitally_available_via</code> type: <code>DigitalService</code>, has <code>access_point</code> and <code>conforms_to</code>type <code>InformationObject</code> id:iiif Image PI

--

	{ "@context": "https://linked.art/ns/v1/linked-art.json", 
	"id": "https://dfk-paris.org/example/datarecord/10056", 
	"type": "DigitalObject", 
	"_label": "datarecord ID 10056",
	"refer_to" : 
    [
    	{"type" : "LinguisticObject",
     	 "_label" : "source, what the record is about",
     	 "classified_as": 
         [
    		{
      		"id": "http://vocab.getty.edu/aat/300048715", 
      		"type": "Type", 
            "_label": "Article"
    		},
        {
        "subject_of": 
        [
    	{
      	"id": "https://digi.ub.uni-heidelberg.de/diglit/iiif/cicerone1926/canvas/0127.json", 
      	"type": "DigitalObject", 
      	"conforms_to": 
          [
        	{
          	"id": "http://iiif.io/api/presentation", 
          	"type": "InformationObject"
        	}
      	  ], 
      "format": "application/ld+json;profile=\"http://iiif.io/api/presentation/3/context.json\""
         }
         ]
	   }
      ]
	}
	]
	}
 
*JSON-LD Playground: https://tinyurl.com/yjt7atw4*

* **This solution is still under construction, as from the description of linked.art this solution is meant for a manifest, but here it is directed to a canvas.**

### Quotation

A substantial part of all the records carries quotes from the article they refer to. This quotes differs in length and are chosen along the individual interests of the researchers.

--

	{ "@context": "https://linked.art/ns/v1/linked-art.json", 
	"id": "https://dfk-paris.org/example/datarecord/10056", 
	"type": "DigitalObject", 
	"_label": "datarecord ID 10056",
	"refer_to" :
	[
	{
     	 "type": "LinguisticObject",
     	 "_label": "source, what the record is about",
      "classified_as": [
        {
          "id": "http://vocab.getty.edu/aat/300048715",
          "type": "Type",
          "_label": "Article"
        }
      ],
      ...//...
       "referred_to_by" : 
       [
         {
     	 "type": "LinguisticObject",
     	 "_label": "quotation from the article",
      		"classified_as": [
        	{
          	"id": "http://vocab.getty.edu/page/aat/300026941",
         	 "type": "Type",
          	"_label": "Quotation"
        	}
       ],
           "content" : "Lorem ipsum"
    	 }
       ]
      }
      ]
     }

*JSON-LD playground : [https://tinyurl.com/u4wyj95h](https://tinyurl.com/u4wyj95h)*

### Synopsis

Many but not all data records entail an interpretative description of the source(s) in respect to the research question of the project DFKV in general. As that they are not the same as abstracts. They differ in terms of their form and detail. Dependent on the researcher (and not to the source(s) !) the description is held in French or in German. As sometimes a data record refers to more than one article, the description can't be modeled as a reference to one of the articles. Therefore I decided to view the description as "part" of the data set. 

* the datarecord has <code>part</code>s
  * the first part <code>has type</code> : <code>LinguisticObject</code> with <code>_label</code> "Transcription"
    * the first <code>LinguisticObject</code> has a <code>content</code> : "Lorem Ispum usw."

--

	{ "@context": "https://linked.art/ns/v1/linked-art.json", 
	"id": "https://dfk-paris.org/example/datarecord/10056", 
	"type": "DigitalObject", 
	"_label": "datarecord ID 10056",
	...//...
    "part" : 
     [
       {"type": "LinguisticObject",
       "_label": "Synopsis by researchers of the article(s)",
       "classified_as": 
        [
    	{
      	"id": "http://vocab.getty.edu/page/aat/30002667", 
      	"type": "Type", 
      	"_label": "Synopsis", 
      	"classified_as": 
          [
        	{
         	 "id": "http://vocab.getty.edu/aat/300418049", 
          	"type": "Type", 
          	"_label": "Brief Text"
        	}
      	  ]
    	}
    	],
			"content": "Frimmel berichtet über die niedrigen Bilderpreise z.B. für Courbet und Millet. Die Preisentwicklung für Millets Werke wird ausführlich geschildert, bevor der Autor zwischen Kaufwert und künstlerischem Wert unterscheidet und die Prozesse beschreibt, die für die Preisbildungen alter wie moderner Kunst verantwortlich sind." 
       }
       ]
    }

*JSON-LD playground : [https://tinyurl.com/yh9xuy9w](https://tinyurl.com/yh9xuy9w)*

### classification of Textart

Some of the sources have been classified by the researchers as **"Textarten"** due to the (functional) character of the text as obituary or announcement. The types of the category were partly only shared within the team, partly they were used in more than one team. The definition of the types are not stated and do neither related to thesauri nor to bibliographic informations of the sources. Each of the types is identified by a unique identifier (in relation to the class). Some of the types possess a Label in French and German, others only offer German.



* the data record has a <code>part</code>, that is an <code>LinguisticObject</code>
  * the <code>LinguisticObject</code>is of <code>the type</code> <code>category</code> and has the <code>_label</code> "Textart"
  * the <code>content</code> is "Bericht zur Finissage"
  * the <code>content</code> is written in a <code>Language</code>, that is <code>german</code>
    * the LinguisticObject is <code>identified</code> with an <Identifier>, that is the <code>intern ID</code> "Textart_ID 8701"

--

	{ "@context": "https://linked.art/ns/v1/linked-art.json", 
	  "id": "https://dfk-paris.org/example/datarecord/10056", 
	  "type": "DigitalObject", 
	  "_label": "datarecord ID 10056",
	  ...//...
	  "part" : 
	  [
	  {"type": "LinguisticObject",
	  "_label": "Textart",
	  "classified_as": 
    	[
    	 {
    	 "id": "http://vocab.getty.edu/page/aat/300435444", 
    	 "type": "Type", 
    	 "_label": "classification" 
        }
      ],
        "content" : "Bericht",
      	"language": 
          [
           {
          	"id": "http://vocab.getty.edu/page/aat/300389318", 
          	"type": "Language", 
          	"_label": "Standard German"
     	   }
          ],
     "identified_by" : 
     [
      {
       "type": "Identifier", 
       "classified_as": 
        [
         {
           "id": "http://vocab.getty.edu/aat/300314626", 
           "type": "Type", 
           "_label": "Identification Number"
         }
        ], 
       "content": "Textart_ID 9836"
      }
     ]
    } 
    ]
    }

	
*SON-LD playground : [https://tinyurl.com/vby3edvb](https://tinyurl.com/vby3edvb)*
   
 
### Keywords

In the dataset exist two kinds of keywords. Firstly keywords, that indicate to which research topics the data record refers to. As that they are created freely without any references to existing vocabularies our library entries and they were not or almost not controlled. Therefore some of them are just used once, others several times. Each of the keywords has a unique identifier (in relation to its class) and three labels, one in english, one in french and one in german. 

Secondly each person, that is mentioned in the source(s) is documented. Neither the role of the person in the source text(s) - like being the main subject of an article or just someone who is shortly mentioned as participant of an activity described in the article - nor is it obligatory that the persons name signifies in the context of the source(s) a real person or is meant par example as a reference to a style, way of proceeding things connected to a person. The person names were documented in the notation of the source. This includes abbrevations and initials. Sometimes the researchers added informations to disambiguate them. It is very likely, that one person is represented by more than one entry without notion. Each of the person names has a unique identifier (in relation to its class).  

During the curation activity (2021) each person name that could be identified in the Getty ULAN, the Wikidata or the GND has been referenced. To preserve the original notation, entities which refer to the same item in the controlled vocabularies (and databases) were kept as separate entities. Entries with concordant notations have been dissolved, as they were judged as real duplicates. 

#### Topics

* each data record has <code>keywords</code> to assign topics
* each keyword is <code>identified_by</code> an intern <code>Identifier</code>
* some of the keywords are translated, so that they have an <code>LinguisticObejct</code> in the <code>Language</code> "French" as well as in the <code>Language</code> "German"

--

	{
	"@context": "https://linked.art/ns/v1/linked-art.json",
	"id": "https://dfk-paris.org/example/datarecord/10056",
	"type": "DigitalObject",
	"_label": "datarecord ID 10056",
	...//...
	"part": [
    {
      "type": "Identifier",
      "_label": "Topic_ID",
      "content": "8701",
      "equivalent" :
         [ 
    	  {
      		"type": "LinguisticObject", 
      		"classified_as": 
            [
             {  
          		"id": "http://vocab.getty.edu/aat/300435416", 
          		"type": "Type", 
          		"_label": "Description", 
          		"classified_as": 
                [
            	 {
              		"id": "http://vocab.getty.edu/aat/300418049", 
              		"type": "Type", 
              		"_label": "Brief Text"
                 }
          		],
               "content" :  "Kunsthandel: Allgemeines",
               "language": 
               [
          		{
          		"id": "http://vocab.getty.edu/page/aat/300389318", 
         		"type": "Language", 
          		"_label": "Standard German"
          		}
      	 	   ]
        	 }
            ]
          }
        ]
    
      
    },
    {
      "type": "Identifier",
      "_label": "Topic_ID",
      "content": "11284",
      "equivalent" :
         [ 
    	  {
      		"type": "LinguisticObject", 
      		"classified_as": 
            [
             {  
          		"id": "http://vocab.getty.edu/aat/300435416", 
          		"type": "Type", 
          		"_label": "Description", 
          		"classified_as": 
                [
            	 {
              		"id": "http://vocab.getty.edu/aat/300418049", 
              		"type": "Type", 
              		"_label": "Brief Text"
                 }
          		],
               "content" :  "Zeichnung",
               "language": 
               [
          		{
          		"id": "http://vocab.getty.edu/page/aat/300389318", 
         		"type": "Language", 
          		"_label": "Standard German"
          		}
      	 	   ]
        	 }
            ]
          }, 
    	  {
      		"type": "LinguisticObject", 
      		"classified_as": 
            [
             {  
          		"id": "http://vocab.getty.edu/aat/300435416", 
          		"type": "Type", 
          		"_label": "Description", 
          		"classified_as": 
                [
            	 {
              		"id": "http://vocab.getty.edu/aat/300418049", 
              		"type": "Type", 
              		"_label": "Brief Text"
                 }
          		],
               "content" :  "Drawing",
               "language": 
               [
          		{
          		"id": "http://vocab.getty.edu/aat/300388277", 
         		"type": "Language", 
          		"_label": "English"
          		}
      	 	   ]
        	 }
            ]
          },
    	  {
      		"type": "LinguisticObject", 
      		"classified_as": 
            [
             {  
          		"id": "http://vocab.getty.edu/aat/300435416", 
          		"type": "Type", 
          		"_label": "Description", 
          		"classified_as": 
                [
            	 {
              		"id": "http://vocab.getty.edu/aat/300418049", 
              		"type": "Type", 
              		"_label": "Brief Text"
                 }
          		],
               "content" :  "Dessin",
               "language": 
               [
          		{
          		"id": "http://vocab.getty.edu/page/aat/300419444", 
         		"type": "Language", 
          		"_label": "Standard French"
          		}
      	 	   ]
        	 }
            ]
          }
         ]
    	}
       ]
	}

*JSON-LD playground : [https://tinyurl.com/yjr8ug4q](https://tinyurl.com/yjr8ug4q)*


#### Person names mentioned

* the data record has <code>LinguisticObjects</code>, that are keywords
* <code>part</code> of the keywords are <code>person names</code>
* each <code>person name</code> has an intern<code>identifier</code>
* many of the <code>person name</code>s have an <code>equivalent</code> at ULAN or Wikidata

--


	{ "@context": "https://linked.art/ns/v1/linked-art.json", 
	"id": "https://dfk-paris.org/example/datarecord/10056", 
	"type": "DigitalObject", 
	"_label": "datarecord ID 10056",
	...//...
	"part" : 
	 [
	   {"type": "LinguisticObject",
	   "_label": "Keywords - terms",
	   "classified_as": 
	    [
	   	 {
	    	"id": "http://vocab.getty.edu/page/aat/300311841", 
	   		"type": "Type", 
	    	"_label": "keywords" 
	      }
	     ],
	    "part" : 
	    [
	   	 {"type" : "Name",
	      "_label" : "Person Name (Family name, given-name",
	      "content" : "Millet, Jean-François",            
	  	  "identified_by": 
	      [
	       {
	      	"type": "Identifier", 
	      	"_label": "Intern ID for person name", 
	      	"classified_as": 
	        [
	         {
	          "id": "http://vocab.getty.edu/aat/300314626", 
	          "type": "Type", 
	          "_label": "Identification Number"
	         }
	       ], 
	      "content": "PN_ID 1063"
	       }
	    ],  
	       "equivalent": 
	         [
	         {
	      		"id": "http://vocab.getty.edu/page/ulan/500012529", 
	      		"type": "Person", 
	      		"_label": "Millet, Jean Francois (French painter and 	draftsman, 1814-1875)"
	          },
	          {
	            "id" : "https://www.wikidata.org/wiki/Q148458",
	            "type" : "Person",
	            "_label" : "Jean-François Millet"
	          }, 
	           {"assigned_by": 
	        	[
	        	 {
	               "type": "AttributeAssignment"   
	      	    }
	           ]
	          }
	         ]	
	     },
	   	 {"type" : "Name",
	      "_label" : "Person Name (Family name, given-name",
	      "content" : "Courbet, Gustave",            
	  	  "identified_by": 
	      [
	       {
	      	"type": "Identifier", 
	      	"_label": "Intern ID for person name", 
	      	"classified_as": 
	        [
	         {
	          "id": "http://vocab.getty.edu/page/ulan/500010927", 
	          "type": "Type", 
	          "_label": "Identification Number"
	         }
	       ], 
	      "content": "PN_ID 1116"
	       }
	    ],  
	       "equivalent": 
	         [
	         {
	      		"id": "http://vocab.getty.edu/page/ulan/500012529", 
	      		"type": "Person", 
	      		"_label": "Courbet, Gustave (French painter and designer, 1819-1877)"
	          },
	           {"assigned_by": 
	        	[
	        	 {
	               "type": "AttributeAssignment"   
	      	    }
	           ]
	          }
	         ]	
	     }
	    ]    
	   }
	  ]  
	 }

*JSON-LD : [https://tinyurl.com/zhpvv9du](https://tinyurl.com/zhpvv9du)*

### Activities

Their are two main activities, firstly the creation of the datasets within a relation three-partite database, secondly the curation of the data. The curation consists of two campaigns. The earlier was carried out by Thorsten Wübbena and Moritz Schepp and aimed on presenting the data on the website of the DFK Paris. To arrive there, they formatted the datasets into JSON. The second campaign, lead by me, focussed on the FAIRification of thje data. To this end, some of the entities were semantically enriched and the sources were, wherever possible referenced to digital representations. Furthermore the data records have been mapped to the Linked Art Data model. For the sake of usability the activities of the first campaign were not documented in the dataset, as they do not alter the meaning and content of the data.

--

	{
	"@context": "https://linked.art/ns/v1/linked-art.json",
	"id": "https://dfk-paris.org/example/datarecord/10056",
	"type": "DigitalObject",
	"_label": "datarecord ID 10056",
	...//..
	"part_of" :
	[
    {"type": "Activity", 
     "_label": "Curation", 
     "classified_as": 
     [
      {
      "id": "http://vocab.getty.edu/page/aat/300054277", 
      "type": "Type", 
      "_label": "curating",
      "carried_out_by": 
       [
        {
          "type": "Group", 
          "_label": "Curation team"
        }
       ],
      "timespan": 
        {
         "type": "TimeSpan", 
    	 "begin_of_the_begin": "2021-04-01", 
    	 "end_of_the_end": "2021-10-30"
    	 } 
      }
     ],
     "part": [
    {
      "type": "AttributeAssignment", 
      "assigned": {
        "type": "Identifier", 
        "content": "equivalents"
      }, 
      "assigned_property": "identified_by", 
      "assigned_to": {
        "id": "http://vocab.getty.edu/page/aat/300417447",
        "type": "identification numbers and codes", 
        "_label": "References to Getty ULAN, Wikidata etc."
      }   
    },
    {
      "type": "AttributeAssignment", 
      "assigned": 
      {
        "type": "Identifier", 
        "content": "References to digitized articles"
      }
    }
    ]
    },
    {
      "type": "Creation", 
      "carried_out_by": 
       [
        {
          "type": "Person", 
          "_label": "Name of main PI subproject"
        }
       ],
      "timespan": 
        {
         "type": "TimeSpan", 
    	 "begin_of_the_begin": "2000-01-01", 
    	 "end_of_the_end": "2004-01-01"
    	 }
    	}
    ]
    }

*JSON-LD : [https://tinyurl.com/4uy8dttb](https://tinyurl.com/4uy8dttb)*

## Summary of model / main parts

Data record
* <code>part_of</code> data set
* <code>refer\_to</code> source = article 
  * with bibliographic info 
  * <code>subject_of</code> IIIF-manifest
  * <code>referred-to-by</code> a quotation
* has <code>part</code>s
  * description
  * classification of text type
  * keywords
    * subjects 
    * person names mentioned
* is <code>part_of</code> activities

## Find me at the playground
* https://tinyurl.com/yzlyqcd7

## Alert 1: It's important to add license.
	
