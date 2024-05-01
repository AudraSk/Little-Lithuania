# Test

One two three four, paragraph is appearing here

```js
const workbook = FileAttachment("./data/test.xlsx").xlsx();
```

```js
workbook 
```

```js
const reports = workbook.sheet("Sheet1", {range: "B2:BA5", headers: true});
```

```js
reports
```

```js
Inputs.table(reports)
```

```js
reports[2].Georgia + reports[2].Alabama
```

```js
Plot.plot({
  x: {grid: true, axis: "both"},
  marks: [
    Plot.barX(reports, {x: "Total Population", y: "C"}),
    Plot.ruleX([0])
  ]
})
```

