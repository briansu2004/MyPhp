# PHP - consuming a REST API and handling JSON responses

Here's a basic example of how you can do it using PHP's built-in functions:

1. **Sending a GET Request and Parsing JSON Response:**

```php
<?php
// URL of the REST API
$url = 'https://api.example.com/data';

// Send GET request
$response = file_get_contents($url);

// Decode JSON response
$data = json_decode($response, true);

// Check if decoding was successful
if ($data !== null) {
    // Handle the data
    foreach ($data as $item) {
        // Process each item from the API
        echo $item['key'] . ': ' . $item['value'] . "<br>";
    }
} else {
    // Handle decoding error
    echo "Error decoding JSON response.";
}
?>
```

2. **Sending POST Request with JSON Payload:**

```php
<?php
// Data to be sent in JSON format
$data = array(
    'key1' => 'value1',
    'key2' => 'value2'
);

// Encode data as JSON
$json_data = json_encode($data);

// URL of the REST API
$url = 'https://api.example.com/create';

// Set up cURL to send POST request
$curl = curl_init($url);
curl_setopt($curl, CURLOPT_POST, true);
curl_setopt($curl, CURLOPT_POSTFIELDS, $json_data);
curl_setopt($curl, CURLOPT_HTTPHEADER, array('Content-Type: application/json'));
curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);

// Send the request
$response = curl_exec($curl);

// Check for errors
if ($response === false) {
    echo "Error: " . curl_error($curl);
} else {
    // Handle response
    echo "Response: " . $response;
}

// Close cURL session
curl_close($curl);
?>
```

TODO handle errors appropriately, such as when the API is unreachable or when the JSON response cannot be decoded.
