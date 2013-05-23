OAuth2 Example
-------

	$linkedin = new LinkedIn(array(
		'apiKey' => '<API KEY>',
		'apiSecret' => '<API SECRET>',
		'callbackUrl' => '<CALLBACK>',
	));
	
	if (isset($_GET['code'])) {
		// User authorized your application
		if ($_SESSION['state'] == $_GET['state']) {
			// Get token so you can make API calls
			$token = $linkedin->getAccessToken($this->_request->code);
		} else {
			// CSRF attack? Or did you mix up your states?
			throw new LinkedInException("Error occured");
		}
	} else { 
		if ((empty($_SESSION['expires_at'])) || (time() > $_SESSION['expires_at'])) {
			// Token has expired, clear the state
			$_SESSION = array();
		}
		if (empty($_SESSION['access_token'])) {
			// Start authorization process
			$linkedin->getAuthorizationCode("r_fullprofile r_emailaddress rw_nus r_network");
		}
	}


GET
---

	$linkedin->get('/people/~');
	
POST
---
	$linkedin->post('/people-search/', $options);