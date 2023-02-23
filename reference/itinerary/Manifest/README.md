---
name: Alpaca Itinerary v1 Manifest Reference
---

## Overview

The _Itinerary Manifest_ file provides key information to support application
developers with access to some key information to enhance their mapping
applications.

- Viewports and bounds for various ID's appearing in your data
- Reference to sprites or data sources available
- Sprites and Style URLs

### Manifest URL

The manifest URL is available to load with your itinerary ID and your access
token.

```
https://mapping.withalpaca.travel/v1/itinerary/abc.json?scheme=tms&accessToken=YOUR_ACCESS_TOKEN
```

Update `itinerary/abc` with your itinerary ID and YOUR_ACCESS_TOKEN with your
alpaca travel access token.

### Type Definition

```typescript
type Manifest = {
  // The Itinerary ID
  id: string;

  // The Profile ID
  profile?: string;

  // The bounds for the itinerary, used to position the viewport
  bounds?: [[number, number], [number, number]];

  // Viewports for each of the features
  viewports?: Record<
    string,
    {
      id: string;
      __typename: string;
      lft?: number;
      rgt?: number;
      depth?: number;
      bounds: [[number, number], [number, number]] | null;

      // Various cameras
      // TODO: Outline the use of cameras in this type description
      cameras: any[];
    }
  >;

  // Sources of data
  // TODO: Outline the various sources of data
  sources: any[];

  // Generated Spriesheets
  sprite: Record<string, { layout: string; image: string }>;

  // Styles
  style: {
    // Alpaca Default style (for Mapbox)
    default: string;
  };
};
```

### Example JSON

```json
{
  "id": "itinerary/XXX",
  "profile": "profile/XXX",
  "bounds": [
    [141.91962243618133, -36.12207096190349],
    [147.31849501216556, -33.38301328114559]
  ],
  "viewports": {
    "itinerary/XXX": {
      "id": "itinerary/XXX",
      "__typename": "Itinerary",
      "bounds": [
        [141.91962243618133, -36.12207096190349],
        [147.31849501216556, -33.38301328114559]
      ],
      "cameras": [
        {
          "type": "geometry-bounds",
          "bounds": [
            [141.91962243618133, -36.12207096190349],
            [147.31849501216556, -33.38301328114559]
          ]
        }
      ]
    },
    "itinerary/XXX/location/51Vc9Sx2dlY6Usw3Mj5igt": {
      "id": "itinerary/XXX/location/51Vc9Sx2dlY6Usw3Mj5igt",
      "__typename": "ItineraryLocation",
      "pos": [146.9099993389067, -36.099760943424805],
      "lft": 2,
      "rgt": 3,
      "depth": 0,
      "bounds": null,
      "cameras": []
    }
  },
  "sources": [
    {
      "type": "geojson",
      "url": "https://mapping.withalpaca.travel/v1/itinerary/XXX.geojson?accessToken=YOUR_ACCESS_TOKEN"
    },
    {
      "type": "vector",
      "url": "https://mapping.withalpaca.travel/v1/itinerary/XXX.tilejson?scheme=xyz&accessToken=YOUR_ACCESS_TOKEN",
      "scheme": "xyz"
    }
  ],
  "sprite": {
    "default": {
      "layout": "https://spritesheet.withalpaca.travel/sprites/profile_490ladFZftvd8o0CxTjdtf/itinerary_XXX/itinerary-v1.json?accessToken=YOUR_ACCESS_TOKEN",
      "image": "https://spritesheet.withalpaca.travel/sprites/profile_490ladFZftvd8o0CxTjdtf/itinerary_XXX/itinerary-v1.png?accessToken=YOUR_ACCESS_TOKEN",
      "layout2x": "https://spritesheet.withalpaca.travel/sprites/profile_490ladFZftvd8o0CxTjdtf/itinerary_XXX/itinerary-v1@2x.json?accessToken=YOUR_ACCESS_TOKEN",
      "image2x": "https://spritesheet.withalpaca.travel/sprites/profile_490ladFZftvd8o0CxTjdtf/itinerary_XXX/itinerary-v1@2x.png?accessToken=YOUR_ACCESS_TOKEN"
    }
  },
  "styles": {
    "default": "https://mapping.withalpaca.travel/v1/style/itinerary/XXX.json?accessToken=YOUR_ACCESS_TOKEN"
  }
}
```
