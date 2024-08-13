# Counting Minutes I

## Problem Description

The `countingMinutesI` function calculates the number of minutes between two given times. The input times are provided in the format `h:mm a`, which represents hours and minutes in a 12-hour format with AM/PM. The function accounts for cases where the second time may be on the following day.

## Implementation

The function utilizes the Luxon library to handle the time difference calculation. If the second time is earlier in the day than the first time (which would mean the end time is on the next day), the function adds 24 hours' worth of minutes to ensure an accurate difference.

## Function Definition

```javascript
import { DateTime } from "luxon";

function countingMinutesI(date1, date2) {
  const start_time = DateTime.fromFormat(date1, "h:mm a");
  const end_time = DateTime.fromFormat(date2, "h:mm a");

  let difference = end_time.diff(start_time, "minutes").minutes;
  if (difference < 0) {
    difference += 24 * 60;
  }
  return difference;
}

console.log(countingMinutesI("11:59 PM", "12:03 AM")); // Output: 4
console.log(countingMinutesI("9:00 AM", "10:15 AM")); // Output: 75
console.log(countingMinutesI("11:45 PM", "12:30 AM")); // Output: 45
console.log(countingMinutesI("1:00 PM", "1:00 PM")); // Output: 0
console.log(countingMinutesI("6:00 AM", "5:59 AM")); // Output: 1439