Job Title Service
=============

Table of Contents
_________
- [Request Information](#request-information)
- [Sample Response](#sample-response)
- [Available Taxonomies](#taxonomies)
- [Versioning](#versioning)


# Request Information

HTTP method: GET or POST (form or JSON)

Parameters:

* `taxonomy` (required) : classification taxonomy to use; accepted values are `onet17`, `carotenev3`, and `carotenev3_1`. Complete taxonomy lists can be found [here](https://github.com/cbdr/DataScienceAPITaxonomies/tree/master/JobTitle) (restricted to CBReadOnly). A single title/description may be classified against multiple taxonomies in a single request by providing multiple taxonomies in this parameter, separated by the pipe ("|") character (see example query below).
* `title` (required if description is empty) : job title
* `description` (required if title is empty) : job description

Example: https://api.careerbuilder.com/core/classifier/jobtitle?title=Janitor&taxonomy=carotenev3.1|onet17
# Sample Response
```
{
    "data": {
        "onet17": [
            {
                "title": "Janitors and Cleaners, Except Maids and Housekeeping Cleaners",
                "id": "37-2011.00",
                "confidence": 90
            },
            {
                "title": "First-Line Supervisors of Housekeeping and Janitorial Workers",
                "id": "37-1011.00",
                "confidence": 56
            }
        ],
        "carotenev3.1": [
            {
                "title": "Janitor",
                "id": "37.1",
                "confidence": 1,
                "minor_title": "Building Cleaning and Pest Control Workers",
                "minor_id": "2000"
            }
        ]
    }
}
```

# Taxonomies
Possible taxonomies (with links to full taxonomy results)

| Taxonomy | description |
|----------|--------------|
| [onet17](https://github.com/cbdr/DataScienceAPITaxonomies/blob/master/JobTitle/oNet17.md) | Updated ONets |
| [carotenev3](https://github.com/cbdr/DataScienceAPITaxonomies/blob/master/JobTitle/CaroteneV3.md) | Changes from Carotene v2.2 include 7 removals, 139 updates, and 1,386 new titles.  <br> [CaroteneV2_2ToV3CrossWalk.md](https://github.com/cbdr/DataScienceAPITaxonomies/blob/master/JobTitle/CaroteneV2_2ToV3CrossWalk.md)<br> [Carotenev2.2 to v3 Crosswalk.xlsx](https://github.com/cbdr/DataScienceAPITaxonomies/blob/master/JobTitle/Carotenev2.2%20to%20v3%20Crosswalk.xlsx)|
| [carotenev3.1](https://github.com/cbdr/DataScienceAPITaxonomies/blob/master/JobTitle/CaroteneV3.1.csv) | Changes from Carotene v3 include 4 additions, 78 updates, and 28 removals. Adds disambiguation to v3 and includes minor_title and minor_id fields for hierarchical classification. <br>[Carotenev3 to v3.1 Crosswalk.xlsx](https://github.com/cbdr/DataScienceAPITaxonomies/blob/master/JobTitle/Carotenev3%20to%20v3.1%20Crosswalk.xlsx) |

# Versioning
-----------
JobTitle versions the API contract and taxonomies separately. The API version controls the format of the API call and response. The taxonomy version controls what data is returned for the call. The current API version is 1.0.

Both the Carotene and ONet taxonomies are strongly and immutably versioned. For both systems, the underlying classifiers may occasionally be updated without a version change. This may slightly change the classification results for some inputs, but will not affect the underlying taxonomy data.

Our general versioning strategy is available [here](/Versioning.md).
