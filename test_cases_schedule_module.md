# Test cases

## Test suite 1 &ndash; Notification setup

### **Test 1 &ndash; Basic case**

#### Setup

- Set up a list of schedule change types, which support notifications sending 
  [time change, teacher change, classroom change ...].

- Prepare mockup changes for each available change type.

- Create a student's schedule mockup including the course which will be subject to changes.

#### Steps

- Configure "change types" which trigger notification sending.
  - Choose randomly a subset of change types (for automated tests) and keep information about selected change types for later use.
  - Let a user select change types (for interactive tests).

- Fetch email address of recipient.
  - Use e-mail address provided in the currently logged user's profile, if available.
  - Let a user enter an e-mail address.

- Confirm changes made to the system.
  
- Update the object responsible for observing changes made to the schedule.
  - [__Assertion__] The fetched e-mail address has correct format.
  - [__Assertion__] Selected change types are available and supported. 
  - Update notification system.

- Wait until system finished the update.

- Simulate schedule change.
  - Choose a schedule change from mockup changes.
  - Store old values for comparison.
  - Change schedule item (e.g. time of a course in the schedule).
  - [__Assertion__] The schedule item now has a new value.

#### Assert

- [__Assertion__] Logged user has recieved the notification about the change in the schedule.

### **Test 2 &ndash; E-mail address with incorrect format**

#### Setup

- Select a notification sending triggering "change type".
  
- Hardcode / Provide an e-mail address with incorrect format.
  
#### Steps

- Allow notification sending for selected change type.

- Use hardcoded e-mail address as recipient address.

- Update the notification change observer.

#### Assert

- [__Assertion__] The system correctly recognizes incorrect e-mail address format and fails to update notification settings.

### **Test 3 &ndash; Unsaved notification settings configuration**

#### Setup

- Set up a list of schedule change types, which support notifications sending 
  [time change, teacher change, classroom change ...].

- Prepare mockup changes for each available change type.

- Create a student's schedule mockup including the course which will be subject to changes.

#### Steps

- Configure "change types" which trigger notification sending.
  - Choose randomly a subset of change types (for automated tests) and keep information about selected change types for later use.
  - Let a user select change types (for interactive tests).

- Fetch current notifications sending system configuration.
  - Get a list of "change types" which currently trigger notification sending.

- Change notification settings, but do NOT update the notifications sending system.

- Fetch current notifications sending system configuration _again_.

#### Assert

- [__Assertion__] Old and new notification system configurations have the same content (but the objects are different).

---

## Test suite 2 &ndash; Viewing tests

### **Test case 1 &ndash; View "My schedule" as logged in student**

#### Setup

- Log in as a student
  
- Mock schedule for this student

#### Steps

- Go to the schedule module page
  
- Click on the "My schedule" button.

- [__Assertion__] The schedule is shown.
  
- [__Assertion__] The schedule is in acordance with the mocked schedule data

### **Test 2 &ndash; View classroom schedule**

#### Setup
  
- Mock a classrom

- Mock a variable schedule for this classroom

#### Steps

- Go to the schedule module page
  
- Click on the "Classroom schedules" button.

- [__Assertion__] The mocked classroom is available in the list of classrooms

- Select the classrom and click "Show schedule" button

- [__Assertion__] The schedule is shown.
  
- [__Assertion__] The schedule is in acordance with the mocked schedule data

### **Test 3 &ndash; View subject schedule**

#### Setup
  
- Mock a subject with a schedule

- Mock a variable schedule for this subject

#### Steps

- Go to the schedule module page
  
- Click on the "Subject schedules" button.

- [__Assertion__] The mocked subject is available in the list

- Select the subject and click "Show schedule" button

- [__Assertion__] The schedule is shown.
  
- [__Assertion__] The schedule is in acordance with the mocked schedule data

### **Test 3 &ndash; View subject schedule**

#### Setup
  
- Mock a subject with a schedule

- Mock a variable schedule for this subject

#### Steps

- Go to the schedule module page
  
- Click on the "Subject schedules" button.

- [__Assertion__] The mocked subject is available in the list

- Select the subject and click "Show schedule" button

- [__Assertion__] The schedule is shown.
  
- [__Assertion__] The schedule is in acordance with the mocked schedule data

### **Test 4 &ndash; View unscheduled subject schedule**

#### Setup
  
- Mock a subject with a schedule

#### Steps

- Go to the schedule module page
  
- Click on the "Subject schedules" button.

- [__Assertion__] The mocked subject is available in the list

- Select the subject and click "Show schedule" button

- [__Assertion__] The info banner with text "This subject doesn't have a schedule yet." is visible.

- [__Assertion__] The schedule is not shown.

### **Test 5 &ndash; Fail to view private classroom schedule**

#### Setup
  
- Mock a private classroom with a schedule

- Mock a user without access right to view this schedule

#### Steps

- Go to the schedule module page
  
- Click on the "Classroom schedules" button.

- [__Assertion__] The mocked classroom is available in the list

- Select the subject and click "Show schedule" button

- [__Assertion__] The info banner with text "This classroom is private." is visible.

- [__Assertion__] The schedule is not shown.

---

