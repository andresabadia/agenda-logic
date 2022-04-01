<script setup lang="ts">
import { DATES } from "./models/DATES";

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
</script>

<template>
  <h1>Agenda</h1>
  <div v-for="date in dates" :key="date.name">
    {{ date.start }} - {{ date.name }} - {{ date.end }}
  </div>
  <br /><br />
  <div
    class="level"
    v-for="positionedDate in positionedDates"
    :key="positionedDate[0].name"
  >
    <span class="level-entry" v-for="date in positionedDate" :key="date.name">
      {{ date.start }}h - {{ date.name }} -{{ date.end }}h
    </span>
  </div>
  <br /><br /><br />
  <a href="https://github.com/andresabadia/agenda-logic/" target="_blank"
    >github</a
  >
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.level {
  margin-bottom: 10px;
}
.level-entry:not(:last-of-type) {
  margin-right: 10px;
}
.level-entry {
  background: lightblue;
  padding: 3px;
}
</style>
