# Main logic

```ts
export interface DATES {
  name: string;
  start: number;
  end: number;
}

const dates: DATES[] = [
  { name: "test1", start: 8, end: 10 },
  { name: "test3", start: 9, end: 14 },
  { name: "test2", start: 9, end: 11 },
  { name: "test4", start: 10, end: 12 },
  { name: "test5", start: 11, end: 12 },
  { name: "test6", start: 12, end: 14 },
  { name: "test7", start: 12, end: 14 },
];

const positionedDates = [[]] as DATES[][];

for (let i = 0; i < dates.length; i++) {
  // first element put it to the first level of the positions array
  if (i === 0) {
    positionedDates[0].push(dates[i]);
  } else {
    // loop trough the levels of the array
    for (let j = 0; j < positionedDates.length; j++) {
      const lastElementInLevel =
        positionedDates[j][positionedDates[j].length - 1];
      const currentElement = dates[i];
      if (lastElementInLevel.end <= currentElement.start) {
        // does not overlaps. Add it to the current level and exit the loop
        positionedDates[j].push(dates[i]);
        break;
      }
      // else it overlaps check next level
      // if last level overlaps. Create new level
      if (positionedDates.length - 1 === j) {
        positionedDates.push([dates[i]]);
        break;
      }
    }
  }
}
```
