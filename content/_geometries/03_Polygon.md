---
title: Polygon
---

A bounded two-dimensional area.

# Methods

## **new(array $points): Polygon**

Creates a new Polygon. The polygon has to have at least three diferent points, and first and last point must have the same coordinates! Otherwise it will throw `\JWare\GeoPHP\Exceptions\NotEnoughPointsException` or `\JWare\GeoPHP\Exceptions\FirstAndLastPointNotEqualException` exceptions respectively.

```
use JWare\GeoPHP\Poing;
use JWare\GeoPHP\Polygon;
use \JWare\GeoPHP\Exceptions\FirstAndLastPointNotEqualException;

$polygon = new Polygon([
    new Point(0, 0),
    new Point(4, 0),
    new Point(4, 4),
    new Point(0, 4),
    new Point(0, 0),
]);

// Invalid polygons
try {
    // Has only 2 different points!
    $invalidPolygon = new Polygon([
        new Point(0, 1),
        new Point(3, 1),
        new Point(1, 1) 
    ]);
} catch (NotEnoughPointsException $e) {
    echo 'Opps! Exception: ',  $e->getMessage(), "\n";
}

try {
    $invalidPolygon = new Polygon([
        new Point(0, 1),
        new Point(3, 1),
        new Point(4, 2),
        new Point(1, 1) // Not equals to first point
    ]);
} catch (FirstAndLastPointNotEqualException $e) {
    echo 'Opps! Exception: ',  $e->getMessage(), "\n";
}
```

## **clone(): Polygon**

Creates a Polygon's clone

```
$polygon = new Polygon([
    new Point(0, 0),
    new Point(4, 0),
    new Point(4, 4),
    new Point(0, 4),
    new Point(0, 0),
]);

$clone = $polygon->clone();
```

## **getPoints(): array**

All the polygon's points' getter.

```
$polygon = new Polygon([
    new Point(0, 0),
    new Point(4, 0),
    new Point(2, 4),
    new Point(0, 0)
]);

$polygon->getPoints(); // [Point(0, 0), Point(4, 0), Point(2, 4), Point(0, 0)]

```

## **setPoint(int $idx, Point $point): Polygon**

Setter for one point of the polygon. `$idx` is the index in the array (starting from 0) of the polygon to replace and `$point` Point to put in the specified position. `$idx` can't be the first nor the last Point of the Polygon, otherwise it will throw an `\JWare\GeoPHP\Exceptions\SettingPointException` exception.

```
$polygon = new Polygon([
    new Point(0, 0),
    new Point(4, 0),
    new Point(2, 4),
    new Point(0, 0)
]);

$polygon->setPoint(2, new Point(5, 6));
$polygon->getPoints(); // [Point(0, 0), Point(4, 0), Point(5, 6), Point(0, 0)]
```

## **getCentroid(): Point**

Computes the polygon's centroid.

```
$polygon = new Polygon([
    new Point(-81, 41),
    new Point(-88, 36),
    new Point(-84, 31),
    new Point(-80, 33),
    new Point(-77, 39),
    new Point(-81, 41)
]);

$centroid = $polygon->getCentroid(); // Point(-82, 36)
```

## **area(): float**

Get the Polygon's area. Uses the [Shoelace Formula](https://en.wikipedia.org/wiki/Shoelace_formula).

```
$polygon = new Polygon([
    new Point(0, 0),
    new Point(4, 0),
    new Point(4, 4),
    new Point(0, 4),
    new Point(0, 0),
]);

$polygon1->area(); // 16
```

## **intersectsPoint(Point $point): bool**

Checks whether the polygon intersects a point. A Polygon intersects a Point if at least one of its lines intersects the Point.

```
$polygon = new Polygon([
    new Point(2, 4),
    new Point(4, 4),
    new Point(5, 2),
    new Point(3, 1),
    new Point(2.5, 3),
    new Point(2, 4)
]);

$polygon->intersectsPoint(new Point(3, 4); // True
$polygon->intersectsPoint(new Point(5, 4); // False
```

## **intersectsLine(Line $line): bool**

Checks whether the polygon intersects a line.

