---
name: Alpaca Itinerary GeoJSON/Tiles Reference (v1)
generated: Thu Feb 17 2022
---

## Overview

**Alpaca Itinerary** Tileset and GeoJSON formats include geometries for plotted itineraries for locations, directions and route segments. These provide access for you to create your representation of the itinerary within your mapping platform or application.

### Attribution

When you publicly display maps that use Alpaca Itinerary vector tiles or geojson data, you must display proper attribution.

### IDs

Each feature contains `feature.id`, which assists you in interacting with features using products such as Mapbox. Also often included is `feature.properties.id` which supplies you with Alpaca identifiers in order to further select additional data about that feature from our API.

In some cases, we provide `feature.properties.external_ref` and `feature.properties.external_source` in order for authors to attach other external platform identifiers to assist connecting data with data that may appear in another platform of choice.

## Data Stability

Similarly to other vector tile products (such as Mapbox Streets v8 ❤️), we are following similar goals behind the Alpaca Itinerary v1 data set to preserve compatability with styling or other uses of data properties.

Here are our goals;

- Layers
  - Preserve existing layers
  - Add new layers that could contain additional features from itineraries
- Fields
  - Preserve existing fields
  - Add new fields where additional use cases or feature data is advantageous
    to be included
- Field values
  - The meaning of existing values will not change
  - Values of specific features may change to correct errors or other real-world
    updates (such as changes in underlying data provided to us)
  - New values may be added
  - `null` values will be noted, and fields that are optional will be marked so.
    `null` or optional values should not replace existing fields that have
    not allowed it prior

## Common Attributes

The specification includes a number of feature attributes that can be common to more than one feature type.

### Hierarchy

Attributes provide a means of querying hierarchical relationships as well as ordering between sibling elements

| Value                           | Description                                     |
| ------------------------------- | ----------------------------------------------- |
| `lft` number <br>Example: `5`   | Left outermost value                            |
| `rgt` number <br>Example: `6`   | Right outermost value                           |
| `depth` number <br>Example: `0` | The depth of the element, relative to ancestors |

### Location Numbering

Attributes to assist presenting position numbers assigned to locations

| Value                                                   | Description                                                          |
| ------------------------------------------------------- | -------------------------------------------------------------------- |
| `list_pref` string _optional_<br>Example: `"unordered"` | Any associated list presentation preference applied to this location |
| `location_num` number _optional_<br>Example: `2`        | The location number, relative to the sibling locations               |
| `location_num_dfs` number _optional_<br>Example: `9`    | The accumulative location number for the overall itinerary           |

### Node Reference

Attributes to assist reference more information from the Alpaca GQL

| Value                                                   | Description                        |
| ------------------------------------------------------- | ---------------------------------- |
| `id` string <br>Example: `"itinerary/XXX/location/XXX"` | The Alpaca related node identifier |

### External Identifiers

Attributes to identify this feature in a developers external platform

| Value                                                                       | Description                                       |
| --------------------------------------------------------------------------- | ------------------------------------------------- |
| `external_ref` string _optional_<br>Example: `"myplatform-UUID"`            | Reference identifier in external platform, if any |
| `external_source` string _optional_<br>Example: `"myplatform-section-UUID"` | Reference source in external platform, if any     |

### Itinerary Segments

Reference assignments to itinerary segment identifiers

| Value                                     | Description                                                           |
| ----------------------------------------- | --------------------------------------------------------------------- |
| `segments` text[] <br>Example: `["UUID"]` | A collection of assigned segment identifiers for this feature, if any |

### Icon

Attributes that describe the associated itinerary icon

| Value                                                         | Description                  |
| ------------------------------------------------------------- | ---------------------------- |
| `icon` text _optional_<br>Example: `"itinerary/XXX/icon/YYY"` | The id of the itinerary icon |

### Content

Attributes that contain content supplied by the user

| Value                                                          | Description                                    |
| -------------------------------------------------------------- | ---------------------------------------------- |
| `label` text _optional_<br>Example: `"Mavis the Grocer"`       | The primary label associated with this feature |
| `tags` text[] _optional_<br>Example: `["a tag","another tag"]` | Any assigned user tags                         |

### Viewport Adjustments

Attributes that describe any adjustments for the camera when focusing on this feautre

