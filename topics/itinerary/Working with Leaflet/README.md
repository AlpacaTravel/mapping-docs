[//]: # "Title: Leaflet"
[//]: # "Weight: 3"
[//]: # "Layout: 1-col"
[//]: # "TOC: false"

# Leaflet

## The GeoJSON layer

Alpaca Travel Itineraries can be added to leaflet maps through using a
[GeoJSON Layer](https://leafletjs.com/reference.html#geojson).

```javascript
// ... Create a leaflet "map" before here

// Update YOUR_ACCESS_TOKEN and the itinerary/XXX with your details
const url =
  "https://mapping.withalpaca.travel/v1/itinerary/XXX.geojson?accessToken=YOUR_ACCESS_TOKEN";

// Fetch the Itinerary GeoJSON from the mapping service
fetch(url)
  .then(res => res.json())
  .then(data => {
    // Add the data you have loaded into a leaflet GeoJSON layer
    // Refer to the reference documentation for working with styling itineraries
    L.geoJSON(data, {
      // You can filter out what features you want to include
      filter: function(feature, layer) {
        // For instance, we can just include markers
        return feature.properties.class === 'location_marker';
      }

      // You can create circle markers using pointToLayer
      pointToLayer: function(feature, latlng) {
        return L.circleMarker(latlng, {
          radius: 8,
          fillColor: "#ff7800",
          color: "#000",
          weight: 1,
          opacity: 1,
          fillOpacity: 0.8
        });
      },

      // Or style the features
      style: function (feature) {
        // Style your feature here..
        // You can refer to the reference documentation on the structure
        // of features, and what information is available.
      }
    }).bindPopup(function (layer) {
      // Bind information that is available in the geojson feature
      return layer.feature.properties.label;
    }).addTo(map);
  });
```

See More:

- [Using GeoJSON with Leaflet](https://leafletjs.com/examples/geojson/)

- [Working with GeoJSON and Vector Tiles](/topics/itinerary/Working%20with%20GeoJSON%20and%20Vector%20Tiles/README.md)
  An overview to getting started with GeoJSON and Vector Tiles when working with
  itineraries.

- [Alpaca Travel GeoJSON and Vector Tiles Reference](/reference/itinerary/GeoJSON%20and%20Vector%20Tiles/README.md)

## Vector Tiles

Alternatively, you can used vector tiles which optimise data loading through
requesting detail via a tile coordinates and zoom level.

The Vector Tiles are located at the following URL:

```
https://mapping.withalpaca.travel/v1/itinerary/abc/{z}/{x}/{y}.vector.pbf?scheme=tms&accessToken=YOUR_ACCESS_TOKEN
```

Replace "itinerary/abc" in the URL with your own itinerary ID, and replace
"YOUR_ACCESS_TOKEN" with your access token.

See [Leadlet.VectorGrid](https://github.com/Leaflet/Leaflet.VectorGrid).
