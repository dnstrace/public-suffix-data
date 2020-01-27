# public-suffix-data

[![Build Status](https://travis-ci.org/mns-llc/suffixer.svg?branch=master)](https://travis-ci.org/mns-llc/suffixer)

A parsed subset of the Public Suffix List for ingestion into custom tools.

### Contents

* public-suffix-list.dat: the copy of the PSL used to generate ...
* icann.json: ICANN suffixes in nested+JSON format
* private.json: Private suffixes in nested+JSON format

### Format

All domains are punycoded from international formats.

The provided nested+JSON files are formatted such that the decoded array is approximately the following - this excerpt pulled from the icann.json datafile:

```
[ "ac" => [
       "%"   => [ ]
       "com" => [
             "%"   => [ ] ]
       "edu" => [
             "%"   => [ ] ]
        ... ]
  "ad" => ...
```

Or in a more comprehensible form: the JSON files provide a multidimensional array structure such that in order to check the validity of a domain, simply work backwards from the TLD. If a given field (say, TLD to start) exists in the keys of the current array, that level is valid. Progress by taking the resultant array from the matched key and moving one level down. Continue until the best remaining match is a wildcard (%). If no real or wildcard match can be made, the domain is invalid.

To determine the registrable domain with reasonable certainty, take the value in the wildcard spot. This is typically but not always correct.

### Last Generator Output
```
ICANN suffixes found: 7329, unique: 7321
Private suffixes found: 1480, unique: 1480
Discrepancy: 8
Obvious punycode errors: 0

Max ICANN suffix depth: 4
Max Private suffix depth: 5

ICANN TLDs: 1527
Private TLDs: 194
```
