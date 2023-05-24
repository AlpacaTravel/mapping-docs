[//]: # "Title: HERE Maps API for JavaScript"
[//]: # "Weight: 4"
[//]: # "Layout: 1-col"
[//]: # "TOC: false"

# HERE Maps API for JavaScript

It is possible to use the HERE Maps API for JavaScript.

## GeoJSON Data display

You can refer to the documentation for covering data display using the GeoJSON
file format.

```javascript
// ... Initialize your map

// Update YOUR_ACCESS_TOKEN and the itinerary/XXX with your details
const url =
  "https://mapping.withalpaca.travel/v1/itinerary/XXX.geojson?accessToken=YOUR_ACCESS_TOKEN";

// Create GeoJSON reader which will down the specified file from Alpaca Travel
const reader = new H.data.geojson.Reader(url, {
  style: function (mapObject) {
    // Parsed geo object can be styled using setStyle method
    // Refer to styling at the here.com documentation
  },
});

// Start parsing the file
reader.parse();

// Add layer which shows GeoJSON data on the map
map.addLayer(reader.getLayer());
```

See More:

- [Working with GeoJSON and Vector Tiles](/topics/itinerary/Working%20with%20GeoJSON%20and%20Vector%20Tiles/README.md)
  An overview to getting started with GeoJSON and Vector Tiles when working with
  itineraries.
- [Alpaca Travel GeoJSON and Vector Tiles Reference](/reference/itinerary/GeoJSON%20and%20Vector%20Tiles/README.md)
- [HERE.com Maps API for JavaScript - GeoJSON Data display](https://developer.here.com/documentation/examples/maps-js/data/display-geojson-on-map)
