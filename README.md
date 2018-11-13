sed -e "s/'/ /g" Bed_and_Breakfast.csv > Bed_and_Breakfast_noaportrofo.csv
csvgeocode Bed_and_Breakfast_noaportrofo.csv  --handler mapbox --delay 1000 --verbose --url "http://api.tiles.mapbox.com/v4/geocode/mapbox.places/{{INDIRIZZO}},{{CAP}} {{COMUNE}}.json?access_token=pk.eyJ1IjoiY2FzY2FmaWNvIiwiYSI6ImNqbm4ydHNwZDF2dXgza28zZjU5bDNubnUifQ.TuSsIb0WTBfUsJCGdRZKFg"

cat BBgeocoded-csv.txt.json | grep null | sort -u
sed -i -e '/null/d' BBgeocoded-csv.txt.json 



aggiustare geocoding
