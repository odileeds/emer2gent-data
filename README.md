# Emer<sup>2</sup>gent Data Resources
This is an attempt to provide a way to bring together resources/data being used by the [Emer<sup>2</sup>gent Data Alliance](http://www.emergentalliance.org). Each individual organisation should maintain their own index in the [format below](#organisation-index) that exists at a fixed URL somewhere on the web. Each organisation index is then under the control of that organisation. These separate indexes are registered once in a [central index](#central-index).

**Note** - This is a work-in-progress and the format may change.

## Central index
The [index.json](index.json) file in this repository is a central place to define other lists. It contains an object in the format:
```javascript
{
    "example": {                                        // A unique key for the organisation
        "author": "A.N. Other",	                        // The name of the organisation
        "description": "A description of the author"	// A short description
        "url": "https://an.other/",                     // URL of the organisation
        "index": "https://an.other/covid-19/index.json" // The URL of their organisation index file
    },
    .
	.
	.
}
```

### Organisation index

These are JSON files containing a list of `datasets`. Each dataset can contain multiple `resources` (URLs of files/visualisations etc). The organisation index file is of the form:

```javascript
{
	"version": "1.0",    // The version number of the metadata format
	"datasets": []       // An array of datasets ([see below](#dataset))
}
```

### Dataset

An individual dataset's metadata is defined as follows:

```javascript
{
    __"id": "7013c827-f9b8-44da-90a3-1b86eacd4c2b"__,
    "sharing": "public",
    "topics": ["health", "timeline"],
    "tags": ["council housing", "tenant", "stock", "house"],
    "licence": "OGL-UK-3.0",
    "createdAt": "2016-06-02T11:27:08",
    "updatedAt": "2020-04-28T11:10:21.637Z",
    "update_frequency": "Annually",
    "title": "Johns Hopkins COVID-19 Dataset",
    "author": "Johns Hopkins University",
    "author_email": "fakeemail@coronavirus.jhu.edu",
    "url": "https://coronavirus.jhu.edu/",
    "maintainer": "Stuart Lowe",
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
    "dependencies": [{
            "url": "https://raw.githubusercontent.com/odileeds/emer2gent-data/master/metadata/country-code-mapping.json",
            "description": "Country names to ISO code mapping. Requires as data uses non-standard country names."
    }]
}
```