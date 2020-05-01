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

These are JSON files containing a list of `datasets`. Each dataset can contain multiple `resources` (URLs of files/visualisations etc).

See the [metadata folder](metadata/README.md) for a **draft** metadata schema and some  metadata files.
