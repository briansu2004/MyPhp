# PHP - CSV

## Save the results fetched from a REST API into a CSV file in PHP

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
    // Open a file for writing (or create if it doesn't exist)
    $csvFile = fopen('api_data.csv', 'w');

    // Write CSV header
    fputcsv($csvFile, array_keys($data[0]));

    // Write each data row to CSV
    foreach ($data as $row) {
        fputcsv($csvFile, $row);
    }

    // Close the file
    fclose($csvFile);

    echo "Data has been saved to api_data.csv file.";
} else {
    // Handle decoding error
    echo "Error decoding JSON response.";
}
?>
```

This script will fetch data from the API, parse it as JSON, and then write it to a CSV file named `api_data.csv`. Make sure the web server has write permissions to the directory where you're saving the CSV file. You can adjust the file name and path as needed.

## Read CSV and Parse

We can use the built-in functions `fopen()`, `fgetcsv()`, and `fclose()` to accomplish this.

```php
<?php
// Open the CSV file for reading
$csvFile = fopen('example.csv', 'r');

// Check if the file was opened successfully
if ($csvFile !== false) {
    // Initialize an array to store parsed data
    $data = array();

    // Read each line from the CSV file
    while (($row = fgetcsv($csvFile)) !== false) {
        // Add the row to the data array
        $data[] = $row;
    }

    // Close the CSV file
    fclose($csvFile);

    // Display or process the parsed data
    foreach ($data as $row) {
        // Access each column of the row
        foreach ($row as $value) {
            echo $value . ' ';
        }
        echo "<br>";
    }
} else {
    // Handle file opening error
    echo "Error opening CSV file.";
}
?>
```

This script opens a CSV file named `example.csv`, reads its contents line by line using `fgetcsv()`, and stores each row as an array in the `$data` array. Finally, it loops through the `$data` array to display or process each row and its columns.
