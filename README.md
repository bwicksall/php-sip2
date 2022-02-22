# SIP2 TLS/SSL communication library for PHP

PHP class library to facilitate communication with Integrated Library System (ILS) servers via 3M's SIP2.

This fork adds TLS and SSL support so we can connect directly to secure Stunnel endpoints if available.


## Composer Installation

Ignore this for now.

To install this package, run this command:
```sh
composer require cap60552/php-sip2
```

## General Installation
Copy the sip2.class.php file to a location in your php_include path.

## General Usage

	// create object
	$mysip = new sip2;

	// Set host name
	$mysip->hostname = 'server.example.com';
	$mysip->port = 6002;

	// Identify a patron
	$mysip->patron = '101010101';
	$mysip->patronpwd = '010101';
 
	// connect to SIP server 
	$result = $mysip->connect();

	// Get Charged Items Raw response
	$in = $mysip->msgPatronInformation('charged');

	// parse the raw response into an array
	$result = $mysip->parsePatronInfoResponse( $mysip->get_message($in) );

## Usage with SSL or TLS

First create your client certificate:

    openssl genrsa 4096 > sip.key
    openssl req -new -key sip.key -x509 -days 1000 -out sip.crt
    cat sip.crt sip.key > sip.pem

Now take the above example and add these SSL/TLS related variables:

    // Port to your Stunnel server
    $mysip->port      = 6443;

    // Path to your sip.pem file
    $mysip->cert      = __DIR__. '/sip.pem';

    // tls, ssl or tcp.  tcp is the default
    $mysip->conn_type = 'tls';

## Contribution

Feel free to contribute!
