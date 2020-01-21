---
title: Getting Started
---

## Pre-requisites

GeoPHP was tested on PHP >= 7. Please, let PHP 5 die!

## Installation

Install the library running:

`composer require jware/geophp`

## Usage

```
use \JWare\GeoPHP\Polygon;
use \JWare\GeoPHP\Point;

$polygon = new Polygon([
    new Point(1, -1),
    new Point(2, 1),
    new Point(3, -1),
    new Point(2, -2),
    new Point(1, -1)
]);

$point = new Point(-1, 2);
$point2 = new Point(2, 2);

$polygon->containsPoint($point); // False
$polygon->containsPoint($point2); // True
```

Please read the documentation to see the full method list available.