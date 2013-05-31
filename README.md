# Overview
This is a PHP SDK to help communication with the LinkedIn API.

## Init
	$linkedin = new LinkedIn(array(
		'apiKey' => '<API KEY>',
		'apiSecret' => '<API SECRET>',
		'callbackUrl' => '<CALLBACK>',
	));

## Obtaining an access token example

	if (isset($_GET['code'])) {
		if ($_SESSION['state'] == $_GET['state']) {
			$token = $linkedin->getAccessToken($this->_request->code);
		} else {
			throw new LinkedInException("Error occured");
		}
	} else { 
		if ((empty($_SESSION['expires_at'])) || (time() > $_SESSION['expires_at'])) {
			$_SESSION = array();
		}
		if (empty($_SESSION['access_token'])) {
			$linkedin->getAuthorizationCode("r_fullprofile r_emailaddress rw_nus r_network");
		}
	}

## GET


	$linkedin->get('/people/~', $options);
	
## POST

	$linkedin->post('/people-search/', $options);