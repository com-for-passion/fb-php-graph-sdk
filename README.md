# Facebook SDK for PHP (v5)

[![Build Status](https://img.shields.io/travis/facebook/php-graph-sdk/5.x.svg)](https://travis-ci.org/facebook/php-graph-sdk)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/facebook/php-graph-sdk/badges/quality-score.png?b=5.x)](https://scrutinizer-ci.com/g/facebook/php-graph-sdk/?branch=5.x)
[![Latest Stable Version](http://img.shields.io/badge/Latest%20Stable-5.7.0-blue.svg)](https://packagist.org/packages/facebook/graph-sdk)

This repository contains the open source PHP SDK that allows you to access the Facebook Platform from your PHP app.

## Installation

The Facebook PHP SDK can be installed with [Composer](https://getcomposer.org/). Run this command:

```sh
composer require com-for-passion/fb-php-graph-sdk
```

Please be aware, that there are issues when using the Facebook SDK together with [Guzzle](https://github.com/guzzle/guzzle) 6.x. php-graph-sdk v5.x only works with Guzzle 5.x out of the box. However, [there is a workaround to make it work with Guzzle 6.x](https://www.sammyk.me/how-to-inject-your-own-http-client-in-the-facebook-php-sdk-v5#writing-a-guzzle-6-http-client-implementation-from-scratch).

## Upgrading to v5.x

Upgrading from v4.x? Facebook PHP SDK v5.x introduced breaking changes. Please [read the upgrade guide](https://www.sammyk.me/upgrading-the-facebook-php-sdk-from-v4-to-v5) before upgrading.

## Usage

> **Note:** This version of the Facebook SDK for PHP requires PHP 5.4 or greater.

Simple GET example of a user's profile.

```php
require_once __DIR__ . '/vendor/autoload.php'; // change path as needed

$fb = new \Facebook\Facebook([
  'app_id' => '{app-id}',
  'app_secret' => '{app-secret}',
  'default_graph_version' => 'v2.10',
  //'default_access_token' => '{access-token}', // optional
]);

// Use one of the helper classes to get a Facebook\Authentication\AccessToken entity.
//   $helper = $fb->getRedirectLoginHelper();
//   $helper = $fb->getJavaScriptHelper();
//   $helper = $fb->getCanvasHelper();
//   $helper = $fb->getPageTabHelper();

try {
  // Get the \Facebook\GraphNodes\GraphUser object for the current user.
  // If you provided a 'default_access_token', the '{access-token}' is optional.
  $response = $fb->get('/me', '{access-token}');
} catch(\Facebook\Exceptions\FacebookResponseException $e) {
  // When Graph returns an error
  echo 'Graph returned an error: ' . $e->getMessage();
  exit;
} catch(\Facebook\Exceptions\FacebookSDKException $e) {
  // When validation fails or other local issues
  echo 'Facebook SDK returned an error: ' . $e->getMessage();
  exit;
}

$me = $response->getGraphUser();
echo 'Logged in as ' . $me->getName();
```

Complete documentation, installation instructions, and examples are available [here](docs/).
