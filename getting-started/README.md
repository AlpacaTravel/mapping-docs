[//]: # "Title: Getting Started"
[//]: # "Weight: 1"
[//]: # "Layout: 1-col"
[//]: # "TOC: false"
[//]: # "Keywords: map, geojson, itinerary"

# Mapping

> Alpaca supports a number of mapping technologies and approaches for you to
> present your interactive content produced on the Alpaca platform. Work with
> native formats to present your content exactly the way you want to.

Alpaca provides an environment for developers to work with various mapping
environments to display their content. The alpaca.tech supports a number of
mapping tools, including [Mapbox](/topics/itinerary/Working%20with%20Mapbox/),
[Leaflet](/topics/itinerary/Working%20with%20Leaflet/),
[Google Maps](/topics/itinerary/Working%20with%20Google%20Maps/),
[ArcGIS](/topics/itinerary/Working%20with%20ArcGIS%20Maps%20SDK%20for%20JavaScript/)
and [more](/topics/itinerary/). You can also use
[SVG files](/topics/itinerary/Working%20with%20SVG/) and D3 visualisations.

<iframe src="https://www.alpaca.travel/api/examples/mapbox-gl-js/animate-camera-along-a-trail/index.html"
  style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
/></iframe>

<em>
  Using Mapbox GL environment natively, allowing developers to create their
  own interactions and presentation of content.
  [View source](https://www.alpaca.travel/reference/article/animate-camera-along-a-trail).
</em>

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
