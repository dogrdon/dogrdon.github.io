---
layout: post
title: "Handling Large JSON Files with Streaming"
description: "jq is an amazing tool for querying JSON, but loading large JSON files into memory is often not possible. Fortunately it has an option for streaming JSON without loading it into memory"
category: library-data
tags: [json, metadata, jq, streaming, DPLA, data]
---

<figure>
<img class="blog-post" src="/assets/images/posts/2016/03/stream.gif" alt="gif of json data streaming through jq"/><figcaption>Probably going to want to scroll down before you start reading</figcaption></figure>

### Working With Large JSON 

JSON is the format for moving around data on the web. [jq](https://stedolan.github.io/jq/) is a great command line tool for parsing and querying JSON either from a web resource or a locally stored file. It allows you to query, filter, and transform JSON with very little overhead or setup. It's perfect for quickly finding what you want, or exploring and anylzing data returned from a web service. 

But what if the JSON you want to work with is in a very large file, maybe 500mb or more?

There are a number of reasons why you might be working with a large JSON file rather than pulling it from an API. Perhaps a service provides a full data dump, such as the [Digital Public Library of America](http://dp.la), which provides a [5gb (and expanding) compressed JSON file](http://dp.la/info/developers/download/) of all of its metadata. 

Serving up the entire data store over HTTP is not desirable for many reasons. The ability to provide a full export to JSON is a quick and easy way for a service to provide all its open data to its consumers at once for analysis or building applications.

The default behavior for any utility or software that parses JSON might be to load the entire JSON array into RAM first before being able to parse it. If you've ever tried to do this with a very large JSON file, you know that it will never complete because it will end up hammering your computer's RAM and swap, rendering it unuasable before it can even start parsing the data.

<figure>
<img class="blog-post" src="/assets/images/posts/2016/03/maccrash.jpg" alt="Image of macintosh crash screen"/><figcaption>5gb of JSON to load into RAM? I'll just be over here crashing.</figcaption></figure>

Fortunately jq implemented [the capacity to stream your JSON file](https://stedolan.github.io/jq/manual/#Streaming) to the parser. Instead of loading the entire file up at once, streaming sends the contenst of the file through the parser one item at a time in an "event driven" fashion. As the items pass through, you can filter and select as you go, without compromising your computer's memory. 

### Example Usage

Below are examples for selecting a particular value from each record and for extracting only the items that meet a certain condition (say a specific item format). For these examples I'll refer to the [Digital Public Library of America's bulk download](http://dp.la/info/developers/download). 

#### Quick Introduction to jq

Without streaming, say I wanted to use jq to select all of the titles from an API call to the DPLA for the search term 'computers'.

I can request this from: `http://api.dp.la/v2/items?q=computers&api_key=[PLUS API KEY HERE]`. 

From this, I get in return: 

{% highlight javascript %}
{
  "count": 4121,
  "start": 0,
  "limit": 10,
  "docs": [
    {
      "@context": "http://dp.la/api/items/context",
      "isShownAt": "http://collections.mnhs.org/cms/display.php?irn=10463525",
      "dataProvider": "Minnesota Historical Society",
      "@type": "ore:Aggregation",
      "provider": {
        "@id": "http://dp.la/api/contributor/mdl",
        "name": "Minnesota Digital Library"
      },
      "object": "http://collections.mnhs.org/cms/web5/media.php?thumb=yes&irn=10269009",
      "ingestionSequence": 20,
      "id": "0b1340a232731dd6c54bc63ce91d4396",
      "ingestDate": "2016-03-18T21:54:14.478119Z",
      "_rev": "7-e246af1e802f4d4e64e6d93d4d6899bc",
      "aggregatedCHO": "#sourceResource",
      "_id": "minnesota--http://collections.mnhs.org/cms/display.php?irn=10463525",
      "sourceResource": {
        "title": "Computers",
        "description": "Cutting edge program to acquaint students with computers shared with the Pillsbury Company. Tom Aker, reporter, comments from school grounds.",
        "subject": [
          {
            "name": "Computers"
          },
          {
            "name": "Education Data processing"
          }
        ],
        "rights": "http://www.mnhs.org/copyright",
        "format": "Moving Images",
        "collection": {
          "id": "b97327edc09d4a8daf286afc58bdc4cf",
          "title": "Collections Online",
          "@id": "http://dp.la/api/collections/b97327edc09d4a8daf286afc58bdc4cf"
        },
        "stateLocatedIn": {
          "iso3166-2": "US-MN"
        },
        "@id": "http://dp.la/api/items/0b1340a232731dd6c54bc63ce91d4396#sourceResource",
        "type": "image",
        "date": [
          {
            "displayDate": "Created: 06/06/1966"
          }
        ],
        "creator": [
          "Hubbard Broadcasting Corporation, KSTP television (Channel 5)",
          "Aker, Tom",
          "Smicht, Rallie",
          "Pillsbury Company",
          "Robbinsdale Cooper High School"
        ]
      },
      "admin": {
        "validation_message": "{u'iso3166-2': u'US-MN'} is not of type 'array'",
        "sourceResource": {
          "title": "Computers"
        },
        "valid_after_enrich": false
      },
      "ingestType": "item",
      "@id": "http://dp.la/api/items/0b1340a232731dd6c54bc63ce91d4396",
      "originalRecord": {
        "tags": [
          "dpla"
        ],
        "record": {
          "@context": "http://dp.la/api/items/context",
          "record_hash": "57e2b2b546f19b8c6d14df202907bd1a3fc02e9f",
          "title": "Computers",
          "isShownAt": "http://collections.mnhs.org/cms/display.php?irn=10463525",
          "dataProvider": "Minnesota Historical Society",
          "sourceResource": {
            "title": "Computers",
            "description": "Cutting edge program to acquaint students with computers shared with the Pillsbury Company.  Tom Aker, reporter, comments from school grounds.",
            "subject": [
              {
                "name": "Computers"
              },
              {
                "name": "Education Data processing"
              }
            ],
            "rights": "http://www.mnhs.org/copyright",
            "format": "Moving Images",
            "collection": {
              "title": "Collections Online"
            },
            "stateLocatedIn": {
              "iso3166-2": "US-MN"
            },
            "date": {
              "displayDate": "Created: 06/06/1966"
            },
            "type": "imagemimageoimagevimageiimagenimagegimage imageiimagemimageaimagegimageeimagesimage",
            "creator": [
              "Hubbard Broadcasting Corporation, KSTP television (Channel 5)",
              "Aker, Tom",
              "Smicht, Rallie",
              "Pillsbury Company",
              "Robbinsdale Cooper High School"
            ]
          },
          "provider": "Minnesota Digital Library",
          "object": "http://collections.mnhs.org/cms/web5/media.php?thumb=yes&irn=10269009",
          "identifier": "http://collections.mnhs.org/cms/web5/media.php?thumb=yes&irn=10269009",
          "originalRecord": {
            "family_name_facets": {
              "family_name_facet": [
                "Aker",
                "Smicht"
              ]
            },
            "fulltexts": {
              "fulltext": [
                "Cutting edge program to acquaint students with computers shared with the Pillsbury Company.  Tom Aker, reporter, comments from school grounds.",
                "Transcribed Title: Computers",
                "Film reel",
                "Standard sound aperture, reduced frame",
                "Color Sound on medium Magnetic sound track on film Magnetic stripe sound Original reversal film B wind",
                "KSTP-TV Archive, Minnesota Historical Society",
                "film",
                "moving images"
              ]
            },
            "subject_facets": {
              "subject_facet": [
                "Computers",
                "Education Data processing"
              ]
            },
            "given_name_facets": {
              "given_name_facet": [
                "Tom",
                "Rallie"
              ]
            },
            "event_dates": {
              "event_date": [
                "1966-06-06T00:00:00Z",
                "1966-06-06T23:59:59Z"
              ]
            },
            "subject_texts": {
              "subject_text": [
                "Computers",
                "Education Data processing"
              ]
            },
            "link": "http://collections.mnhs.org/cms/display.php?irn=10463525",
            "family_name_displays": {
              "family_name_display": [
                "Aker",
                "Smicht"
              ]
            },
            "type_displays": {
              "type_display": "Moving Images"
            },
            "name_displays": {
              "name_display": [
                "Hubbard Broadcasting Corporation, KSTP television (Channel 5)",
                "Aker, Tom",
                "Smicht, Rallie",
                "Pillsbury Company",
                "Robbinsdale Cooper High School"
              ]
            },
            "collection_name": "Collections Online",
            "image_link": "http://collections.mnhs.org/cms/web5/media.php?thumb=yes&irn=10269009",
            "given_name_displays": {
              "given_name_display": [
                "Tom",
                "Rallie"
              ]
            },
            "descriptions": {
              "description": [
                "Cutting edge program to acquaint students with computers shared with the Pillsbury Company.  Tom Aker, reporter, comments from school grounds.",
                "Transcribed Title: Computers"
              ]
            },
            "type_texts": {
              "type_text": "Moving Images"
            },
            "name_texts": {
              "name_text": [
                "hubbard broadcasting corporation, kstp television (channel 5)",
                "aker, tom",
                "smicht, rallie",
                "pillsbury company",
                "robbinsdale cooper high school",
                "cooper high school"
              ]
            },
            "event_date_label": "Dates",
            "titles": {
              "title": "Computers"
            },
            "event_display_dates": {
              "event_display_date": "Created: 06/06/1966"
            },
            "family_name_texts": {
              "family_name_text": [
                "aker",
                "smicht"
              ]
            },
            "type_facets": {
              "type_facet": "Moving Images"
            },
            "given_name_texts": {
              "given_name_text": [
                "tom",
                "rallie"
              ]
            },
            "name_facets": {
              "name_facet": [
                "Hubbard Broadcasting Corporation, KSTP television (Channel 5)",
                "Aker, Tom",
                "Smicht, Rallie",
                "Pillsbury Company",
                "Robbinsdale Cooper High School"
              ]
            },
            "subject_displays": {
              "subject_display": [
                "Computers",
                "Education Data processing"
              ]
            }
          }
        },
        "_id": "57e2b2b546f19b8c6d14df202907bd1a3fc02e9f",
        "ingested_at": "2015-12-29T16:24:09Z",
        "provider": {
          "@id": "http://dp.la/api/contributor/mdl",
          "name": "Minnesota Digital Library"
        },
        "collection": {
          "id": "b97327edc09d4a8daf286afc58bdc4cf",
          "title": "Collections Online",
          "@id": "http://dp.la/api/collections/b97327edc09d4a8daf286afc58bdc4cf"
        },
        "import_job_id": 4,
        "import_job_name": "MHS",
        "published": true,
        "record_id": "57e2b2b546f19b8c6d14df202907bd1a3fc02e9f"
      },
      "score": 10.649403
    },
    [...WAY MORE RECORDS HERE...]
  ]
}
{% endhighlight %}

If I wanted to get all of the titles only from that request, I might use:

{% highlight shell %}
curl 'http://api.dp.la/v2/items?api_key=b2e5bb78379ad55ead9a148202c8e5fd&q=computers' | jq '.docs[].sourceResource.title'`
{% endhighlight %}

The result of which would be:

{% highlight shell %}
"Computers"
"on computers"
"Computers"
"Computers"
"Computers"
[
  "Computers"
]
[
  "Computers"
]
"on computers"
"Personal computers"
"Computers, 1958"
{% endhighlight %}

Here I am using a command line utility `curl` to request the resource and then I'm using the `|` or pipe to tell it that I want to send the results of that request to the jq utility for grabbing only the title. 

The grabbing is acommplished by using `.docs[]` to access the entire docs array where the results are provided and then specifying that I want only values for the `title` property of the `sourceResource` object for each item returned from the DPLA for this request. There is a [good tutorial](https://stedolan.github.io/jq/tutorial/) for getting started with jq if you are interested in knowing more.

#### Selecting Using a Stream

<section id="back_1"/>
This is great, but what if I wanted to pull every title for every item in the DPLA and perform some sort of text analysis on it? If I were to download the entire dataset and use jq to extract only the titles with something like 

{% highlight shell %}
zcat < all.json.gz | jq '.[]._source.sourceResource.title' 
{% endhighlight %}

we would have the scenario as described above that our computer's memory would overload and it would probably freeze up indefinitely <b><a href="#notes">[1]</a></b>.

Rather, I can use the `--stream` argument. Though what jq sees when the data are streamed is a little different. I will show the stream equivalent command and then try to explain a little bit of the differences.

{% highlight shell %}
zcat < all.json.gz | jq --stream 'select(.[0][1] == "_source" and .[0][2] == "sourceResource" and .[0][3] == "title") | .[1]'
{% endhighlight %}

<section id="back_2"/>
There's a lot going on here that is different from the load-into-memory jq command <b><a href="#notes">[2]</a></b>.

With streamimg, a record ends up looking more like this to the parser:

{% highlight shell %}
[[0,"_index"],"dpla-20150410-144958"]
[[0,"_type"],"item"]
[[0,"_id"],"getty--GETTY_ROSETTAIE638128"]
[[0,"_score"],0]
[[0,"_source","@context"],"http://dp.la/api/items/context"]
[[0,"_source","isShownAt"],"http://primo.getty.edu/primo_library/libweb/action/dlDisplay.do?vid=GRI&afterPDS=true&institution=01GRI&docId=GETTY_ROSETTAIE638128"]
[[0,"_source","dataProvider"],"Getty Research Institute"]
[[0,"_source","@type"],"ore:Aggregation"]
[[0,"_source","provider","@id"],"http://dp.la/api/contributor/getty"]
[[0,"_source","provider","name"],"J. Paul Getty Trust"]
[[0,"_source","provider","name"]]
[[0,"_source","object"],"http://rosettaapp.getty.edu:1801/delivery/DeliveryManagerServlet?dps_pid=IE638128&dps_func=thumbnail"]
[[0,"_source","ingestionSequence"],6]
[[0,"_source","ingestDate"],"2016-01-09T02:53:07.536775Z"]
[[0,"_source","_rev"],"5-1f33d45f65d30018800e166e0ff93274"]
[[0,"_source","id"],"509667c03617c3f9dabcb5641aec3fe5"]
[[0,"_source","aggregatedCHO"],"#sourceResource"]
[[0,"_source","_id"],"getty--GETTY_ROSETTAIE638128"]
[[0,"_source","admin","validation_message"],null]
[[0,"_source","admin","sourceResource","title"],"Blindman's bluff, c. 1750-1800"]
[[0,"_source","admin","sourceResource","title"]]
[[0,"_source","admin","valid_after_enrich"],true]
[[0,"_source","admin","valid_after_enrich"]]
[[0,"_source","sourceResource","title",0],"Blindman's bluff, c. 1750-1800"]
...<<TRUNCATED FOR SPACE>>
{% endhighlight %}


As we can see here it no longer <i>looks</i> like a JSON obect. Each property of a record gets turned into a `[<path>, <leaf-value>]` as an input for the jq parser. That is, each line is a path to a value in the JSON, which can get rather verbose for very nested values.

So if we are looking for the `title` for each record, we would be interested only in the input: 
{% highlight shell %}
[[0,"_source","sourceResource","title",0],"Blindman's bluff, c. 1750-1800"]
{% endhighlight %}

Our jq streaming query above then does just that. in the `select()` function that we use to query the stream, we are asking: "check if the element at index 1 of the 0 index of the input equals '_source' and index 2 of the 0 index of the input equals 'sourceResource' and index 3 of the 0 index of the input equals 'title' then return the leaf value of that path, which should be 'Blindman's bluff, c. 1750-1800'". 

Written out, it is not compelling as a set of instructions, but hopefully demonstrating what the parser is seeing in streaming mode is helpful to understand why the query is so different.

#### Filtering a Stream

But say that, instead of picking out a particular value, we would rather return only the whole records that have a particular value for one of its properties. In this example, we only want to return the items in the DPLA that are sound recordings, ignoring any thing else that is and image, text, moving image, or physical object. We could do that with: 

{% highlight shell %}
zcat < all.json.gz | jq --stream "fromstream(1|truncate_stream(inputs))" | jq "select(any(._source.sourceResource; .type=="sound"))"`
{% endhighlight %}

In this example I am using one more pipe before selecting the items that I want. I am also using a the `any(generator; condition)` [built-in function](https://stedolan.github.io/jq/manual/#Builtinoperatorsandfunctions), which allows for quickly applying a specific condition (in this case the `type` of the item returned must be 'sound') to a specified input (in this case the `sourceResource` object in the item). 

But before I do that, I want to utilize the `fromstream()` and `truncate_stream()` functions in order to first turn the stream of paths and leaves back into something more like the original JSON object. 

If we look at first item outcome of just this part of the command--before making the select--we see the output as:

{% highlight shell %}
{
  "_type": "item",
  "_id": "getty--GETTY_ROSETTAIE638128",
  "_score": 0,
  "_source": {
    "@context": "http://dp.la/api/items/context",
    "isShownAt": "http://primo.getty.edu/primo_library/libweb/action/dlDisplay.do?vid=GRI&afterPDS=true&institution=01GRI&docId=GETTY_ROSETTAIE638128",
    "dataProvider": "Getty Research Institute",
    "@type": "ore:Aggregation",
    "provider": {
      "@id": "http://dp.la/api/contributor/getty",
      "name": "J. Paul Getty Trust"
    },
    "object": "http://rosettaapp.getty.edu:1801/delivery/DeliveryManagerServlet?dps_pid=IE638128&dps_func=thumbnail",
    "ingestionSequence": 6,
    "ingestDate": "2016-01-09T02:53:07.536775Z",
    "_rev": "5-1f33d45f65d30018800e166e0ff93274",
    "id": "509667c03617c3f9dabcb5641aec3fe5",
    "aggregatedCHO": "#sourceResource",
    "_id": "getty--GETTY_ROSETTAIE638128",
    "admin": {
      "validation_message": null,
      "sourceResource": {
        "title": "Blindman's bluff, c. 1750-1800"
      },
      "valid_after_enrich": true
    },
    "sourceResource": {
      "title": [
        "Blindman's bluff, c. 1750-1800"
      ],
      "extent": "1 image of 1 tapestry",
      "description": [
        "Tapestry Dimensions: H 8'2\" x W 7'5\"",
        "Tapestry Materials/Techniques: unknown",
        "Culture: French",
        "Weaving Center: Aubusson",
        "Ownership History: French  sold to Charles Sternberg 2/7/1966.",
        "In landscape with trees  young man standing blind-folded  others seated, watching the scene; river & buildings in distance",
        "(BRD) string of pearls with spiral garland",
        "A similar tapestry with the same border, albeit composition reversed, is illustrated in Göbel Vol. 2, part 2, ill. 278.",
        "French & Co. stock sheet in archive, 45851",
        "Göbel, Wandteppiche II:2 (1928), Ill. 278",
        "Related Works: Compositionally similar tapestries: GCPA 0243088, 0243090-0243094, 0243096-0243097, 0243089 (composition reversed); compositionally similar tapestry (larger composition), GCPA 0243086"
      ],
      "subject": [
        {
          "name": "Genre: Country Life"
        }
      ],
      "rights": "Digital images courtesy of the Getty's Open Content Program.",
      "@id": "http://dp.la/api/items/509667c03617c3f9dabcb5641aec3fe5#sourceResource",
      "collection": {
        "id": "632c46648b97b7838bcbe3c95509ec23",
        "title": "Study photographs of tapestries",
        "@id": "http://dp.la/api/collections/632c46648b97b7838bcbe3c95509ec23"
      },
      "date": {
        "displayDate": "c. 1750-1800",
        "end": "1800",
        "begin": "1750"
      },
      "type": "image",
      "identifier": [
        "97.P.7",
        "Original DB ID: 3230",
        "Web DB ID: 308146"
      ],
      "creator": "Huet, Jean-Baptiste (French, 1745-1811) (designed after) [painter]",
      "specType": [
        "Photograph/Pictorial Works"
      ]
    },
    "@id": "http://dp.la/api/items/509667c03617c3f9dabcb5641aec3fe5",
    "ingestType": "item",
    "originalRecord": {
      "PrimoNMBib": {
        "record": {
          "control": {
            "sourceid": "GETTY_ROSETTA",
            "sourceformat": "DC",
            "recordid": "GETTY_ROSETTAIE638128",
            "sourcesystem": "Other",
            "sourcerecordid": "IE638128"
          },
          "sort": {
            "creationdate": "1750",
            "author": "Huet, Jean-Baptiste (French, 1745-1811) (designed after) [painter]",
            "title": "Blindman's bluff, c. 1750-1800"
          },
          "addata": {
            "genre": "unknown",
            "btitle": "Blindman's bluff, c. 1750-1800",
            "ristype": "GEN",
            "risdate": "1750",
            "format": "book",
            "date": "1750",
            "au": "Huet, Jean-Baptiste (French, 1745-1811) (designed after) [painter]"
          },
          "search": {
            "addtitle": [
              "Access File Blindman's bluff Image 1 Preservation Master File Blindman's bluff Image 1",
              "Study photographs of tapestries (http://hdl.handle.net/10020/cat373681)",
              "GRI Photo Archive"
            ],
            "scope": "GETTY_ROSETTA",
            "lsr34": "Study photographs of tapestries",
            "subject": "Genre: Country Life",
            "format": "1 image of 1 tapestry",
            "creationdate": "c. 1750-1800",
            "general": [
              "http://hdl.handle.net/10020/97p7_308146",
              "97.P.7",
              "Original DB ID: 3230",
              "Web DB ID: 308146",
              "Study photographs of tapestries (http://hdl.handle.net/10020/cat373681)",
              "GRI Photo Archive",
              "Access File Blindman's bluff Image 1 Preservation Master File Blindman's bluff Image 1",
              "Digital images courtesy of the Getty's Open Content Program."
            ],
            "creatorcontrib": "Huet, Jean-Baptiste (French, 1745-1811) (designed after) [painter]",
            "title": "Blindman's bluff",
            "startdate": "17500101",
            "description": [
              "Tapestry Dimensions: H 8'2\" x W 7'5\"",
              "Tapestry Materials/Techniques: unknown",
              "Culture: French",
              "Weaving Center: Aubusson",
              "Ownership History: French  sold to Charles Sternberg 2/7/1966.",
              "In landscape with trees  young man standing blind-folded  others seated, watching the scene; river & buildings in distance",
              "(BRD) string of pearls with spiral garland",
              "A similar tapestry with the same border, albeit composition reversed, is illustrated in Göbel Vol. 2, part 2, ill. 278.",
              "French & Co. stock sheet in archive, 45851",
              "Göbel, Wandteppiche II:2 (1928), Ill. 278",
              "Related Works: Compositionally similar tapestries: GCPA 0243088, 0243090-0243094, 0243096-0243097, 0243089 (composition reversed); compositionally similar tapestry (larger composition), GCPA 0243086"
            ],
            "searchscope": "GETTY_ROSETTA",
            "sourceid": "GETTY_ROSETTA",
            "enddate": "17501231",
            "lsr08": [
              "Tapestry Dimensions: H 8'2\" x W 7'5\"",
              "Tapestry Materials/Techniques: unknown",
              "Culture: French",
              "Weaving Center: Aubusson",
              "Ownership History: French  sold to Charles Sternberg 2/7/1966.",
              "In landscape with trees  young man standing blind-folded  others seated, watching the scene; river & buildings in distance",
              "(BRD) string of pearls with spiral garland",
              "A similar tapestry with the same border, albeit composition reversed, is illustrated in Göbel Vol. 2, part 2, ill. 278.",
              "French & Co. stock sheet in archive, 45851",
              "Göbel, Wandteppiche II:2 (1928), Ill. 278",
              "Related Works: Compositionally similar tapestries: GCPA 0243088, 0243090-0243094, 0243096-0243097, 0243089 (composition reversed); compositionally similar tapestry (larger composition), GCPA 0243086"
            ],
            "recordid": "GETTY_ROSETTAIE638128",
            "rsrctype": [
              "digital_entity",
              "Textiles - Tapestries",
              "Still image"
            ]
          },
          "browse": {
            "author": "$$DHuet, Jean-Baptiste (French, 1745-1811) (designed after) [painter]$$EHuet, Jean-Baptiste (French, 1745-1811) (designed after) [painter]",
            "subject": "$$DGenre: Country Life$$EGenre: Country Life",
            "title": "$$DBlindman's bluff$$EBlindman's bluff"
          },
          "facets": {
            "topic": "Genre: Country Life",
            "prefilter": "digital_entities",
            "creatorcontrib": "Huet, Jean-Baptiste (French, 1745-1811) (designed after) [painter]",
            "toplevel": "online_resources",
            "frbrtype": "6",
            "frbrgroupid": "687489380",
            "lfc02": [
              "GRI Digital Collections",
              "GRI Photo Archive"
            ],
            "creationdate": "1750",
            "lfc05": "DPLA",
            "rsrctype": "digital_entities"
          },
          "links": {
            "linktorsrc": "$$Tgetty_rosetta_linktorscr$$DDisplay item",
            "thumbnail": "$$Tgetty_rosetta_thumb",
            "lln02": "$$Tgetty_rosetta_linktorscr$$D",
            "openurlfulltext": "$$Topenurlfull_journal"
          },
          "display": {
            "lds29": "http://hdl.handle.net/10020/97p7_308146",
            "lds27": "Digital images courtesy of the Getty's Open Content Program.",
            "subject": "Genre: Country Life",
            "format": "1 image of 1 tapestry",
            "type": "digital_entity",
            "creationdate": "c. 1750-1800",
            "creator": "Huet, Jean-Baptiste (French, 1745-1811) (designed after) [painter]",
            "lds14": [
              "97.P.7",
              "Original DB ID: 3230",
              "Web DB ID: 308146"
            ],
            "lds26": "Still image",
            "title": "Blindman's bluff, c. 1750-1800",
            "source": "GETTY_ROSETTA",
            "lds04": [
              "Tapestry Dimensions: H 8'2\" x W 7'5\"",
              "Tapestry Materials/Techniques: unknown",
              "Culture: French",
              "Weaving Center: Aubusson",
              "Ownership History: French  sold to Charles Sternberg 2/7/1966.",
              "In landscape with trees  young man standing blind-folded  others seated, watching the scene; river & buildings in distance",
              "(BRD) string of pearls with spiral garland",
              "A similar tapestry with the same border, albeit composition reversed, is illustrated in Göbel Vol. 2, part 2, ill. 278.",
              "French & Co. stock sheet in archive, 45851",
              "Göbel, Wandteppiche II:2 (1928), Ill. 278",
              "Related Works: Compositionally similar tapestries: GCPA 0243088, 0243090-0243094, 0243096-0243097, 0243089 (composition reversed); compositionally similar tapestry (larger composition), GCPA 0243086"
            ],
            "lds47": "Collection description",
            "lds34": "Study photographs of tapestries"
          },
          "delivery": {
            "delcategory": "Online Resource"
          },
          "ranking": {
            "booster2": "1",
            "booster1": "1"
          }
        },
        "xmlns": "http://www.exlibrisgroup.com/xsd/primo/primo_nm_bib"
      },
      "RANK": "1.0",
      "sear:GETIT": {
        "deliveryCategory": "Online Resource",
        "GetIt2": "http://1.1.1.1?ctx_ver=Z39.88-2004&ctx_enc=info:ofi/enc:UTF-8&ctx_tim=2016-01-08T17%3A55%3A38IST&url_ver=Z39.88-2004&url_ctx_fmt=infofi/fmt:kev:mtx:ctx&rfr_id=info:sid/primo.exlibrisgroup.com:primo3-Journal-GETTY_ROSETTA&rft_val_fmt=info:ofi/fmt:kev:mtx:book&rft.genre=unknown&rft.atitle=&rft.jtitle=&rft.btitle=Blindman's%20bluff,%20c.%201750-1800&rft.aulast=&rft.auinit=&rft.auinit1=&rft.auinitm=&rft.ausuffix=&rft.au=Huet,%20Jean-Baptiste%20(French,%201745-1811)%20(designed%20after)%20%5Bpainter%5D&rft.aucorp=&rft.volume=&rft.issue=&rft.part=&rft.quarter=&rft.ssn=&rft.spage=&rft.epage=&rft.pages=&rft.artnum=&rft.issn=&rft.eissn=&rft.isbn=&rft.sici=&rft.coden=&rft_id=info:doi/&rft.object_id=&rft_dat=IE638128&rft.eisbn=&rft_id=info:oai/&req.language=",
        "GetIt1": "http://rosettaapp.getty.edu:1801/delivery/DeliveryManagerServlet?dps_pid=IE638128"
      },
      "_id": "GETTY_ROSETTAIE638128",
      "SEARCH_ENGINE_TYPE": "Local Search Engine",
      "ID": "1433634",
      "provider": {
        "@id": "http://dp.la/api/contributor/getty",
        "name": "J. Paul Getty Trust"
      },
      "SEARCH_ENGINE": "Local Search Engine",
      "collection": {
        "id": "632c46648b97b7838bcbe3c95509ec23",
        "title": "Study photographs of tapestries",
        "@id": "http://dp.la/api/collections/632c46648b97b7838bcbe3c95509ec23"
      },
      "sear:LINKS": {
        "sear:thumbnail": "http://rosettaapp.getty.edu:1801/delivery/DeliveryManagerServlet?dps_pid=IE638128&dps_func=thumbnail",
        "sear:openurlfulltext": "http://1.1.1.1?ctx_ver=Z39.88-2004&ctx_enc=info:ofi/enc:UTF-8&ctx_tim=2016-01-08T17%3A55%3A38IST&url_ver=Z39.88-2004&url_ctx_fmt=infofi/fmt:kev:mtx:ctx&rfr_id=info:sid/primo.exlibrisgroup.com:primo3-Journal-GETTY_ROSETTA&rft_val_fmt=info:ofi/fmt:kev:mtx:book&rft.genre=unknown&rft.atitle=&rft.jtitle=&rft.btitle=Blindman's%20bluff,%20c.%201750-1800&rft.aulast=&rft.auinit=&rft.auinit1=&rft.auinitm=&rft.ausuffix=&rft.au=Huet,%20Jean-Baptiste%20(French,%201745-1811)%20(designed%20after)%20%5Bpainter%5D&rft.aucorp=&rft.volume=&rft.issue=&rft.part=&rft.quarter=&rft.ssn=&rft.spage=&rft.epage=&rft.pages=&rft.artnum=&rft.issn=&rft.eissn=&rft.isbn=&rft.sici=&rft.coden=&rft_id=info:doi/&rft.object_id=&svc_val_fmt=info:ofi/fmt:kev:mtx:sch_svc&svc.fulltext=yes&rft_dat=IE638128&rft.eisbn=&rft_id=info:oai/&req.language=",
        "sear:linktorsrc": "http://rosettaapp.getty.edu:1801/delivery/DeliveryManagerServlet?dps_pid=IE638128",
        "sear:lln02": "http://rosettaapp.getty.edu:1801/delivery/DeliveryManagerServlet?dps_pid=IE638128"
      },
      "NO": "10918"
    }
  }
}
{% endhighlight %}

As this is now the input for the `select()` using `any()`, we evaluate the `type` property of the `sourceResource` object from each DPLA item in the stream and only return the items that have a `type` that equals "sound". And we don't crash our systems doing so.

### Conclusion

Streaming serialized data so it can be acted on even if there is a lot of it is [not new](https://en.wikipedia.org/wiki/Simple_API_for_XML). And there are plenty of other tools that can be used to stream JSON data in particular. Libraries in [Python](https://pypi.python.org/pypi/ijson/) and [Ruby](https://github.com/brianmario/yajl-ruby), for example, implement the [YAJL streaming JSON parsing library](https://github.com/lloyd/yajl) from C. But jq is a great tool because it is easily and quickly accessible from the command line, making it perfect for exploring and shaping JSON data on the fly or in a pinch.

The above is only the tip of the iceberg. There is plenty more that can be done with jq and you can explore all of its capabilities at [the documentation](https://stedolan.github.io/jq/manual).

### Notes
<section id="notes"/>
<b>[1]</b> Here I am using the full data dump and I am accessing it locally, so there's a few differences in the command syntax from the intro command. First, I am using a utility called `zcat` on the compressed json file because I just want to send the JSON content to jq, rather than uncompress it to a new file first. Also, the structure for the bulk data download is a little different from what is returned from the DPLA API in that the `sourceResource` object is nested within a `_source` object. More information about the format of the bulk downloads can be found [here](https://digitalpubliclibraryofamerica.atlassian.net/wiki/display/TECH/Database+export+files) [<a href="#back_1">back</a>]

<b>[2]</b> The developers of jq provide a bit of a more technical explanation of streaming in jq [here](https://stedolan.github.io/jq/manual/#Streaming), though I found this a little hard to grasp. I've attempted to describe it here in a bit more casually, but it admitedly lacks technical detail and rigor. [<a href="#back_2">back</a>]
