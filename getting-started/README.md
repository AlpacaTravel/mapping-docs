[//]: # "Title: Getting Started"
[//]: # "Weight: 1"
[//]: # "Layout: 1-col"
[//]: # "TOC: false"
[//]: # "Keywords: map, geojson, itinerary"

# Mapping

Alpaca supports a number of mapping technologies and approaches for you to
present your interactive content.

## Endpoint URLs

Those familiar with working with maps will be interested in knowing some various
datasets for obtaining information.

<aside class="info">
  Update the URL and substitute `itinerary/XXX` with the ID of your itinerary.
  All requests must be authenticated using `?accessToken=ACCESS_TOKEN` 
  substituting your access token as appropriate.
</aside>

| Type + Description                                                                                              | URL                                                         |
| --------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------- |
| **Manifest**<br/>A JSON file format containing URL's and cameras to be used to assist identify initial viewport | https://mapping.withalpaca.travel/v1/itinerary/XXX.json     |
| **GeoJSON**<br/>FeatureCollection JSON that contains all the individual elements of an itinerary to style       | https://mapping.withalpaca.travel/v1/itinerary/XXX.geojson  |
| **Vector Tiles**<br/>Optimised vectors loaded on demand for performance                                         | https://mapping.withalpaca.travel/v1/itinerary/XXX.tilejson |
