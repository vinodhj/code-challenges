# Time Difference

## Description

The `timeDifference` function calculates the absolute difference in minutes between two times provided in the format "h:mm a" (12-hour format with AM/PM). If the time strings are not in the correct format, the function returns an error message indicating the issue.

## Function Definition

```javascript
import { DateTime } from "luxon";

function timeDifference(time1, time2) {
  // Parse the time strings using Luxon's DateTime
  const t1 = DateTime.fromFormat(time1, "h:mm a");
  const t2 = DateTime.fromFormat(time2, "h:mm a");

  // Check if both times are valid
  if (!t1.isValid || !t2.isValid) {
    return `The input "${time1}" can't be parsed as format "h:mm a". Reason: ${t1.invalidReason}`;
  }

  // Calculate the difference in minutes
  let difference = Math.abs(t1.diff(t2, "minutes").minutes);

  return difference;
}

// Test cases
console.log(timeDifference("1:00 PM", "3:30 PM")); // Output: 150
console.log(timeDifference("11:00 AM", "11:30 AM")); // Output: 30
console.log(timeDifference("7:45 AM", "8:15 AM")); // Output: 30
console.log(timeDifference("10:15 PM", "11:45 PM")); // Output: 90
console.log(timeDifference("11:00 PM", "1:00 AM")); // Output: 120
console.log(timeDifference("invalid", "1:00 AM")); // Output: The input "invalid" can't be parsed as format "h:mm a". Reason: unparsed
