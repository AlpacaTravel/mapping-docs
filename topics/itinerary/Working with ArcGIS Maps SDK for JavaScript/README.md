[//]: # "Title: ArcGIS Maps SDK for JavaScript"
[//]: # "Weight: 5"
[//]: # "Layout: 1-col"
[//]: # "TOC: false"

# ArcGIS Maps SDK for JavaScript

Alpaca Travel mapping data for Itineraries can be presented using the ESRI
ArcGIS Maps SDK for JavaScript. You can use this SDK as your preferred way of
presenting your interactive map.

## GeoJSONLayer

ArcGIS supports a GeoJSONLayer that can be used to obtain data from your
itinerary and present on the ArcGIS Map.

```javascript
const geojsonLayer = new GeoJSONLayer({
  url: `https://mapping.withalpaca.travel/v1/itinerary/XXX.geojson?accessToken=YOUR_ACCESS_TOKEN`,
  copyright: "made with alpaca",
  popupTemplate: template,
});
```

See More:

- [Working with GeoJSON and Vector Tiles](/topics/itinerary/Working%20with%20GeoJSON%20and%20Vector%20Tiles/README.md)
  An overview to getting started with GeoJSON and Vector Tiles when working with
  itineraries.
- [Alpaca Travel GeoJSON and Vector Tiles Reference](/reference/itinerary/GeoJSON%20and%20Vector%20Tiles/README.md)
- [ArcGIS Maps SDK - GeoJSONLayer Example](https://developers.arcgis.com/javascript/latest/sample-code/layers-geojson/)
- [ArcGIS Maps SDK - GeoJSONLayer API Reference](https://developers.arcgis.com/javascript/latest/api-reference/esri-layers-GeoJSONLayer.html)

## Vector Tile Layer

ArcGIS uses a JSON file describing your vector tiles. The format is different to
the tilejson format and we will add support for this in the future.