```
$polygon = new Polygon([
    new Point(2, 4),
    new Point(4, 4),
    new Point(4, 2),
    new Point(3, 1),
    new Point(2.5, 3),
    new Point(2, 4)
]);

$line1 = new Line(
    new Point(1, 1),
    new Point(5, 5)
);

$line2 = new Line(
    new Point(-1, 1),
    new Point(-5, -10)
);

$polygon->intersectsLine($line1); // True
$polygon->intersectsLine($line2); // False
```

## **intersectsPolygon(Polygon $polygon): bool**

Checks whether the polygon intersects another polygon.

```
$polygon1 = new Polygon([
    new Point(2, 4),
    new Point(4, 4),
    new Point(5, 2),
    new Point(3, 1),
    new Point(2.5, 3),
    new Point(2, 4)
]);

$polygon2 = new Polygon([
    new Point(-3, -4),
    new Point(-1, -5),
    new Point(-2, -6),
    new Point(-3, -4)
]);

$polygon3 = new Polygon([
    new Point(4, 3),
    new Point(6, 2.5),
    new Point(6, 1.5),
    new Point(4.5, 1.25),
    new Point(4, 3)
]);

$polygon1->intersectsPolygon($polygon3); // True
$polygon1->intersectsPolygon($polygon2); // False
```

## **euclideanDistance(Point $otherPoint): float**

Computes the euclidean distance between two points.

```
$point = new Point(1, 2);
$point2 = new Point(4, 5);

$point->euclideanDistance($point2); // 4.243
```

## **intersectsLine(Line $line): bool**

Checks whether the point intersects a line.

```
$line = new Line(
    new Point(1, 1),
    new Point(5, 5)
);
$point = new Point(3, 3);
$point2 = new Point(3, 4);

$point->intersectsLine($line); // True
$point2->intersectsLine($line); // False
```

## **intersectsPoint(Point $otherPoint): bool**

Checks whether the point intersects with another point. Two points intersect if they have the same X and Y coordinates (same as `isEqual` method).

```
$point = new Point(3, 3);
$point2 = new Point(3, 4);
$point3 = new Point(3, 4);

$point->intersectsPoint($point2); // False
$point2->intersectsPoint($point3); // True
```

## **intersectsPolygon(Polygon $polygon): bool**

Checks whether the point intersects with a polygon.

```
$polygon = new Polygon([
    new Point(1, 1),
    new Point(3, 3),
    new Point(2, 7),
    new Point(4, 5),
    new Point(7, 5),
    new Point(1, 1)
]);
$point = new Point(3, 3);
$point2 = new Point(3, 4);

$point->intersectsPolygon($Polygon); // True
$point2->intersectsPolygon($Polygon); // False
```

## **containsPoint(Point $point): bool**

Checks whether a point is inside a polygon.

```
$polygon = new Polygon([
    new Point(0, 0),
    new Point(4, 0),
    new Point(4, 4),
    new Point(0, 4),
    new Point(0, 0)
]);

$polygon->containsPoint(new Point(2, 2)); // True
$polygon->containsPoint(new Point(10, 12)); // False
```

## **containsLine(Line $line): bool**

Checks whether the polygon contains a line.

```
$polygon = new Polygon([
    new Point(0, 0),
    new Point(4, 0),
    new Point(4, 4),
    new Point(0, 4),
    new Point(0, 0)
]);
$line1 = new Line(
    new Point(2, 2),
    new Point(3, 3)
);
$line2 = new Line(
    new Point(-1, -1),
    new Point(2, 3)
);

$polygon->containsLine($line1); // True
$polygon->containsLine($line2); // False
```

## **containsPolygon(Polygon $polygon): bool**

Checks whether the polygon contains another polygon.

```
$polygon1 = new Polygon([
    new Point(0, 0),
    new Point(4, 0),
    new Point(4, 4),
    new Point(0, 4),
    new Point(0, 0)
]);
$polygon2 = new Polygon([
    new Point(4, 0),
    new Point(8, 0),
    new Point(8, 4),
    new Point(4, 4),
    new Point(4, 0)
]);

$polygon3 = new Polygon([
    new Point(1, 2),
    new Point(2, 2),
    new Point(2, 3),
    new Point(1, 2)
]);

$polygon1->containsPolygon($polygon3) // True
$polygon1->containsPolygon($polygon2) // False
```