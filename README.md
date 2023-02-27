# LalamovePHP-SDK

The LalamovePHP-SDK is a PHP library that provides an easy-to-use interface for developers to connect to Lalamove's on-demand delivery service. With this SDK, developers can authenticate, create quotations, create orders, and retrieve order details.

# Authentication

To use the LalamovePHP-SDK, you must first authenticate with Lalamove's API. You can obtain your API credentials from the Lalamove developer portal. Once you have your credentials, you can create an instance of the SDK and set your API key, API secret, market, and environment:

```
require_once 'vendor/autoload.php';

use stdmedoth\LalamovePhpSdk;

$api_key = 'YOUR_API_KEY';
$api_secret = 'YOUR_API_SECRET';
$market = 'YOUR_MARKET'; // e.g. 'SG'
$environment = 'YOUR_ENVIRONMENT'; // either 'product' or 'sandbox'

$lalamove = new LalamovePhpSdk($api_key, $api_secret, $market, $environment);
```

# Creating a Quotation

To create a quotation, you need to provide the following information:

- serviceType: Type of service. This parameter is required and can be obtained from the services endpoint.
- stops: An array of stops objects containing pickup and dropoff information, including the location coordinates (latitude and longitude) and the address of each stop.
- language: Language used to return the quotation. This parameter is optional and can be set to en_US by default.
- item: An object containing information about the item being delivered, including quantity, weight, categories, and handling instructions. This parameter is optional.

> Here's an example code snippet to create a quotation:

```
$serviceType = $possible_service->key;
$stops = [(object)[
    'coordinates' => (object)[
        'lat' => "-23.6008754",
        'lng' => "-46.6521289"
    ],
    'address' => 'Alameda Anapurus'
], (object)[
    'coordinates' => (object)[
        'lat' => "$location->lat",
        'lng' => "$location->lng",
    ],
    'address' => $package['destination']['address']
]];
$item = (object)[
    "quantity" => "$quantity",
    "weight" => "LESS_THAN_3KG",
    "categories" => ["FOOD_DELIVERY", "OFFICE_ITEM"],
    "handlingInstructions" => ["KEEP_UPRIGHT"]
];
$response = $lalamove_api->quotations($serviceType, $stops, $language, $item);
$quotation = $response->data;

```
