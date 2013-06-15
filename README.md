# Overview
This is a PHP SDK to help communication with the LinkedIn API using OAuth 2 flow.

## Init
```php
$linkedin = new LinkedIn(array(
	'apiKey' => '<API KEY>',
	'apiSecret' => '<API SECRET>',
	'callbackUrl' => '<CALLBACK>',
));
```
## Obtaining an access token example
```php
if (isset($_GET['code'])) {
  // Check to see if our states match
	if ($_SESSION['state'] == $_GET['state']) {
	  // If alls good the pass the code to the get assess token function; returns (String) accesstoken
		$token = $linkedin->getAccessToken($this->_request->code);
	} else {
	  // If our states did not match, throw Exception
		throw new LinkedInException("Mismatch on states");
	}
} else { 
	// If we do not have an access token, send the user through the authenication process
	if (empty($_SESSION['access_token'])) {
	  // Define the scope for what permissions we need to access the data we want
	  $scope = "r_fullprofile r_emailaddress rw_nus r_network";
	  
	  // $linkedin->getLoginUrl() will build our url and pass it back to our script
	  $url = $linkedin->getLoginUrl($scope); 
		
      // Redirect the browser to LinkedIn for authenication
	  header("Location: " . $url)
	}
}
```
## GET
```php
$linkedin->get('/people/~', $options);
```

## POST
```php
$linkedin->post('/people-search/', $options);
```