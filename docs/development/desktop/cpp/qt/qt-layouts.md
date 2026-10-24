# Qt Layouts

[← back](index.md)

Qt layouts arrange widgets inside a container and update their geometry when the container is resized. They avoid fixed coordinates and make interfaces adapt to window size, content, fonts, and platform settings.

## Summary

- [Layout types](#layout-types)
- [Space allocation](#space-allocation)
- [Basic rules](#basic-rules)

## Layout types

| Layout | Arrangement |
|---|---|
| [QHBoxLayout and QVBoxLayout](qt-layouts/box-layouts.md) | A horizontal row or a vertical column |
| [QGridLayout](qt-layouts/grid-layout.md) | A grid of rows and columns, with items spanning multiple cells |

Layouts can contain widgets and other layouts.

## Space allocation

[Space allocation, margins/paddings, and spacing](qt-layouts/space-distribution.md) explains how a layout allocates available space to widgets and nested layouts, and distinguishes allocated area from margins, gaps, and spacer items.

## Basic rules

* A container widget normally has one top-level layout.
* A layout manages widget position and size; avoid calling `setGeometry()` on widgets managed by a layout.
* Layouts respect widget size hints, minimum and maximum sizes, size policies, and stretch factors.
* Use nested layouts to build more complex rows and columns.
