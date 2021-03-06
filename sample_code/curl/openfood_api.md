## JSON API Endpoints

## Products#Index

### Retrieve a Products Listing

Returns a list of products with default paging (50 products per page). It will return paging links and an index of the Nutrient and Image includes, but not the data.

```
curl -i -g -H "Accept: application/vnd.api+json" -H 'Content-Type:application/vnd.api+json' -X GET "https://www.openfood.ch/api/v2/products/972" -H 'Authorization: Token token="[API_KEY]"'
```

### With Includes

#### Images

```
curl -i -g -H "Accept: application/vnd.api+json" -H 'Content-Type:application/vnd.api+json' -X GET "https://www.openfood.ch/api/v2/products?include=images" -H 'Authorization: Token token="[API_KEY]"'
```

#### Nutrients

```
curl -i -g -H "Accept: application/vnd.api+json" -H 'Content-Type:application/vnd.api+json' -X GET "https://www.openfood.ch/api/v2/products?include=nutrients'" -H 'Authorization: Token token="[API_KEY]"'
```

#### Paging

##### Set Page Size

```
curl -i -g -H "Accept: application/vnd.api+json" -H 'Content-Type:application/vnd.api+json' -X GET "https://www.openfood.ch/api/v2/products?page[size]=3" -H 'Authorization: Token token="[API_KEY]"'
```

#### Access a specific page

```
curl -i -g -H "Accept: application/vnd.api+json" -H 'Content-Type:application/vnd.api+json' -X GET "https://www.openfood.ch/api/v2/products?page[size]=20&page[number]=5" -H 'Authorization: Token token="[API_KEY]"'
```


##### Using Page Links

The JSON-API specification describes the inclusion of paging links at the bottom of a response. For example:

```
"links": {
    "self": "https://www.openfood.ch/api/v2/products?page%5Bnumber%5D=1&page%5Bsize%5D=3",
    "next": "https://www.openfood.ch/api/v2/products?page%5Bnumber%5D=2&page%5Bsize%5D=3",
    "last": "https://www.openfood.ch/api/v2/products?page%5Bnumber%5D=4890&page%5Bsize%5D=3"
  }
```

Using Curl as an example

```
curl -i -g -H "Accept: application/vnd.api+json" -H 'Content-Type:application/vnd.api+json' -X GET  "https://www.openfood.ch/api/v2/products?page[number]=2&page[size]=3" -H 'Authorization: Token token="[API_KEY]"'
```

### Retrieve a single Product

#### Call by ID

Add the product ID to the url

```
curl -i -H "Accept: application/vnd.api+json" -H 'Content-Type:application/vnd.api+json' -X GET "https://www.openfood.ch/api/v2/products/972" -H 'Authorization: Token token="[API_KEY]"'
```

## Nutrients

The Nutrients endpoint does not contain paging features.


## Serch by barcodes

```bash
curl -X GET --header "Accept: application/json" --header "Authorization: Token token=[API_KEY]" "https://www.openfood.ch/api/v2/products?barcodes=4104420034563%2C4104420033764"
```

#### Term search against products

```bash
curl -X POST 'https://www.openfood.ch/api/v2/products/_search?pretty' -H 'Content-Type: application/json' -d'
{
  "query": {
    "term" : { "status" : "draft" }
  }
}
'
```

#### Terms search against products

```bash
curl -X POST -H "Accept: application/vnd.api+json" -H 'Content-Type:application/vnd.api+json' "https://www.openfood.ch/api/v2/products/_search?pretty" -H 'Content-Type: application/json' -H 'Authorization: Token token="[API_KEY]"' -d'
{
    "_source": true,
    "query": {
        "constant_score" : {
            "filter" : {
                "terms" : { "barcode" : ["4104420034563", "4104420033764"]}
            }
        }
    }
}
'
```

#### Terms search against nutrients

```bash
curl -X POST -H "Accept: application/vnd.api+json" -H 'Content-Type:application/vnd.api+json' "https://www.openfood.ch/api/v2/nutrients/_search?pretty" -H 'Content-Type: application/json' -H 'Authorization: Token token="[API_KEY]"' -d'
{
    "query": {
        "constant_score" : {
            "filter" : {
                "terms" : { "unit" : ["µg"]}
            }
        }
    }
}
'
```
