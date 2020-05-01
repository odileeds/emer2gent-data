# Emer<sup>2</sup>gent Data Resources
This is an attempt to provide a way to bring together resources/data being used by the [Emer<sup>2</sup>gent Data Alliance](http://www.emergentalliance.org).

There are many organisations with many different technologies available. The aim is to distribute effort as much as possible and allow individual organisations to maintain their own lists of metadata about their resources - an [organisation index](#organisation-index) - in a common format. Their organisation index should exist at a fixed URL on the web. That might be in a Github repository, on their own site, or somewhere else; as long as the URL doesn't change and is accessible. An organisation only needs to update the [central index](#central-index) once with basic details about their organisation index.

**Note** - This is a work-in-progress and the format may change.

## Central index
The [index.json file in this repository](index.json) is a central place to define other lists. It contains an object in the format:
```json
{
    "unique-id": {                                        
        "author": "A.N. Other",
        "description": "A description of the author",
        "url": "https://an.other/",
        "index": "https://an.other/covid-19/index.json"
    }
}
```

The properties are defined as follows:

* `unique-id` - A unique key for the organisation. This should only be made of [URL-safe characters](http://www.ietf.org/rfc/rfc3986.txt) i.e. ALPHA  DIGIT  `-`, `.`, `_`, `~`. It will be used to namespace IDs of individual datasets.
* `author` - The name of the organisation
* `description` - A short description
* `url` - The URL of the organisation
* `index` - The URL of the organisation's [index file](#organisation-index)

### Organisation index

These are JSON files containing a list of `datasets`. Here is [an example index file for ODI Leeds' COVID-19 resources](https://odileeds.github.io/covid-19/index.json). Each dataset can contain multiple `resources` (URLs of files/visualisations etc). The organisation index file is of the form:

* `version` - The version number of the metadata format (this page uses `1.0`)
* `datasets` - An array of [datasets as defined below](#dataset).

We have created an [initial json schema](schemas/sub-index.json) to provide a full specification and examples are documented below.

Here is a basic example:

```json
{
	"version": "1.0",
	"datasets": []
}
```

### Dataset

An individual dataset's metadata has the following required fields:

* `id` - A unique ID within this index file. This should be persistent and made of [URL-safe characters](http://www.ietf.org/rfc/rfc3986.txt) i.e. ALPHA  DIGIT  `-`, `.`, `_`, `~`.
* `createdAt` - An [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) datetime string of when the dataset was created.
* `title` - The title of the dataset.

The following fields are optional:

* `sharing` - One of `public` (for publicly visible resources), `private` (for resources that are not available), or `alliance` (for resources available to members of the Emer2gent Alliance).
* `topics` - An array of topics from the [topic list](topics.json).
* `tags` - An array of text strings for tagging the dataset. These can be whatever you like.
* `licence` - A text string with the `Identifier` from the [SPDX list of licences](https://spdx.org/licenses/).
* `updatedAt` - An [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) datetime string of when the dataset was last updated. 
* `update_frequency` - Can be one of `Annually, Monthly, Quarterly, Weekly, Daily, Hourly, Real time, One off`.
* `title` - The title of the dataset.
* `author` - The name of the author.
* `author_email` - A contact email address for the author of the dataset.
* `url` - A URL associated with the dataset.
* `maintainer` - The name of the maintainer.
* `maintainer_email` - A contact email address for the maintainer so people can provide feedback.
* `description` - A text description of the dataset.
* `resources` - A list of resources ([see below](#resource)).
* `references` - A list of dependencies ([see below](#reference)).

Let's look at a bare-bones example with the minimum of metadata. This might be useful as a placeholder but wouldn't actually define any resources.

```json
{
	"id": "1",
	"createdAt": "2020-05-01T00:00Z",
	"title": "An example"
}
```

Now let's have a more complete example that has three CSV files and a web-based visualisation as [resources](#resource):

```json
{
    "id": "jh-dashboard",
    "sharing": "public",
    "topics": ["health", "timeline"],
    "tags": ["#COVID-19","data"],
    "licence": "CC0",
    "createdAt": "2016-06-02T11:27:08",
    "updatedAt": "2020-04-28T11:10:21.637Z",
    "update_frequency": "Annually",
    "title": "Johns Hopkins COVID-19 Dataset",
    "author": "Johns Hopkins University",
    "author_email": "fakeemail@coronavirus.jhu.edu",
    "url": "https://coronavirus.jhu.edu/",
    "maintainer": "A. Person",
    "maintainer_email": "fakeemail@coronavirus.jhu.edu",
    "description": "2019 Novel Coronavirus COVID-19 (2019-nCoV) Data Repository by Johns Hopkins CSSE",
    "resources": [{
            "type": "vis",
            "format": "html",
            "title": "COVID-19 United States Cases by County",
            "description": "Data is updated once per day after 8 p.m. Eastern to allow the system to pull county-level data. For the most up-to-date confirmed cases and deaths, please see the COVID-19 Global Map. New York City borough deaths data does not include Probable COVID-19 deaths, as this data is not reported.",
            "url": "https://coronavirus.jhu.edu/us-map"
     },{
            "type": "data",
            "format": "csv",
            "check_size": 3482,
            "temporal_coverage_from": "2020-01-22",
            "temporal_coverage_to": "2020-05-01",
            "title": "Global number of confirmed cases",
            "description": "",
            "url": "https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv"
     },{
            "type": "data",
            "format": "csv",
            "check_size": 3482,
            "temporal_coverage_from": "2020-01-22",
            "temporal_coverage_to": "2020-05-01",
            "title": "Global number of deaths",
            "description": "",
            "url": "https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_deaths_global.csv"
     },{
            "type": "data",
            "format": "csv",
            "check_size": 3482,
            "temporal_coverage_from": "2020-01-22",
            "temporal_coverage_to": "2020-05-01",
            "title": "Global number of recovered patients",
            "description": "",
            "url": "https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_recovered_global.csv"
    }],
    "references": [{
            "url": "https://raw.githubusercontent.com/rolls-royce/EMER2GENT/master/data/sun/geo/country_name_mapping.csv",
            "description": "Country names to ISO code mapping. Required as data uses non-standard country names."
    }]
}
```

### Resource

Your dataset may contain multiple resources such as a visualisation, CSV, JSON, PDF, API etc. The `resources` array lets you add them. The fields are:

* `type` - One of `data` (e.g. for raw or processed data), `vis` (e.g for a visualisation, chart, or dashboard), or `cat` (e.g. for a catalogue of other resources).
* `format` - The type of resource. This should be the file extension in lowercase e.g. `csv`, `pdf`, `xls` etc.
* `title` - A title for the resource.
* `description` - An optional description for the resource. This may explain something specific to this resource.
* `url` - The URL of the resource on the web. 

Here is an example of a visualisation resource:

```json
{
	"type": "vis",
	"format": "html",
	"title": "COVID-19 United States Cases by County",
	"description": "Data is updated once per day after 8 p.m. Eastern to allow the system to pull county-level data. For the most up-to-date confirmed cases and deaths, please see the COVID-19 Global Map. New York City borough deaths data does not include Probable COVID-19 deaths, as this data is not reported.",
	"url": "https://coronavirus.jhu.edu/us-map"
}
```


### Reference

This section can be used to specify other datasets which are linked to this one. For example, some resources may require other datasets or resources in order to be able to make full use of it. For example, the Johns Hopkins COVID-19 Dataset uses non-standard country names. From an analysis point of view, ISO country codes are much better.

The team at Rolls-Royce created an excellent [country name to ISO3166 codes lookup CSV](https://github.com/rolls-royce/EMER2GENT/tree/master/data/sun/geo) - here's an example of that written as a references:

```json
{
	"url": "https://raw.githubusercontent.com/rolls-royce/EMER2GENT/master/data/sun/geo/country_name_mapping.csv",
	"description": "Country name to ISO3166 code mapping, as dataset uses non-standard country names"
}
```
