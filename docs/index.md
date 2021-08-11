site_name: MkLorum

#
## Places API

What you will learn:

- [Overview](#overview)
- [API Authentication](#aPI-authentication)
- [GraphiQL Explorer](#graphiQL-explorer)
- [SafeGraph Place API Query parameters](#safeGraph-place-aPI-query-parameters)
- [Places API Examples](#places-aPI-examples)
- [Throttling and Rate Limit](#throttling-and-rate-limit)




<hr>


### Overview

The SafeGraph Places API (beta) is useful for retrieving information about a point of interest (POI) using the Placekey or the location name. Additionally, you can search for POI by brand, NAICS code, or address.

If you require any additional attributes or functions, please contact api@safegraph.com.

### API Version

The Places API returns versioned data. SafeGraph updates its Places data on a monthly basis. Check the version attribute in each response to determine which monthly release the response data comes from.

<hr>

## API Authentication

#### Getting an API Key

SafeGraph uses a single API key to authenticate requests for all of their API connections. To generate an API key, follow these steps:

1. Visit https://shop.safegraph.com

2. Create an account with SafeGraph. For exsiting user, click **Log In**.

3. Click the button **Create an API Key**.

#### Using curl

    curl 'https://api.safegraph.com/v1/graphql' \
    -H 'apikey: {YOUR_API_KEY}' \
    -H 'content-type: application/json' \
    --data-raw '{
	"query":"query {\n  place(placekey: \"225-222@5vg-7gs-t9z\") {\n\t\tsafegraph_core {\n\t\t\tlocation_name\n\t\t\ttop_category\n\t\t\tstreet_address\n\t\t\tcity\n\t\t\tregion\n\t\t\tlatitude\n\t\t\tlongitude\n\t\t}\n\t}\n}\n"
    }' 


#### Passing the API Key

The API key header is used to authenticate requests by passing the API key.

    header

    apikey: {YOUR_API_KEY}

<hr>

## GraphiQL Explorer

The GraphiQL Explorer is the easiest approach to learn the behavior of safeGraph API. You can view and understand the format for your inputs and desired outputs. Insert your API key to begin to submit queries and to view the self-generated documentation in the right hand Docs pane.

At any time, press Shift+Space to display a list of possible inputs for your current syntax.

#### Sample Request and Response

To test the API, copy and paste your API key into the **API Key** area and click the **Rounded play** icon.


    query {
      place(placekey: "222-222@5qw-shj-7qz") { 
		placekey 
    safegraph_core {
      location_name
      street_address
			city
      region
      postal_code
      iso_country_code
    }
      }
    }

<hr>

## SafeGraph Place API Query parameters

The following queries are supported by a SafeGraph API

#### Placekey

Retrieves information based on palcekey. Click [here](#places-aPI-examples) for example.

    
    query {
    place(placekey: "222-222@5qw-shj-7qz")

**NOTE :** 

  - **This version of the API supports only Placekeys with a POI encoding. Support for Placekeys with only the address encoding or the Where part is coming soon!**

  - **For Placekeys with only the Where Part (e.g. @5vg-7gq-tvz ) or only the Address Encoding (e.g. 223@5vg-7gq-tvz), the API will return an error.**




#### Location Name + Address

Retrieves information based on location name and address. Click [here](#getting-place-details-by-location-name-+-address) for example.

    (query: {
			location_name: "Taco Bell", 
			street_address: "710 3rd St", 
			city: "San Francisco", 
			region: "CA", 
			iso_country_code: "US"
		})


<hr>

## Places API Examples

### Single Look Up - Place( )

Examples of queries that make use of the place() query type. Submit unique identifiers for a given place and request data from the SafeGraph Core, Geometry, or Patterns data sets.

###### Getting Place Details by Placekey

    query {
      place(placekey: "222-222@5qw-shj-7qz") { 
		placekey 
    safegraph_core {
      location_name
      street_address
	  city
      region
      postal_code
      iso_country_code
    }
    }
    }

###### Example code:    

    curl 'https://api.safegraph.com/v1/graphql' \
    -H 'apikey: {YOUR_API_KEY}' \
    -H 'content-type: application/json' \
    --data-raw '{
	"query":"query {\n  place(placekey: \"225-222@5vg-7gs-t9z\") {\n\t\tsafegraph_core {\n\t\t\tlocation_name\n\t\t\ttop_category\n\t\t\tstreet_address\n\t\t\tcity\n\t\t\tregion\n\t\t\tlatitude\n\t\t\tlongitude\n\t\t}\n\t}\n}\n"
    }   



### Getting Place Details by Location Name + Address

Submit a name and address pairing and request information back from the SafeGraph Core, Geometry or Patterns data sets. This is useful for retrieving additional attributes for places within your existing data.

    query {
	place(query: {
			location_name: "Taco Bell", 
			street_address: "710 3rd St", 
			city: "San Francisco", 
			region: "CA", 
			iso_country_code: "US"
		}) { 
		placekey 
		safegraph_core {
			location_name
			street_address
			postal_code
			phone_number
			category_tags
		}
	}
    }

<hr>

## Throttling and Rate Limit

#### Pay-as-you-go Pricing

The Places API is billed by the number of data records returned, with each record costing $0.05 USD. A single API request will be billed separately for each record returned. 

**NOTE: Repeated queries for the same data will count as separate billable records.**


#### Rate Limits

The rate limit to the Places API is 1000 requests per minute, and 100 requests per minute for the bulk requests. For requests that exceed this limit, an HTTP 429 response code will be given.   

<hr>

## Terms of Use

You may store the data from this API. But you may not expose the data in its current form or substantially similar form. For more information, please refer to the Data License Agreement.

If you would like to display Places API data in your app, please contact api@safegraph.com.