| Value                                         | Description         |
| --------------------------------------------- | ------------------- |
| `bearing` number _optional_<br>Example: `270` | Bearing, from 0-360 |
| `pitch` number _optional_<br>Example: `60`    | Pitch, from 0-60    |
| `zoom` number _optional_<br>Example: `17`     | Zoom, from 0-20+    |

### Feature Flags Behaviour

Attributes that can help describe interactions with this feature, such as omitting it from a list, map or providing further detail

| Value                                               | Description                                                                                            |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| `flags` text _optional_<br>Example: `["omit-list"]` | A collection of keys relating to which behaviours should be omitted when interacting with this feature |

### Collection Position

Attributes that assist contextualise the ordering of this feature with other collection results

| Value                            | Description                                                 |
| -------------------------------- | ----------------------------------------------------------- |
| `index` number <br>Example: `3`  | The index of this element within the collection (0 indexed) |
| `length` number <br>Example: `4` | The total length of the collection this feature is part of  |

### Progress

Attributes to describe progress along a feature, such as breaking up a path line string into various percentage of length

| Value                                 | Description                                                         |
| ------------------------------------- | ------------------------------------------------------------------- |
| `percentage` number <br>Example: `50` | Percentage progress along this feature (Values: 0, 25, 50, 75, 100) |

### Distance

Attributes to assist presenting the distance of the linestring feature

| Value                                | Description        |
| ------------------------------------ | ------------------ |
| `distance` number <br>Example: `400` | Distance in meters |

### Duration

Attributes relating to the expected duration to travel this feature

| Value                                             | Description                   |
| ------------------------------------------------- | ----------------------------- |
| `duration_min` number _optional_<br>Example: `40` | Minimum duration (in minutes) |
| `duration_max` number _optional_<br>Example: `40` | Maximum duration (in minutes) |

### Travel Mode

Attributes to describe the mode of transportation used in this feature

| Value                            | Description                                                                            |
| -------------------------------- | -------------------------------------------------------------------------------------- |
| `mode` enum <br>Example: `"car"` | A series of values to describe the mode of transport (e.g. foot, car) for this feature |

### Multi-modal Travel Properties

Describes when multiple modes of transport are used in Itinerary Directions

| Value                                               | Description                                                                       |
| --------------------------------------------------- | --------------------------------------------------------------------------------- |
| `multi_modal` boolean _optional_<br>Example: `true` | Whether multiple modes of transport are used to describe the itinerary directions |

### RouteSegment Travel Mode

Attributes to describe the aggregated route segment travel modes

| Value                                                      | Description                                                                                                |
| ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `route_segment_modes` enum[] <br>Example: `["car","foot"]` | A collection of values to describe all modes of transport used within the associated RouteSegment features |

### RouteSegment / ItineraryDirections Relationship

Attributes to describe the relationship of route segments to their directions counterpart

| Value                                                             | Description                                                          |
| ----------------------------------------------------------------- | -------------------------------------------------------------------- |
| `directions` string <br>Example: `"itinerary/XXX/directions/XXX"` | The node reference ID of the associated Itinerary Directions feature |

### ItineraryDirections / RouteSegment Relationship

Attributes to describe the relationship of directions to the route segments counterpart

| Value                                                                                   | Description                                                   |
| --------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| `route_segment` string <br>Example: `"itinerary/XXX/directions/XXX/segment/unstable.0"` | The node reference ID of the associated Route Segment feature |

### Origin / Destination Node Reference

Attributes to create relationships to Locations

| Value                                                                 | Description                                       |
| --------------------------------------------------------------------- | ------------------------------------------------- |
| `origin` string _optional_<br>Example: `"itinerary/XXX/location/XXX"` | The origin Itinerary Location Node Reference      |
| `dest` string _optional_<br>Example: `"itinerary/XXX/location/XXX"`   | The destination Itinerary Location Node Reference |

### Optional Stop information

Attributes to assist presenting optional locations

| Value                                            | Description                                                                  |
| ------------------------------------------------ | ---------------------------------------------------------------------------- |
| `optional` boolean _optional_<br>Example: `true` | Whether this feature has been indicated as an optional stop on the itinerary |

## GeoJSON Reference

Features are container within the GeoJSON `FeatureCollection` `features` array. The `bbox` property often included provide a bounding box calculation for the features.

