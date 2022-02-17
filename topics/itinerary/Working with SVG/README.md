# Working with SVG

> Scalable Vector Graphics can be used in mapping to provide vector
> representations of itineraries without requiring an interactive mapping SDK

Alpaca provides resources for developers and designers to design a SVG
representation of an itinerary.

The mapping service can output SVG representations of itinerary resources that
are unstyled documents. Developers can incorporate the asset onto their website
and then style the SVG elements as they prefer. SVG's can also be worked with
using d3.js and other tools to style and present data as they wish.

In addition to the SVG itinerary documents, Alpaca provide some physical and
cultural data to contextualise the itinerary SVG against features such as
administrative boundies level 0 or 1 (country / regions).

When building applications, Alpaca offers a GraphQL API in order to obtain more
information about itinerary features. For developers that are familiar with
working with d3.js or alternative libraries, you may want to access the GeoJSON
data directly to make alternative projections.

When making requests to either GraphQL or SVG resources hosted on Alpaca, you
must provide your `accessToken`.

## SVG Output

SVG's are generated from the following base URL:

```
https://mapping.withalpaca.com/itinerary/XXX.svg?accessToken=pk.123
```

Substitute your itinerary/XXX with your itinerary ID and the accessToken with
your access token.

### Common Attributes

To assist with stylising the SVG, the SVG output can have the presence of
certain `data-` attributes. The following table outlines some of the attributes
that may be included for certain features.

| Attribute         | Description                                                                                                      |
| ----------------- | ---------------------------------------------------------------------------------------------------------------- |
| class             | The feature class, which corresponds to the same classes from GeoJSON (`location_marker`, `directions_path` etc) |
| data-id           | Identifier for feature in Alpaca (can be used for GraphQL calls)                                                 |
| data-label        | Label associated with the feature                                                                                |
| data-location-num | The number associated with the location                                                                          |
| data-mode         | The mode of transport for the directions                                                                         |

### Customising SVG's

Along with your request, you can include the following query parameters to
change the SVG export.

| Query Parameter | Description                                                            |
| --------------- | ---------------------------------------------------------------------- |
| bbox            | Alternative bounding box, in 4 numeric values; "west,south,east,north" |
| pointAsCircle   | Render points as an circle opposed to a path                           |
| radius          | Radius for the point                                                   |
| width, height   | Viewport Canvas controls                                               |

### Administrative Boundaries

Alpaca also provide simple boundary resources.

```
https://mapping.withalpaca.com/place/XXX.svg?accessToken=pk.123
```

Substitute the place/XXX with values as obtained from the following table

| Resource                             | Description                                                                                 |
| ------------------------------------ | ------------------------------------------------------------------------------------------- |
| place/naturalearth:ISO-3166-1:XX     | 50m Admin 0 feature, substitute the XX with the ISO-3166 2 letter country code (such as AU) |
| place/naturalearth:ISO-3166-2:XX-YYY | 50m Admin 1 feature, substitute the XX-YYY with the ISO-3166-2 code (such as AU-VIC)        |
| place/naturalearth:admin:0           | All countries                                                                               |

### Merging SVG

You can combine SVG data together into a single request leveraging the `merge`
query parameter. Provide multiple resources in the query param in order to
draw those SVG's into the same document body.

This can assist designers position the itinerary against other geographic
features.

```
[https](https://mapping.withalpaca.com/itinerary/XXX.svg?accessToken=pk.123&merge=place/naturalearth:ISO-3166-1/AU&bbox=109,-45,110,-9)
```

**Basic Styled SVG Example**

<img src="./svg-basic-styled.png" alt="Basic SVG Example" />
