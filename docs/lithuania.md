---
title: Lithuanians in US
---

<style>
h1 {
  margin: 2rem 0;
  max-width: none;
  font-family: var(--sans-serif);
  font-size: 3vw;
  font-weight: 900;
  line-height: 1;
  background: linear-gradient(30deg, var(--theme-foreground-focus), currentColor);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
</style>

# Lithuanians in the United States

Let's use Observable to explore [states.xlsx](./data/states.xlsx). This Excel Workbook contains data about Lithuanian-born people living in the United States&mdash;organized by state and census year starting in 1920.

This file is written in Markdown and you can edit the source in `/docs/lithuania.md`. Data files for all the examples below are stored in `/docs/data/`.

## Importing Excel Files

Observable has built-in support for parsing Excel files via [Excel.js](https://github.com/exceljs/exceljs). You can load your workbook using the following JavaScript code:

```js echo
const workbook = FileAttachment("./data/states.xlsx").xlsx();
```

If we inspect `workbook` we can see information about the sheets in our Excel file. Click on the arrow to expand the `Workbook` and explore the data:


```js echo
workbook
```

In this example we're going to look at data in the `LtBorn` sheet. Using the `sheet()` method we can extract the rows and columns we need and make them available as a JavaScript object. 

```js echo
const reports = workbook.sheet("LtBorn", {range: "C3:M56", headers: true});
```

Now, if we inspect `reports` just like we did with `workbook` above&mdash;we should see a JavaScript object containing the rows and columns we requested from `states.xlsx`. By default, each object represents a row, and each object property represents a cell value. Click on the arrow to expand the `Array(56)` and explore the data:

```js echo
reports
```

## Exploring Data

The easiest first step is to reproduce a nice table so we can verify our data looks as we expect:

```js echo
Inputs.table(reports)
```
```js echo
Plot.plot({
  projection: "albers-usa",
  marks: [
    Plot.geo(nation),
    Plot.geo(statemesh, {strokeOpacity: 0.2})
  ]
})
```

A chart, perhaps? Let's give the user a slider to select the census year:

```js echo
const census = view(Inputs.range([1920, 2030], {step: 10}));
```

```js echo
Plot.plot({
  x: {grid: true, axis: "both"},
  marks: [
    Plot.barX(reports, {x: census.toString(), y: "C"}),
    Plot.ruleX([0])
  ]
})
```