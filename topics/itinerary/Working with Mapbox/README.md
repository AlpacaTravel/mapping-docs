[//]: # "Title: Mapbox JS"
[//]: # "Weight: 1"
[//]: # "Layout: 1-col"

# Mapbox

> Mapbox provides a thoroughly customisable environment for developing
> interactive maps

<iframe src="https://www.alpaca.travel/api/examples/mapbox-gl-js/display-itinerary-on-a-map/index.html"
  style="width:100%; height:400px; border:0; border-radius: 4px; overflow:hidden;"
  ></iframe>

<em>Example of loading an itinerary into Mapbox GL.
[View Source code](https://www.alpaca.travel/reference/article/display-an-itinerary-on-a-map).</em>

Mapbox provides a number of products to assist developers work with interactive
maps. Various mapping clients are provided to cover `web` and `mobile`
development environments.

Alpaca provides data to developers working with Mapbox to make presenting the
content easier.

Developers may consider using `GeoJSON` or the Alpaca hosted `Vector Tiles`
which can be easily added as a source of their map or map style. Additionally,
developers can interact with the GraphQL API which provides access to
interactively query their Itinerary and access geometry through queries.

- **[Working with GeoJSON and Vector Tiles](/topics/itinerary/Working%20with%20GeoJSON%20and%20Vector%20Tiles/README.md)**
  A resource to understand what data is available to incorporate into Mapbox
  maps via the `geojson` or `vector` style source
- **[GraphQL API Documentation](https://github.com/AlpacaTravel/graphql-docs)**
  Documentation to assist developers with querying itineraries or specific
  features for more information

When making requests to either GraphQL or resources hosted on Alpaca, you must
provide your `accessToken`.

## GeoJSON

GeoJSON enables obtaining a full verbose data set for styling. Mapbox can add
GeoJSON directly via adding it to your map style as a data source.

**Adding GeoJSON to mapbox-gl JS**

The Mapbox GL JS API can add a full geojson document directly to the map via the
`addSource` API call.

- [map.addSource() API Reference](https://docs.mapbox.com/mapbox-gl-js/api/map/#map#addsource)

```javascript
map.addSource("itinerary", {
  // Use the source type of 'geojson`
  type: "geojson",
  // Provide the URL to the hosted geojson
  // Note: Update with your Itinerary ID and accessToken
  data: "https://mapping.withalpaca.travel/v1/itinerary/XXX.geojson?accessTokenYOUR_ACCESS_TOKEN",
});
```

**Adding GeoJSON to a Mapbox Style**

When working with a Mapbox Style, you can also add the itinerary `geojson`
directly as a source.

- [Mapbox Style Reference](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#geojson)

```json
"itinerary": {
  "type": "geojson",
  "data": "https://mapping.withalpaca.travel/v1/itinerary/XXX.geojson?accessToken=YOUR_ACCESS_TOKEN"
}
```

Note: You will need to update the above `data` URL with the correct itinerary id
and accessToken.

## Hosted Vector Tiles

Alpaca provides hosted vector tiles via its' CDN. In order to use the vector
tiles, you will need to add a `vector` source and direct it to the `tilejson`
file which contains information about where to obtain the tiles.

**Adding Vector Tiles to mapbox-gl JS**

- [map.addSource() API Reference](https://docs.mapbox.com/mapbox-gl-js/api/map/#map#addsource)

```javascript
map.addSource("itinerary", {
  // Use the source type of 'vector`
  type: "vector",
  // Provide the URL to the hosted tilejson
  // Note: Update with your Itinerary ID and accessToken
  url: "https://mapping.withalpaca.travel/v1/itinerary/XXX.tilejson?scheme=xyz&accessToken=YOUR_ACCESS_TOKEN",
  // Important to include the scheme of 'xyz'
  scheme: "xyz",
});
```

**Adding Vector Tiles to a Mapbox Style**

When working with a Mapbox Style, you can also add the itinerary `vector` tiles
directly as a source.

- [Mapbox Style Reference](https://docs.mapbox.com/mapbox-gl-js/style-spec/sources/#vector)

```json
"itinerary": {
  "type": "vector",
  "data": "https://mapping.withalpaca.travel/v1/itinerary/XXX.tilejson?scheme=xyz&accessToken=YOUR_ACCESS_TOKEN",
  "scheme": "xyz"
}
```

Note: You will need to update the above `data` URL with the correct itinerary id
and accessToken.

## Styling Data

Mapbox maps are styled by first adding `sources` and then adding `layers` which
target features from `sources` and renders them on to the map.

The above section describes common ways of adding the sources to your mapbox
style, but you will need to then understand how to select data from the source
to present the features you desire to show users.

The best place to start is the
[Mapbox examples](https://docs.mapbox.com/mapbox-gl-js/example/) or by refering
to the
[Mapbox style specification](https://docs.mapbox.com/mapbox-gl-js/style-spec/).

Once you become familiar with the concepts of styling, you will want to refer to
**[Working with GeoJSON and Vector Tiles](/topics/itinerary/Working%20with%20GeoJSON%20and%20Vector%20Tiles/README.md)**
to understand what data is available to select and style.

## Default Alpaca Style

Alpaca also offers a default style that can be used to style mapbox out of the
box. You can use the default style to quickly leverage the Mapbox API on top of
an Alpaca map style and data.

```
https://mapping.withalpaca.travel/v1/itinerary/XXX.json?accessToken=YOUR_ACCESS_TOKEN
```

You will need to update the itinerary/XXX with your itinerary ID and your access
Token.

```javascript
mapboxgl.accessToken = "<your mapbox access token here>";
const map = new mapboxgl.Map({
  container: "map", // container ID
  // update the below with your alpaca itinerary id and alpaca access token
  style:
    "https://mapping.withalpaca.travel/v1/itinerary/XXX.json?accessToken=YOUR_ACCESS_TOKEN",
});
```

## Recommended examples for using Mapbox

Mapbox provides a number of examples that can assist developers working to
create and style maps.

- [Add markers](https://docs.mapbox.com/mapbox-gl-js/example/add-a-marker/)
- [Add a popup to a marker](https://docs.mapbox.com/mapbox-gl-js/example/set-popup/)
- [Add lines to a map](https://docs.mapbox.com/mapbox-gl-js/example/geojson-line/)
- [Create a 3D view of terrain](https://docs.mapbox.com/mapbox-gl-js/example/add-terrain/)
- [Trace along a line](https://docs.mapbox.com/mapbox-gl-js/example/live-update-feature/)
- [Animate the camera along a path](https://docs.mapbox.com/mapbox-gl-js/example/free-camera-path/)
- [Animate a path with terrain elevation](https://docs.mapbox.com/mapbox-gl-js/example/query-terrain-elevation/)
