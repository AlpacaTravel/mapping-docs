# Google Maps

> Google Maps provide the Maps Platform for developers to create features from
> the Google Maps platform

Alpaca provides ways to be able to leverage the data from Alpaca within your
Google Map.

## Integration Options

Alpaca provides two main methods for developers to consider integrating their
data on to the Google Maps platform.

The `GeoJSON` data format provides a way to easily add data from the Alpaca
platform to maps. The data contains locations as well as directions that can
be used directly on the maps.

Alternatively, you can leverage the `GraphQL API` that provides access to the
content on the Alpaca platform, including itinerary information and geometry
such as LngLat positions and polylines (that can be summarised).

Developers can also mix the data approaches, and choose to use the data entered
in Alpaca but draw routes from Google platform. To achieve this, data entered
including waypoint information, is avialable for querying via the GraphQL API
and can then be used withing the Maps Platform.

- **[Working with GeoJSON](/topics/itinerary/Working%20with%20GeoJSON%20and%20Vector%20Tiles/README.md)**
  A resource to understand what data is available to incorporate into Google
  Maps Platform via `geojson`
- **[GraphQL API Documentation](https://github.com/AlpacaTravel/graphql-docs)**
  Documentation to assist developers with querying itineraries or specific
  features for more information

When making requests to either GraphQL or resources hosted on Alpaca, you must
provide your `accessToken`.

## GeoJSON

GeoJSON can be easily integrated into the maps API via the `loadGeoJson()` API
call on a map instance.

```javascript
map.data.loadGeoJson(
  "https://mapping.withalpaca.travel/v1/itinerary/XXX.geojson?accessToken=YOUR_ACCESS_TOKEN"
);
```

Note: You will need to update the above URL with the correct itinerary
id and accessToken.