```js
{
  type: 'FeatureCollection',
  features: [...],
  bbox: [1, 1, 2, 3]
}
```

Each feature of the itinerary has a number of GeoJSON `Feature` objects. The object contains a number of properties, including an `id`, `geometry`, `properties` and often the `bbox` property.

The `geometry` property provides an encoding of geometry depending on the geometry type, such as `point`, `linestring`, `multilinestring` or `polygon`. An example of of a geometry would be `{ type: 'point', coordinates: [1, 1] }`).

The `properties` property provides a number of attributes about the feature corresponding to the type of feature (differentiated by the `class` attribute).

```js
{
  id: 123,
  type: 'Feature',
  geometry: { ... },
  properties: { ... },
  bbox: [1, 1, 2, 2]
}
```

## Tileset Reference

Opposed to serving the full GeoJSON features to your users, you can leverage the vector tilesets to load in details at specific map areas and zoom levels to optimise map loading.

Features are organised into several layers within the vector tilesets offered. You can selectively target features within a specific layer

The Alpaca Itinerary v1 contains the following layers in the tileset.

| Layer                                                                                                                 | Minimum zoom level | Feature Classes                                                                                                    |
| --------------------------------------------------------------------------------------------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------ |
| **location**<br>Contains plotted locations encompassing places within the itineraries                                 | 0                  | `location_marker`, `location_directions_preference`                                                                |
| **directions**<br>Contains itinerary directions geometry to help represent the suggested directions between locations | 0                  | `directions_distance_progress`, `directions_path`, `directions_path_waypoint`, `directions_path_distance_progress` |

## Features

The **Alpaca Itinerary v1** features include a number of representations of the
`ItineraryLocation`, `ItineraryDirections` and `RouteSegment` types.

| Type                                  | Description                                                               |
| ------------------------------------- | ------------------------------------------------------------------------- |
| **location_marker**                   | The primary marker for this location                                      |
| **location_directions_preference**    | The position preference to obtain directions to                           |
| **directions_distance_progress**      | Point representing a percentiles of progress along the overall directions |
| **directions_path**                   | Itinerary Directions path for itinerary directions                        |
| **directions_path_waypoint**          | The waypoints used for directing along the Itinerary Directions Path      |
| **directions_path_distance_progress** | Point representing a percentiles of progress along the route segment      |

### Feature `location_marker`

**Tile Layer**: `location`
**Geometry**: `Point`

The primary marker for this location

| Property                             | Description                                                                                                                               |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `class` string                       | `location_marker`                                                                                                                         |
| `lft` number                         | Hierarchy `lft`<br>Left outermost value                                                                                                   |
| `rgt` number                         | Hierarchy `rgt`<br>Right outermost value                                                                                                  |
| `depth` number                       | Hierarchy `depth`<br>The depth of the element, relative to ancestors                                                                      |
| `id` string                          | Node Reference `id`<br>The Alpaca related node identifier                                                                                 |
| `external_ref` string _optional_     | External Identifiers `external_ref`<br>Reference identifier in external platform, if any                                                  |
| `external_source` string _optional_  | External Identifiers `external_source`<br>Reference source in external platform, if any                                                   |
| `segments` text[]                    | Itinerary Segments `segments`<br>A collection of assigned segment identifiers for this feature, if any                                    |
| `icon` text _optional_               | Icon `icon`<br>The id of the itinerary icon                                                                                               |
| `label` text _optional_              | Content `label`<br>The primary label associated with this feature                                                                         |
| `tags` text[] _optional_             | Content `tags`<br>Any assigned user tags                                                                                                  |
| `bearing` number _optional_          | Viewport Adjustments `bearing`<br>Bearing, from 0-360                                                                                     |
| `pitch` number _optional_            | Viewport Adjustments `pitch`<br>Pitch, from 0-60                                                                                          |
| `zoom` number _optional_             | Viewport Adjustments `zoom`<br>Zoom, from 0-20+                                                                                           |
| `flags` text _optional_              | Feature Flags Behaviour `flags`<br>A collection of keys relating to which behaviours should be omitted when interacting with this feature |
| `optional` boolean _optional_        | Optional Stop information `optional`<br>Whether this feature has been indicated as an optional stop on the itinerary                      |
| `list_pref` string _optional_        | Location Numbering `list_pref`<br>Any associated list presentation preference applied to this location                                    |
| `location_num` number _optional_     | Location Numbering `location_num`<br>The location number, relative to the sibling locations                                               |
| `location_num_dfs` number _optional_ | Location Numbering `location_num_dfs`<br>The accumulative location number for the overall itinerary                                       |

