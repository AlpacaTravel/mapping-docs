# Working with GeoJSON and Vector Tiles

Alpaca provides a GeoJSON version of the mapping data for developers to access
geometry.

## About GeoJSON

> GeoJSON is a format for encoding a bariety of geographic data structures

GeoJSON supports a wide range of geometry types to represent the features of
an itinerary, including `Point` and `LineString`. The objects include additional
properties that provide information related to the itinerary content.

**Example of a GeoJSON feature**

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates" [125.6, 10.1]
      },
      "properties": {
        "class": "location_marker",
        "id": "itinerary/123/location/234",
        "label": "My Itinerary Location"
      }
    }
  ]
}
```

## Vector Tiles

> Vector Tiles are hosted and optimised representations of mapping data broken
> into a series of xyz data sets.

Vector tiles work to optimise the presentation of data by breaking the geometry
into a series of tiles across a coordinate space and zoom level. As the user
interacts with the map, additional fidelity of the data can be progressively
requested, improving the load time to maps.

Data is vectorized, which means that Vector Tiles may not be supported by the
mapping technology that you are leveraging.

## "Itinerary" Introduction

Predominantly, when working with itineraries, the use case relates to showing
the suggested movements of the user across a map. These features include;

- The locations the user will travel to, including locations that are optional
  to visit along the way.
- Travel directions and options for the user to move between those locations,
  such as via `car` or `plane`

When working with GeoJSON, you are able to target specific feature types of the
itinerary and then use feature data to present and style that data.

[Itinerary GeoJSON and Vector Tiles Reference](/reference/itinerary/GeoJSON%20and%20Vector%20Tiles/README.md)

### Feature Types

Common features include `Point` and `LineString` geometry types, identified in
the `geometry.type` field.

You can then further discriminate their type by accessing the `properties.class`
field, which will identify further the type of feature, such as the common
elements of `location_marker` or `directions_path`.

There are a number of additional feature types that are available to describe
and represent further fidelity in your maps, such as representing way points,
preferred directions and progress markers.

### Feature Data

Along with each feature, the `properties` field provides broader access to data
that can be used to further style the presentation of elements. These change
depending on the type of feature.

Location features include data for styling locations, including the common
properties of `properties.label` as well as `properties.location_num` and
`properties.optional` to represent stops along the way.

Direction features include data for styling routes, such as the
`properties.mode` of transport or providing progress markers at certain
percentages along the routes (often to place markers) via the
`properties.percentage` property.

More complex relationships between features, such as hierarchical relationships,
are represented. Fields such as `properties.depth` and nested set properties
of `properties.lft` and `properties.rgt` can assist traversing the itinerary.
This also extends to the use of `properties.segments` to group locations or
`properties.tags` for general tagging of specific content.

### Accessing More Data

Features also include a `properties.id` field, which can be used in combination
with the Alpaca GraphQL API in order to access additional specific content or
data for a feature.

Where information within the itinerary relates to information in a clients own
platform, Alpaca includes the properties `properties.external_ref` and
`properties.external_source` to assist developers in creating interactions with
information sourced from their own applications.

### Vector Layers

Vector Tiles support the grouping of fields into layers. Data is grouped based
on their logical type, such as `locations` or `directions`.

### Preview of Data

Alpaca provides an interactive preview of the mapping data to help identify the
data for your itinerary.

[Preview your data](https://mapping.withalpaca.travel/)
