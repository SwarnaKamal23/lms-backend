```js
// npm install -g json-server
// json-server --watch db.json --port 3001
```

```js
// Step 1 : Step 1: Filter all entries of batchId 101

const enrolled = studentBatches.filter(batch => batch.batchId === 101);


// o/p of enrolled
[
  {
    studentId: 1,
    batchId: 101,
    leaveSummaryStats: { ... },
    leaveBreakdownStats: { ... },
    workHourStats: { ... }
  },
  {
    studentId: 3,
    batchId: 101,
    leaveSummaryStats: { ... },
    leaveBreakdownStats: { ... },
    workHourStats: { ... }
  }
]
```

```js
// Step 2 : Step 2: Join each enrolled entry with the matching student details

const studentDetails = enrolled.map(batchEntry => {
  const student = students.find(student => student.id === batchEntry.studentId);
  return {
    ...student,
    ...batchEntry  // brings in stats like leaveSummaryStats, etc.
  };
});

// o/p of studentDetails
[
  {
    id: 1,
    name: "Rahul Sharma",
    phone: "9876543210",
    email: "rahul.sharma@example.com",
    joinedOn: "2023-07-15",
    studentId: 1,
    batchId: 101,
    leaveSummaryStats: {
      onTime: 250,
      lateAttendance: 4,
      workFromHome: 100,
      absent: 2,
      sickLeaves: 3,
      performanceMessage: "Better than 80% of students"
    },
    leaveBreakdownStats: { ... },
    workHourStats: { ... }
  },
  {
    id: 3,
    name: "Karan Mehta",
    phone: "9012345678",
    email: "karan.mehta@example.com",
    joinedOn: "2023-06-20",
    studentId: 3,
    batchId: 101,
    leaveSummaryStats: {
      onTime: 200,
      lateAttendance: 6,
      workFromHome: 120,
      absent: 4,
      sickLeaves: 6,
      performanceMessage: "Better than 65% of students"
    },
    leaveBreakdownStats: { ... },
    workHourStats: { ... }
  }
]

```