#### Example

```json
{
  "type": "Feature",
  "id": 123,
  "properties": {
    "class": "location_marker",
    "lft": 5,
    "rgt": 6,
    "depth": 0,
    "id": "itinerary/XXX/location/XXX",
    "external_ref": "myplatform-UUID",
    "external_source": "myplatform-section-UUID",
    "segments": ["UUID"],
    "icon": "itinerary/XXX/icon/YYY",
    "label": "Mavis the Grocer",
    "tags": ["a tag", "another tag"],
    "bearing": 270,
    "pitch": 60,
    "zoom": 17,
    "flags": ["omit-list"],
    "optional": true,
    "list_pref": "unordered",
    "location_num": 2,
    "location_num_dfs": 9
  },
  "geometry": {
    "type": "Point",
    "coordinates": [0, 0]
  }
}
```

### Feature `location_directions_preference`

**Tile Layer**: `location`
**Geometry**: `Point`

The position preference to obtain directions to

| Property                             | Description                                                                                                                               |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `class` string                       | `location_directions_preference`                                                                                                          |
| `lft` number                         | Hierarchy `lft`<br>Left outermost value                                                                                                   |
| `rgt` number                         | Hierarchy `rgt`<br>Right outermost value                                                                                                  |
| `depth` number                       | Hierarchy `depth`<br>The depth of the element, relative to ancestors                                                                      |
| `id` string                          | Node Reference `id`<br>The Alpaca related node identifier                                                                                 |
| `external_ref` string _optional_     | External Identifiers `external_ref`<br>Reference identifier in external platform, if any                                                  |
| `external_source` string _optional_  | External Identifiers `external_source`<br>Reference source in external platform, if any                                                   |
| `segments` text[]                    | Itinerary Segments `segments`<br>A collection of assigned segment identifiers for this feature, if any                                    |
| `optional` boolean _optional_        | Optional Stop information `optional`<br>Whether this feature has been indicated as an optional stop on the itinerary                      |
| `flags` text _optional_              | Feature Flags Behaviour `flags`<br>A collection of keys relating to which behaviours should be omitted when interacting with this feature |
| `list_pref` string _optional_        | Location Numbering `list_pref`<br>Any associated list presentation preference applied to this location                                    |
| `location_num` number _optional_     | Location Numbering `location_num`<br>The location number, relative to the sibling locations                                               |
| `location_num_dfs` number _optional_ | Location Numbering `location_num_dfs`<br>The accumulative location number for the overall itinerary                                       |

#### Example

```json
{
  "type": "Feature",
  "id": 123,
  "properties": {
    "class": "location_directions_preference",
    "lft": 5,
    "rgt": 6,
    "depth": 0,
    "id": "itinerary/XXX/location/XXX",
    "external_ref": "myplatform-UUID",
    "external_source": "myplatform-section-UUID",
    "segments": ["UUID"],
    "optional": true,
    "flags": ["omit-list"],
    "list_pref": "unordered",
    "location_num": 2,
    "location_num_dfs": 9
  },
  "geometry": {
    "type": "Point",
    "coordinates": [0, 0]
  }
}
```

### Feature `directions_distance_progress`

**Tile Layer**: `directions`
**Geometry**: `Point`

Point representing a percentiles of progress along the overall directions

