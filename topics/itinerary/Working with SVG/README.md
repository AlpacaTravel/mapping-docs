[//]: # "Title: Scalable Vector Graphics"
[//]: # "Weight: 7"

# Working with SVG

<img src="./svg-basic-styled.png" alt="Basic SVG Example" />

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
https://mapping.withalpaca.travel/v1/itinerary/XXX.svg?accessToken=YOUR_ACCESS_TOKEN
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

| Query Parameter      | Description                                                            |
| -------------------- | ---------------------------------------------------------------------- |
| bbox                 | Alternative bounding box, in 4 numeric values; "west,south,east,north" |
| pointAsCircle        | Render points as an circle opposed to a path; "true" or "false"        |
| markerLabelAsText    | Render text elements for markers with label values; "true" or "false"  |
| radius               | Radius for the point; "1", "2"...                                      |
| width, height        | Viewport Canvas controls                                               |
| lineStringProcessing | Line simplification and Bezier Spline operations to generalise detail  |

### LineString Processing

To recreate a "generalised" route outline for geometry and smooth out line
detail, the SVG can be customised using two operations:

- Simplify
- Bezier Spline

These operations can be used at the same time to both simplify the line then
smooth out the detail using bezier splines.

Simplify is achieved using Douglas-Peucker algorithm, and can have a customised
tolerance (default is `0.85`). You can splify a simplify operation via
`lineStringProcessing=simplify`, or by passing the tolerance via
`lineStringProcessing=simplify_0.01`.

Bezier Spline is achieved by `lineStringProcessing=bezierSpline` and can also be
customised via the resolution (default `10000`) controlling the time in
milliseconds between points and sharpness (default `0.85`) controlling how curvy
the path should be between splines. You can control the resolution and sharpness
through appending them to the string;
`lineStringProcessing=bezierSpline_8000_0.6`.

You can additionally support multiple stages of processing by seperating each
processing operation by a `,`, such as
`lineStringProcessing=simplify,bezierSpline`.

### Administrative Boundaries

Alpaca also provide simple boundary resources.

```
https://mapping.withalpaca.travel/v1/place/XXX.svg?accessToken=YOUR_ACCESS_TOKEN
```

Substitute the place/XXX with values as obtained from the following table:

| Resource                             | Description                                                                                                                                                                                                                                   |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| place/naturalearth:iso-3166-1:xx     | 50m Admin 0 feature, substitute the XX with the ISO-3166 2 letter country code (such as au)                                                                                                                                                   |
| place/naturalearth:iso-3166-2:xx-yyy | 50m Admin 1 feature, substitute the XX-YYY with the ISO-3166-2 code (such as au-vic)                                                                                                                                                          |
| place/abs:2021-tourism:xxxxx         | Australian tourism regions, where xxxxx is the TR_CODE21 (See ABS)[https://www.abs.gov.au/statistics/standards/australian-statistical-geography-standard-asgs-edition-3/jul2021-jun2026/access-and-downloads/digital-boundary-files]          |
| place/abs:2021-lga:xxxxx             | Australian postal regions, where xxxxx is the LGA_CODE21 (See ABS)[https://www.abs.gov.au/statistics/standards/australian-statistical-geography-standard-asgs-edition-3/jul2021-jun2026/access-and-downloads/digital-boundary-files]          |
| place/abs:2021-suburb:xxxxx          | Australian suburbs, where xxxxx is the SAL_CODE21 (See ABS)[https://www.abs.gov.au/statistics/standards/australian-statistical-geography-standard-asgs-edition-3/jul2021-jun2026/access-and-downloads/digital-boundary-files]                 |
| place/abs:2021-electoral:xxxxx       | Australian state electoral regions, where xxxxx is the SED_CODE21 (See ABS)[https://www.abs.gov.au/statistics/standards/australian-statistical-geography-standard-asgs-edition-3/jul2021-jun2026/access-and-downloads/digital-boundary-files] |
| place/abs:2021-postal:xxxxx          | Australian state electoral regions, where xxxxx is the POA_CODE21 (See ABS)[https://www.abs.gov.au/statistics/standards/australian-statistical-geography-standard-asgs-edition-3/jul2021-jun2026/access-and-downloads/digital-boundary-files] |

You can also use an interactive map to identify the ID to include:

- [Natural Earth Cultural (countries, regions and timezones)](https://mapping.withalpaca.com/set/naturalearth_cultral)
- [ABS 2021 Tourism Regions](https://mapping.withalpaca.travel/set/abs_2021_tourism)
- [ABS Postal Boundaries](https://mapping.withalpaca.travel/set/abs_2021_postal)
- [ABS LGAs Boundaries](https://mapping.withalpaca.travel/set/abs_2021_lga)
- [ABS Electoral Boundaries](https://mapping.withalpaca.travel/set/abs_2021_electoral)
- [ABS Suburb Boundaries](https://mapping.withalpaca.travel/set/abs_2021_suburb)

### Merging SVG

You can combine SVG data together into a single request leveraging the `merge`
query parameter. Provide multiple resources in the query param in order to draw
those SVG's into the same document body.

This can assist designers position the itinerary against other geographic
features.

```
https://mapping.withalpaca.travel/v1/itinerary/XXX.svg?accessToken=YOUR_ACCESS_TOKEN&merge=place/naturalearth:iso-3166-1:au&bbox=109,-45,110,-9
```
