# PostGIS

I use this to store lots of geospatial data. 

```bash
docker compose up
```

## Some Notes
https://www.gbif.org/occurrence/download/0111759-210914110416597

```sql
drop table if exists stage.ma_winter;
create table stage.ma_winter (
	gbifID bigint,
	datasetKey char(36),
	occurrenceID text,
	kingdom text,
	phylum text,
	class text,
	_order text,
	family text,
	genus text,
	species text,
	infraspecificEpithet text,
	taxonRank text,
	scientificName text,
	verbatimScientificName text,
	verbatimScientificNameAuthorship text,
	countryCode text,
	locality text,
	stateProvince text,
	occurrenceStatus text,
	individualCount text,
	publishingOrgKey char(36),
	decimalLatitude numeric,
	decimalLongitude numeric,
	coordinateUncertaintyInMeters numeric,
	coordinatePrecision numeric,
	elevation numeric,
	elevationAccuracy numeric,
	depth numeric,
	depthAccuracy numeric,
	eventDate timestamp,
	day integer,
	month integer,
	year integer,
	taxonKey bigint,
	speciesKey bigint,
	basisOfRecord text,
	institutionCode text,
	collectionCode text,
	catalogNumber text,
	recordNumber text,
	identifiedBy text,
	dateIdentified timestamp,
	license text,
	rightsHolder text,
	recordedBy text,
	typeStatus text,
	establishmentMeans text,
	lastInterpreted timestamp,
	mediaType text,
	issue text
);
```


```python
with open('../data/MA_winter_escaped.csv', 'wb') as wh:
    with open('../data/MA_winter.csv', 'rb') as rh:
        wh.writelines((line.replace(b'"', b'') for line in rh.readlines()))
```

1.8 million records took about 500seconds to load in (after escaping the quotes) and 13 minutes to convert lon, lats into points.