| Property                         | Description                                                                                                                      |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `class` string                   | `directions_distance_progress`                                                                                                   |
| `lft` number                     | Hierarchy `lft`<br>Left outermost value                                                                                          |
| `rgt` number                     | Hierarchy `rgt`<br>Right outermost value                                                                                         |
| `depth` number                   | Hierarchy `depth`<br>The depth of the element, relative to ancestors                                                             |
| `id` string                      | Node Reference `id`<br>The Alpaca related node identifier                                                                        |
| `percentage` number              | Progress `percentage`<br>Percentage progress along this feature (Values: 0, 25, 50, 75, 100)                                     |
| `multi_modal` boolean _optional_ | Multi-modal Travel Properties `multi_modal`<br>Whether multiple modes of transport are used to describe the itinerary directions |
| `origin` string _optional_       | Origin / Destination Node Reference `origin`<br>The origin Itinerary Location Node Reference                                     |
| `dest` string _optional_         | Origin / Destination Node Reference `dest`<br>The destination Itinerary Location Node Reference                                  |
| `mode` enum                      | Travel Mode `mode`<br>A series of values to describe the mode of transport (e.g. foot, car) for this feature                     |
| `route_segment` string           | ItineraryDirections / RouteSegment Relationship `route_segment`<br>The node reference ID of the associated Route Segment feature |

#### Example

```json
{
  "type": "Feature",
  "id": 123,
  "properties": {
    "class": "directions_distance_progress",
    "lft": 5,
    "rgt": 6,
    "depth": 0,
    "id": "itinerary/XXX/location/XXX",
    "percentage": 50,
    "multi_modal": true,
    "origin": "itinerary/XXX/location/XXX",
    "dest": "itinerary/XXX/location/XXX",
    "mode": "car",
    "route_segment": "itinerary/XXX/directions/XXX/segment/unstable.0"
  },
  "geometry": {
    "type": "Point",
    "coordinates": [0, 0]
  }
}
```

### Feature `directions_path`

**Tile Layer**: `directions`
**Geometry**: `LineString, MultiLineString`

Itinerary Directions path for itinerary directions

| Property                         | Description                                                                                                                      |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `class` string                   | `directions_path`                                                                                                                |
| `lft` number                     | Hierarchy `lft`<br>Left outermost value                                                                                          |
| `rgt` number                     | Hierarchy `rgt`<br>Right outermost value                                                                                         |
| `depth` number                   | Hierarchy `depth`<br>The depth of the element, relative to ancestors                                                             |
| `id` string                      | Node Reference `id`<br>The Alpaca related node identifier                                                                        |
| `distance` number                | Distance `distance`<br>Distance in meters                                                                                        |
| `duration_min` number _optional_ | Duration `duration_min`<br>Minimum duration (in minutes)                                                                         |
| `duration_max` number _optional_ | Duration `duration_max`<br>Maximum duration (in minutes)                                                                         |
| `multi_modal` boolean _optional_ | Multi-modal Travel Properties `multi_modal`<br>Whether multiple modes of transport are used to describe the itinerary directions |
| `mode` enum                      | Travel Mode `mode`<br>A series of values to describe the mode of transport (e.g. foot, car) for this feature                     |
| `origin` string _optional_       | Origin / Destination Node Reference `origin`<br>The origin Itinerary Location Node Reference                                     |
| `dest` string _optional_         | Origin / Destination Node Reference `dest`<br>The destination Itinerary Location Node Reference                                  |
| `route_segment` string           | ItineraryDirections / RouteSegment Relationship `route_segment`<br>The node reference ID of the associated Route Segment feature |
| `index` number                   | Collection Position `index`<br>The index of this element within the collection (0 indexed)                                       |
| `length` number                  | Collection Position `length`<br>The total length of the collection this feature is part of                                       |

#### Example

```json
{
  "type": "Feature",
  "id": 123,
  "properties": {
    "class": "directions_path",
    "lft": 5,
    "rgt": 6,
    "depth": 0,
    "id": "itinerary/XXX/location/XXX",
    "distance": 400,
    "duration_min": 40,
    "duration_max": 40,
    "multi_modal": true,
    "mode": "car",
    "origin": "itinerary/XXX/location/XXX",
    "dest": "itinerary/XXX/location/XXX",
    "route_segment": "itinerary/XXX/directions/XXX/segment/unstable.0",
    "index": 3,
    "length": 4
  },
  "geometry": {
    "type": "LineString",
    "coordinates": [
      [0, 0],
      [5, 5],
      [10, 10]
    ]
  },
  "bbox": [0, 0, 10, 10]
}
```

### Feature `directions_path_waypoint`

**Tile Layer**: `directions`
**Geometry**: `Point`

The waypoints used for directing along the Itinerary Directions Path

