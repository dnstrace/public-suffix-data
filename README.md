# public-suffix-data

A parsed subset of the Public Suffix List for ingestion into custom tools.

### Contents

* public-suffix-list.dat: the copy of the PSL used to generate ...
* icann.json: ICANN suuffixes in dnstrace format
* private.json: Private suffixes in dnstrace format

### Format

All domains are punycoded from international formats.

The provided JSON files are formatted such that the decoded array is approximately the following - this excerpt pulled from the private.json datafile:

```
Array(
   "com" => [
      ["amazonaws","s3-eu-west-1","%"],
      ["amazonaws","s3-eu-west-2","%"],
      ["amazonaws","s3-eu-west-3","%"], ...
      ]
   "net" => [ ... ]
    ...
```

The first level of the array contains keys corresponding to TLDs. The second layer of the array contains a suffix-first (inversed) array of values to match, where the % value signals wildcard.

In order to decide if a domain is valid (assuming invalid characters have already been checked for):

1. Explode along "." into an array
2. Reverse sort the array so the TLD is in index 0
3. Match its index-zero value to a TLD
4. Find the longest matching array of suffixes within that TLD

If there is a match, the domain is valid. If not, it is invalid. To determine the registrable domain with reasonable certainty, take the value in the wildcard spot. This is typically but not always correct.

### Last Generator Output

Thu Mar 15 02:02:19 EDT 2018

ICANN suffixes found: 7273   Private suffixes found: 1174

Unique ICANN suffixes: 7265   Unique Private suffixes: 1174

Discrepancy: 8

Obvious punycode errors: 0

Max ICANN suffix depth: 4   Max Private suffix depth: 5

ICANN TLDs: 1551   Private TLDs: 147

