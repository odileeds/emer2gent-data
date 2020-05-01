# Emer<sup>2</sup>gent Data Resources
This is an attempt to provide a centralised index of all data being used by the [Emer<sup>2</sup>gent Data Alliance](http://www.emergentalliance.org).

**Note** - This is a work-in-progress and the format may change.

## Format
The [index.json](index.json) file in this repository simply contains an array of entries in the format:
```javascript
{
    "name": "A data source",
    "metaURL: "http://website.com/some-metadata.json"
}
```
There is minimal data stored in the index entry - all of the metadata will be stored in the resources' metadata file. The metadata does not have to be stored in this repo, it can be hosted anywhere as long as it has a fixed URL.

See the [metadata folder](metadata/README.md) for a **draft** metadata schema and some  metadata files.