| Property                         | Description                                                                                                                      |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `class` string                   | `directions_path_waypoint`                                                                                                       |
| `lft` number                     | Hierarchy `lft`<br>Left outermost value                                                                                          |
| `rgt` number                     | Hierarchy `rgt`<br>Right outermost value                                                                                         |
| `depth` number                   | Hierarchy `depth`<br>The depth of the element, relative to ancestors                                                             |
| `id` string                      | Node Reference `id`<br>The Alpaca related node identifier                                                                        |
| `origin` string _optional_       | Origin / Destination Node Reference `origin`<br>The origin Itinerary Location Node Reference                                     |
| `dest` string _optional_         | Origin / Destination Node Reference `dest`<br>The destination Itinerary Location Node Reference                                  |
| `index` number                   | Collection Position `index`<br>The index of this element within the collection (0 indexed)                                       |
| `length` number                  | Collection Position `length`<br>The total length of the collection this feature is part of                                       |
| `multi_modal` boolean _optional_ | Multi-modal Travel Properties `multi_modal`<br>Whether multiple modes of transport are used to describe the itinerary directions |
| `mode` enum                      | Travel Mode `mode`<br>A series of values to describe the mode of transport (e.g. foot, car) for this feature                     |
| `route_segment` string           | ItineraryDirections / RouteSegment Relationship `route_segment`<br>The node reference ID of the associated Route Segment feature |

#### Example

```json
{
  "type": "Feature",
  "id": 123,
  "properties": {
    "class": "directions_path_waypoint",
    "lft": 5,
    "rgt": 6,
    "depth": 0,
    "id": "itinerary/XXX/location/XXX",
    "origin": "itinerary/XXX/location/XXX",
    "dest": "itinerary/XXX/location/XXX",
    "index": 3,
    "length": 4,
    "multi_modal": true,
    "mode": "car",
    "route_segment": "itinerary/XXX/directions/XXX/segment/unstable.0"
  },
  "geometry": {
    "type": "Point",
    "coordinates": [0, 0]
  }
}
```

### Feature `directions_path_distance_progress`

**Tile Layer**: `directions`
**Geometry**: `Point`

Point representing a percentiles of progress along the route segment

| Property                         | Description                                                                                                                      |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `class` string                   | `directions_path_distance_progress`                                                                                              |
| `lft` number                     | Hierarchy `lft`<br>Left outermost value                                                                                          |
| `rgt` number                     | Hierarchy `rgt`<br>Right outermost value                                                                                         |
| `depth` number                   | Hierarchy `depth`<br>The depth of the element, relative to ancestors                                                             |
| `id` string                      | Node Reference `id`<br>The Alpaca related node identifier                                                                        |
| `percentage` number              | Progress `percentage`<br>Percentage progress along this feature (Values: 0, 25, 50, 75, 100)                                     |
| `origin` string _optional_       | Origin / Destination Node Reference `origin`<br>The origin Itinerary Location Node Reference                                     |
| `dest` string _optional_         | Origin / Destination Node Reference `dest`<br>The destination Itinerary Location Node Reference                                  |
| `multi_modal` boolean _optional_ | Multi-modal Travel Properties `multi_modal`<br>Whether multiple modes of transport are used to describe the itinerary directions |
| `index` number                   | Collection Position `index`<br>The index of this element within the collection (0 indexed)                                       |
| `length` number                  | Collection Position `length`<br>The total length of the collection this feature is part of                                       |
| `mode` enum                      | Travel Mode `mode`<br>A series of values to describe the mode of transport (e.g. foot, car) for this feature                     |
| `route_segment` string           | ItineraryDirections / RouteSegment Relationship `route_segment`<br>The node reference ID of the associated Route Segment feature |

#### Example

```json
{
  "type": "Feature",
  "id": 123,
  "properties": {
    "class": "directions_path_distance_progress",
    "lft": 5,
    "rgt": 6,
    "depth": 0,
    "id": "itinerary/XXX/location/XXX",
    "percentage": 50,
    "origin": "itinerary/XXX/location/XXX",
    "dest": "itinerary/XXX/location/XXX",
    "multi_modal": true,
    "index": 3,
    "length": 4,
    "mode": "car",
    "route_segment": "itinerary/XXX/directions/XXX/segment/unstable.0"
  },
  "geometry": {
    "type": "Point",
    "coordinates": [0, 0]
  }
}
```
