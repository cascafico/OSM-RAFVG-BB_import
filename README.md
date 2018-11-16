# OSM-RAFVG-BB_import

I've found a 600+ rows Bed&Breakfast dataset, available opendata by RAFVG. No geo coordinates. Since hiousenumbers were recently imported from RAFVG dataset, I decided to go for geocoding. To get reliable coordinates I used csvgeocode script attached to nominatim geocoding service. Nominatim requires almost perfect (standardized) odonyms, hence I started openrefine and a reconcile service which comes in a separate jar. Reconcile service needs a csv with authoritative names, which I get from overpass-turbo and some filtering.


### Data preparation
sed -i -e "s/'//" BB.csv 
csvgeocode BBtogeocode.csv   BBgeocoded.csv--handler mapbox --delay 1000 --verbose --url "http://api.tiles.mapbox.com/v4/geocode/mapbox.places/{{INDIRIZZO}},{{CAP}} {{COMUNE}}.json?access_token=xxx"

### Refine
Openrefine > BBgeocoded.json

### checking and removing null elements
cat BBgeocoded.json | grep null | sort -u
sed -i -e '/null/d' -e '/""/d' BBgeocoded.json

### Fix geocede errors
Openrefine facet in bbox
