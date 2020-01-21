---
title: Line
---

A line segment made up of exactly two [Points](#point).

# Methods

## **new(Point $start, Point $end): Line**

Creates a new Line.

```
use JWare\GeoPHP\Line;
use JWare\GeoPHP\Point;

$line = new Line(new Point(3, 28), new Point(-2, -9));
```

## **clone(): Line**

Creates a Line's clone

```
$line = new Line(new Point(3, 28), new Point(-2, -9));
$line2 = $line->clone();
```

## **getStart(): Point**

Starting point's getter of the line.

```
$line = new Line(new Point(1, -2), new Point(-2, -9));
$line->getStart(); // Point(1, -2)
```

## **setStart(Point $start): Line**

Starting point's setter. Returns the instance for chainable behaviour.

```
$line = new Line(new Point(1, -2), new Point(-2, -9));
$line->setStart(new Point(9, 9))->getStart(); // Point(9, 9)
```

## **getEnd(): Point**

Ending point's getter of the line.

```
$line = new Line(new Point(1, -2), new Point(-2, -9));
$line->getEnd(); // Point(-2, -9)
```

## **setEnd(Point $end): Line**

Ending point's setter. Returns the instance for chainable behaviour.

```
$line = new Line(new Point(1, -2), new Point(-2, -9));
$line->setEnd(new Point(92, 19))->getEnd(); // Point(92, 19)
```

## **determinant(): float**

Computes the determinant of the line.
Determinant = line.start.x * line.end.y - line.start.y * line.end.x

```
$line = new Line(
    new Point(1.34, 2.87),
    new Point(3.23, 4.5)
);

$line->determinant(); // -3.2401
```

## **dx(): float**

Computes the difference in 'x' components (Δx): line.end.x - line.start.x.

```
$line = new Line(
    new Point(2.77, 4.23),
    new Point(2.77, 7.23)
);

$line->dx(); // 0
```

## **dy(): float**

Computes the difference in 'y' components (Δy): line.end.y - line.start.y.

```
$line = new Line(
    new Point(2.77, 14.32),
    new Point(3.77, 9.55)
);

$line->dy(); // -4.77
```

## **slope(): float**

Computes the slope of a line: line.dy() / line.dx()

```
$line = new Line(
    new Point(3.45, 11.3),
    new Point(0.87, 34.243)
);

$line->slope(); // -8.8926
```

## **getPoints(): array**

Getter for starting and ending points.

```
$line = new Line(
    new Point(2, 34),
    new Point(2, 11)
);

$points = $line->getPoints(); // [Point(2, 34), Point(2, 11)]
$points[0]->isEquals($points[1]); // False
```

## **intersectsPoint(Point $point): bool**

Checks whether the line intersects a point.

```
$line = new Line(
    new Point(1, 1),
    new Point(5, 5)
);
$point1 = new Point(3, 3);
$point2 = new Point(-1, 1);

$line->intersectsPoint($point1); // True
$line->intersectsPoint($point2); // False
```

## **intersectsLine(Line $line): bool**

Checks whether the line intersects another line.

```
$line1 = new Line(
    new Point(1, 1),
    new Point(5, 5)
);
$line2 = new Line(
    new Point(3, 3),
    new Point(5, 1)
);
$line3 = new Line(
    new Point(-1, 1),
    new Point(-5, -10)
);

$line1->intersectsLine($line2); // True
$line1->intersectsLine($line3); // False
```

## **intersectsPolygon(Polygon $polygon): bool**

Checks whether the line intersects a polygon.

```
$line = new Line(
    new Point(1, 1),
    new Point(5, 5)
);
$polygon = new Polygon([
    new Point(2, 4),
    new Point(4, 4),
    new Point(4, 2),
    new Point(3, 1),
    new Point(2.5, 3),
    new Point(2, 4)
]);

$line->intersectsPolygon($polygon); // True
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
