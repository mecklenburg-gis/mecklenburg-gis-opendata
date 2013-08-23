#! /bin/sh

files=`find . -type f | egrep '\.geojson$'`
file_count=0
failures=()

for file in $files
do
    echo 'Testing '$file
    (( file_count += 1 ))
    result=$(curl -X POST --data @$file $data http://geojsonlint.com/validate 2>/dev/null)
    if [ "$result" = "{\"status\": \"ok\"}" ]; then
        echo "    Valid GeoJSON"
    else
        echo "    Invalid GeoJSON"
        failures+=($file)
    fi
done

error_count="${#failures[@]}"
echo $file_count files checked. $error_count failures.

if [ "$error_count" = 0 ]; then
    exit 0
else
    exit 1
fi