---
title: Point
---

Represents a single point in 2D space.

# Methods

## **new(float $x, float $y): Point**

Creates a new Point.

```
use JWare\GeoPHP\Point;

$point = new Point(3, 28);
$point2 = new Point($x=12.3, $y=-9.21);
```

## **clone(): Point**

Creates a Point's clone.

```
$point = new Point(3, 28);
$point2 = $point->clone();

$point2->isEqual($point); // True
```

## **getX(): float**

X coordinate getter.

```
$point = new Point(3, 28);
$point->getX(); // 3
```

## **setX(float $x): Point**

X coordinate setter. Returns the instance for chainable behaviour.

```
$point = new Point(3, 28);
$point->setX(33)->getX(); // 33
```

## **getY(): float**

Y coordinate getter.

```
$point = new Point(3, 28);
$point->getY(); // 28
```

## **setY(float $y): Point**

Y coordinate setter. Returns the instance for chainable behaviour.

```
$point = new Point(3, 28);
$point->setY(42)->getY(); // 42
```

## **getXandY(): array**

X and Y coordinates getter.

```
$point = new Point(3, 28);
$point->getXandY(); // [3, 28]
```

## **isEqual(Point $otherPoint): bool**

Checks if two point have the same coordinates.

```
$point = new Point(3, 28);
$point2 = new Point(3, 28);
$point3 = new Point(23, 12);

$point->isEqual($point2); // True
$point->isEqual($point3); // False
```

## **getMagnitude(): float**

Computes the magnitude of the point's vector.

```
$point = new Point(1, 2);
$point->getMagnitude(); // 2.236067977
```

## **fromRadiansToDegrees(): Point**

Converts x and y components of the Point from radians to degrees. Returns a Point with the new components.

```
$point = new Point(2, 3);

$pointConverted = $point->fromRadiansToDegrees();
$pointConverted->getXAndY(); // [114.5916, 171.8873]
```

## **fromDegreesToRadians(): Point**

Converts x and y components of the Point from degrees to radians. Returns a Point with the new components.

```
$point = new Point(57.29578, 0);

$pointConverted = $point->fromDegreesToRadians();
$pointConverted->getXAndY(); // [1, 0]
```

## **getAngle(Point $otherPoint, bool $inDegrees = true): float**

Computes the angle between two points. If `$inDegrees` is true the result is returned in degrees, in radians otherwise.

```
$point1 = new Point(2, 0);
$point2 = new Point(2, 2);

$point1->getAngle($point2); // 45
```

## **dotProduct(Point $otherPoint): float**

Computes the dot product of the two points: dot = x1 * x2 + y1 * y2.

```
$point1 = new Point(2, 4.5);
$point2 = new Point(1.5, 0.5);

$point1->dotProduct($point2); // 5.25s
```

## **crossProduct(Point $point2, Point $point3): float**

Computes the cross product of the three points. A positive value implies $this → #point2 → $point3 is counter-clockwise, negative implies clockwise.

```
$pointA = new Point(1, 2);
$pointB = new Point(3, 5);
$pointC = new Point(7, 12);

$pointA->crossProduct($pointB, $pointC); // 2
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