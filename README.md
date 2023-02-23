<div align="center">
  <img alt="Developer Documentation" src="https://developer.alpacamaps.com/_media/logo.svg" height="75" width="75" />
</div>

# Alpaca Travel Mapping Documentation

<img alt="Mapping Data" src="./map.png" width="803" height="598" />

> [Alpaca Travel](https://alpaca.travel) offers mapping services for developers
> to build their own interactive travel maps.

Alpaca Travel is a platform focused on supporting travel content creators. In
addition to the embeddable versions of the content, Alpaca offer a set of
services to provide access to the data to build your own maps and applications.

[View the GraphQL API Documentation](https://github.com/AlpacaTravel/graphql-docs)

## Playground

Alpaca provides an interactive client that you can access for resources hosted
on the platform. This can be used to interact with features and identify what
mapping data is available.

- **[Mapping Service](https://mapping.withalpaca.travel/)**
  Interact with mapping resources (Requires API Key)

## Itinerary

Itineraries refers to the broad category of content published on the platform,
including trails, trips and lists.

- **[Working with GeoJSON and Vector Tiles](/topics/itinerary/Working%20with%20GeoJSON%20and%20Vector%20Tiles/README.md)**
  An overview to getting started with GeoJSON and Vector Tiles when working with
  itineraries.
- **[Itinerary GeoJSON and Vector Tiles Reference](/reference/itinerary/GeoJSON%20and%20Vector%20Tiles/README.md)**
  A comprehensive reference for the data available within GeoJSON and Vector
  Tile representations of Itinerary

### Other Topics

- **[Mapbox](/topics/itinerary/Working%20with%20Mapbox/)**
  Building thoroughly customisable maps presenting itineraries using Mapbox
- **[Leaflet](/topics/itinerary/Working%20with%20Leaflet/)**
  Adding itinerary information to Leaflet
- **[Google Maps Platform](/topics/itinerary/Working%20with%20Google%20Maps/)**
  Integrating with Google Maps Platform
- **[ARCGis Maps SDK for JavaScript](/topics/itinerary/Working%20with%20ArcGIS%20Maps%20SDK%20for%20JavaScript/)**
  Working with ARCGis Maps SDK for JavaScript to add a GeoJSONLayer to your
  ARCGis Maps application
- **[QGIS](/topics/itinerary/Working%20with%20QGIS/)**
  Easily view your itinerary data in QGIS by adding a Vector Tile Connection
- **[SVG Data](/topics/itinerary/Working%20with%20SVG/)**
  Working with SVG exports of itineraries such as stylising curved and
  generalised representations of itineraries.

## Additional Hosted Datasets

Alpaca Travel also provides additional hosted vector tile datasets that can be
used to enhance the presentation of your maps, such as displaying markers from
the Australian Tourism Data Warehouse, displaying Tourism Regions or other ABS
data, or loading data from the natural world administrative data.

- **[Australian Tourism Data Warehouse](/sets/Australian%20Tourism%20Data%20Warehouse/)**
  Accessing and presenting map that draw from the ATDW database with frequently
  refreshed data
- **[Australian Tourism Regions](/sets/Australian%20Tourism%20Regions/)**
  Accessing and presenting map that draw tourism regions from the ABS
- **[Australian Bureau of Statistics](/sets/Australian%20Bureau%20of%20Statistics/)**
  Accessing and presenting map information from the ABS dataset, including
  locality/suburbs, postcodes, tourism regions or electoral regions.
- **[Natural Earth](/sets/Natural%20Earth/)**
  Present timezones, countries, regions and other administrative information
  from the natural earth dataset.

## API Key

You will need to obtain your API Key in order to authenticate your application
requests. Resources will need to include `?accessToken=` query parameter with
requests.

## Attribution Requirements

Alpaca require correct attribution for using mapping data. This includes at a
minimum displaying:

- "Made with Alpaca" with a link to https://www.alpaca.travel/
- "&copy; OpenStreetMap" with a link to https://www.openstreetmap.org/about

## Alpaca Travel API for Content

Outside of the data embedded within your itinerary mapping data sets, you can
use the `feature.properties.id` for each feature to obtain additional
information from the Alpaca Travel GraphQL API.

See the the [Alpaca Travel GraphQL API documentation](https://github.com/AlpacaTravel/graphql-docs) for more information on how to request information from the API.
This can also be done using the browser 'fetch' function or alternatively using
a hosted SDK that can be included in your browser to make fetching requests
easier.
