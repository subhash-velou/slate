---
title: Velou API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - javascript:  Node.js
  - php: PHP
  - python: Python

toc_footers:

includes:
  - errors

search: true
---

# Introduction

Welcome to Velou API!

You can view code examples in the programming language of your choice by clicking the corresponding tab in the dark-blue area in the rightmost pane. Each tab corresponds to a Software Development Kit (SDK) that Smartsheet provides to make working in that programming language easier. See [SDKs and Sample Code](#sdks-and-code-samples).

## Getting Started

## Authentication

## SDKs and Code Samples

Velou has Software Development Kits (SDKs) providing a higher level interface for several languages.

Language | SDK | Sample Application
-------- | --- | ------------------
JavaScript | [velou-nodejs-sdk](https://github.com/velou/velou-nodejs-sdk) | [velou-nodejs-sample-app](https://github.com/velou/velou-nodejs-sample-app)
PHP | [velou-php-sdk](https://github.com/velou/velou-php-sdk) | [velou-php-sample-app](https://github.com/velou/velou-php-sample-app)
Python | [velou-python-sdk](https://github.com/velou/velou-python-sdk) | [velou-python-sample-app](https://github.com/velou/velou-python-sample-app)

In addition to the sample application provided for each SDK, you can always view code examples in this document by clicking the corresponding tab in the dark-blue area in the rightmost pane.

To use an SDK for development work, follow the instructions in the SDK readme to download and install the SDK. Then download the sample app and run it. Once you've run the sample application, you can clone it and use the structure it provides to start building your own applications.

# Indexing

## Add Products

> Sample Request

```shell
curl https://api.velou.com/1.0/products \
-H "Authorization: Bearer AbCdEf123456" \
-H "Content-Type: application/json" \
-X POST \
-d '
{
  "products": [
    {
      "id": "3924132",
      "name": "Devery Crepe Shift Dress",
      "url": "https://shop.nordstrom.com/s/felicity-coco-devery-crepe-shift-dress-nordstrom-exclusive/3924132",
      "description": "Ever comfortable and chic, the classic shift gains a fresh feeling from crisp, colorful crepe.",
      "features": [
        "34 1/2\" length (size Medium).",
        "Exposed back-zip closure.",
        "97% polyester, 3% spandex.",
        "Hand wash cold, dry flat."
      ],
      "categories": [
        "Women",
        "Clothing",
        "Dresses"
      ],
      "relatedTags": [],
      "gender": "Women",
      "ageGroup": "Adult",
      "colors": [
        {
          "id": "39483",
          "name": "Cobalt",
          "swatchUrl": "https://n.nordstrommedia.com/ImageGallery/store/product/SwatchMedium/15/_101896855.jpg?crop=fit&w=31&h=31"
        },
        {
          "id": "9384",
          "name": "Emerald Green",
          "swatchUrl": "https://n.nordstrommedia.com/ImageGallery/store/product/SwatchMedium/2/_102885802.jpg?crop=fit&w=31&h=31"
        }
      ],
      "media": [
        {
          "url": "https://n.nordstrommedia.com/ImageGallery/store/product/Zoom/12/_102539612.jpg?crop=pad&pad_color=FFF&format=jpeg&w=780&h=1197",
          "altText": "front"
        },
        {
          "url": "https://n.nordstrommedia.com/ImageGallery/store/product/Zoom/5/_102539265.jpg?crop=pad&pad_color=FFF&format=jpeg&w=780&h=1197",
          "altText": "back"
        },
        {
          "url": "https://n.nordstrommedia.com/ImageGallery/store/product/Zoom/19/_102539179.jpg?crop=pad&pad_color=FFF&format=jpeg&w=780&h=1197",
          "altText": "side",
          "colorId": "39483"
        }
      ],
      "skus": [
        {
          "price": 80,
          "colorId": "39483",
          "size": "Small"
        },
        {
          "price": 82,
          "colorId": "39483",
          "size": "Large"
        },
        {
          "price": 80,
          "colorId": "9384",
          "size": "Small"
        }
      ],
      "popularity": {
        "type": 1,
        "data": {
          "overallRating": 4.3,
          "maxRating": 5,
          "reviewCount": 260
        }
      },
      "currencyCode": "USD",
      "isDeleted": false
    }
  ]
}'
```
```javascript
import velouSdk from 'velou-sdk';

const client = new velouSdk.createClient('YourAPIKey');

client.add({});
```

> Sample Response

```json
```

`POST https://api.velou.com/1.0/products`

Add product details

Parameter | Type | Description
--------- | ---- | -----------
**id** | String | The unique Id of a product on your store.
**url** | String | Canonical URL relating to the product in the your store.
name | String | Short name/description of the product.
description | String | Long description of the product.
features | Array[String] | Features of the product: for example, style information, composition, washing instructions, the country where the product was made, any unique words that describe the item.
categories | Array[String] | Category information for the product - there can be multiple categories in a hierarchy of categories for a product. If there's a hierarchy for the categories, start at the root level and store it as the first element of the list, and then go down the hierarchy and store the rest. 
productRelatedTags | Array[String] | A list of tags associated with the product. Typically these are tags that have already been derived by you manually - i.e. the neck style, cut information, etc. NOTE: Only product level related tags should be stored here - any SKU level related tags should be stored in the skuRelatedTags field.
gender | Enum ["Men", "Women", "Unisex"] | Gender of the target customer.
ageGroup | Enum ["Adults", "Teens", "Kids"] | Age group of the target customer.
colors | Array[Color Object] | Detailed color information relating color IDs used in skus and media fields for the product. This field contains a list of color objects with following information:<ul><li>**id** (Integer) The unique Id of a color.</li><li>name (String) Name of the color/s - i.e. "Blue" or "Blue, Red".</li><li>swatchUrl (String) Link to the color swatch image.</li></ul>
media | Array[Media Object] | A list of media objects relating to the product. NOTE: Currently only images are supported. Videos are not supported. Each object contains the following items: <ul><li>**url** (String) URL to access the media object.</li><li>altText (String) alternate text to display if the image is missing.</li><li>colorId (Integer) Color ID relating to the media object - refers to color IDs in colorId field. If a colorId is specified here, a matching colorId definition MUST be available in the colors field.</li></ul>
skus | Array[SKU Objects] | A list of product SKU information including, color, size, price information for all possible combinations. Only SKUs that are available will be in the list - if a particular color and size combination is not available in the list, it will be considered as not available.<br /><br />If there are no SKUs provided, we consider that the product is currently unavailable/discontinued/out of stock.<br /><br />List of product SKUs contains the following information for each SKU:<ul><li>**price** (Float) The current price of the SKU using the specified currency code in the currencyCode field.</li><li>colorId (Integer) Color ID for the color of the SKU. This field relates to textual color information stored in colors field. If a colorId is specified here, a matching colorId definition MUST be available in the colors field.</li><li>size (String) Size information for the SKU. This information could be in many different formats such as "Small", "36", "40 R", etc.</li><li>initialPrice (Float) The initial price of the SKU using the specified currency code in the currencyCode field.</li><li>estimatedRetailPrice (Float) Estimated retail price of the item in new condition (especially applicable in re-sale sites).</li><li>skuCondition (Array[String]) Description of the condition of the item (especially in re-sale sites).</li><li>skuRelatedTags (Array[String]) A list of tags associated with the SKU. Typically these are tags that have already been derived by you manually - i.e. tags relating to pattern, size information for a SKU, etc. NOTE: Only SKU level related tags should be stored here - any product level related tags should be stored in the productRelatedTags field.</li></ul>
popularity | Popularity Object | The popularity of the product based on user feedback on the your store. There are 3 different popularity types supported currently: Star rating, Favorites/Likes and Thumbs up/down.<br /><br />The popularity object contains the following information:<ul><li>**type** (Enum ["STAR", "LIKES", "THUMBS"]) Type of the popularity.</li><li>**data** (Object) Depending on the type, the values contained in data will be different:<br  />type = STAR:<ul><li>**overallRating** (Float) Overall rating for the product.</li><li>**maxRating** (Float) Maximum possible rating for product. Typically this is the same across all items for a store.</li><li>**reviewCount** (Integer) Total review count for the product</li></ul>type = LIKES:<ul></li>**favLikeCount** (Integer) Favorites / Likes count for the product.</li></ul>type = THUMBS:<ul><li>**thumbsUpCount** (Integer) Thumbs up count for the product.</li><li>**thumbsDownCount** (Integer) Thumbs down count for the product.</li></ul>

**Required fields are in bold**

## Update Products

`PUT https://api.velou.com/1.0/products`

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

## Delete Products

`DELETE https://api.velou.com/1.0/products`

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />


# Querying

## Search Results

`GET https://api.velou.com/1.0/search`

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />

### Pagination

<br /><br /><br /><br /><br /><br /><br />

### Filtering

<br /><br /><br /><br /><br /><br /><br />

## Query Suggestions

`GET https://api.velou.com/1.0/suggestions`

<br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br /><br />