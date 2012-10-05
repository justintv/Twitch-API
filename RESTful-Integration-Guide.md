# RESTful Integration Guide

## Overview

In cases where our API is going to be called directly by a program, instead of a web browser, you need to follow the general outline of the examples listed here. This will ensure that you have a smooth integration process.

Their are two types of API requests, requests that require authorizations and ones that are general but still require the client id.

These examples are in PHP but any language will work.

### Make a general API call.

In this example, we will be calling the Stream Resource in order to get a list of currently live streams. It grabs the list from the web server, decodes the json, and outputs the name of the top stream.

```php
  $streams = json_decode(get_url_contents("https://api.twitch.tv/kraken/streams"));
  echo "name" . $streams->streams[0]->channel->name;
```

### Get an Oauth Token from Password Grant flow

You should only use this in the case that you cannot use the Javascript SDK for some reason. We do not offer password grants for the vast majority of cases. You need to explicitly get permission from twitch to use the password credential flow. It will fail with errors without our explicit permission. 

```php
  $login_params = array(
      'client_id'=> 'CLIENT_ID',
      'username' => 'USERNAME',
      'password' => 'PASSWORD'
  );

  $result = post_url_contents("https://api.twitch.tv/kraken/oauth2/token", $login_params);
  $access_result = json_decode($result);
  echo $access_result->access_token;
```

With that access token, you then can make API requests that require it.

### PHP Helper Functions

These functions were used above to simplify some of the PHP code

```php
function get_url_contents($url){
    $crl = curl_init();
    $timeout = 5;
    curl_setopt ($crl, CURLOPT_URL,$url);
    curl_setopt ($crl, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt ($crl, CURLOPT_CONNECTTIMEOUT, $timeout);
    $ret = curl_exec($crl);
    curl_close($crl);
    return $ret;
}

function post_url_contents($url, $fields) {

    foreach($fields as $key=>$value) { $fields_string .= $key.'='.urlencode($value).'&'; }
    rtrim($fields_string, '&');

    $crl = curl_init();
    $timeout = 5;

    curl_setopt($crl, CURLOPT_URL,$url);
    curl_setopt($crl,CURLOPT_POST, count($fields));
    curl_setopt($crl,CURLOPT_POSTFIELDS, $fields_string);

    curl_setopt ($crl, CURLOPT_RETURNTRANSFER, 1);
    curl_setopt ($crl, CURLOPT_CONNECTTIMEOUT, $timeout);
    $ret = curl_exec($crl);
    curl_close($crl);
    return $ret;
}
```