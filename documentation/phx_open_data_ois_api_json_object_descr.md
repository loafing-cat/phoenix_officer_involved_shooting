# Phoenix Open Data API Response Documentation

## Overview

This document provides a concise explanation of the JSON object returned by the Phoenix Open Data API in response to a data query. The API response contains various components, each serving a specific purpose.

## JSON Object Structure

The API response JSON object consists of the following key components:

1. **help**: URL for accessing help documentation about the `datastore_search` action.

2. **success**: A boolean indicating whether the request was successful (`True`) or not (`False`).

3. **result**: The main payload of the response, containing the following subcomponents:

   - **include_total**: A boolean indicating whether the total number of records is included in the response.
   
   - **limit**: The maximum number of records returned in the response.
   
   - **records_format**: Format of the records, typically set to 'objects'.
   
   - **resource_id**: Unique identifier of the queried resource.
   
   - **total_estimation_threshold**: Threshold for total estimation.
   
   - **records**: An array containing the retrieved records as dictionaries.
   
   - **fields**: Metadata about the fields present in the records.
   
   - **_links**: Links for navigation, including start and next page links.
   
   - **total**: Total number of records matching the query criteria.
   
   - **total_was_estimated**: A boolean indicating whether the total count was estimated.

## Usage

To utilize the data returned by the API response:

- Access the records using `response.json()['result']['records']`.
- Extract specific fields or values by traversing the JSON object using keys.
- Utilize the `total` field to know the total number of records matching the query.
- Navigate through pages of results using the provided links in `_links` if pagination is required.

## Example

```python
import requests

api_url = "https://www.phoenixopendata.com/api/3/action/datastore_search?resource_id=24fe89fb-9d4f-4fba-8b40-9330a5f7d9e7&limit=3"
response = requests.get(api_url)
data = response.json()

# extract records from json object (what we're interested in)
records = data['result']['records']

# extract specific fields
for record in records:
    print(record['DATE'], record['LOCATION'])

# extract and print total number of records in database
total_records = data['result']['total']
print("Total records:", total_records)
