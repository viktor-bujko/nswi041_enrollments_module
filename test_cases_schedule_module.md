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
  - Create new system state representation (which includes new notification
  sending settings).

- Fetch email address of recipient.
  - Use e-mail address provided in the currently logged user's profile, if available.
  - Let a user enter an e-mail address.
  
- Update the object responsible for observing changes made to the schedule.
  - [__Assertion__] The fetched e-mail address has correct format.
  - [__Assertion__] Selected change types are available and supported. 
  - Confirm changes made to the system.

- Wait until the system finishes the update.

- Simulate schedule change.
  - Choose a schedule change from mockup changes.
  - Store old values for comparison.
  - Change schedule item (e.g. time of a course in the schedule).
  - [__Assertion__] The schedule item now has a new value.

#### Assert

- [__Assertion__] Logged user has recieved a (e-mail) notification about the change in the schedule.

### **Test 2 &ndash; E-mail address with incorrect format**

#### Setup

- Select a "change type", which triggers notification sending.
  
- Hardcode / Provide an e-mail address with incorrect format.
  
#### Steps

- Allow notification sending for selected change type.

- Use hardcoded e-mail address as recipient address.

- Update the notification change observer.
  - [__Assertion__] System recognizes incorrect e-mail address format.

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
  - Do NOT create a new system state representation.

- Fetch current notifications sending system configuration.
  - Get a list of "change types" which currently trigger notification sending.

- Select a change type which does NOT trigger notification sending.

- Update the object responsible for observing changes made to the schedule.
  - [__Assertion__] System recognizes, that the settings have not changed.
  - [__Assertion__] System does NOT update its state.

- Fetch current notifications sending system configuration _again_.

- Simulate a change in the schedule based on the previously selected change type.
  [__Assertion__] The user should NOT receive any notification.

#### Assert

- [__Assertion__] Old and new notification system configurations have the same content (but the objects are different).

- [__Assertion__] Both notification system configurations are the same (the old and the new one) &ndash; notification sending rules have not changed.

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
  
- [__Assertion__] The schedule is in accordance with the mocked schedule data

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
  
- [__Assertion__] The schedule is in accordance with the mocked schedule data

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
  
- [__Assertion__] The schedule is in accordance with the mocked schedule data

### **Test 4 &ndash; Fail to view unscheduled subject schedule**

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

## Test suite 3 &ndash; Creating a schedule

### **Test 1 &ndash; User correctly creates schedule for the faculty**

#### Setup

- Create subject entities with empty schedules

#### Steps

- Go to schedule module page.
- Click on "Create schedule" button.
- User assign subject and type of the lesson to teacher, room, date and time until all lessons of all subjects are scheduled.

#### Assert
- [__Assertion__] Assigned lesson appears in the schedule of the selected teacher and selected room.

### **Test 2 &ndash; User does not have permissions to create the schedule**

#### Setup

- Log in as user without permissions to create schedules.

#### Steps

- Go to schedule module page.

#### Assert

- [__Assertion__] There is no "Create schedule button".
- [__Assertion__] If the user attemps to emulate click to the invisible "Create schedule button" button, error message is shown.

### **Test 3 &ndash; Two subjects in the same room at the same time**

#### Setup

- Create two subject entities - `Subject 1` with a single lesson in the `Room 1` on `Monday` from `10:40` to `12:10` in its schedule and `Subject 2` with an empty schedule

#### Steps

- Go to schedule module page.
- Click on "Create schedule" button.
- User attemps to create lesson of `Subject 2` in the `Room 1` on `Monday` from `9:55` to `11:30`.

#### Assert

- [__Assertion__] Error message is shown because the room is already occupied at the given time.


### **Test 4 &ndash; Fail final schedule validation**

#### Setup

- Create schedule of several subjects for several teachers with one of following errors:
  -  subject does not have one of its parts scheduled
  -  teacher has more than allowed number of lessons, 
  -  capacity of lesson is greater than capacity of its room

#### Steps

- Go to schedule module page.
- Click on "Create schedule" button.
- Click on "Validate schedule" button.

#### Assert

- [__Assertion__] An error message with description of the error is shown.

### **Test 5 &ndash; Teacher does not have a lunch break**

#### Setup

- System is configured to check for lunch break between `11:30` and `14:00` of at least 20 minutes straight.
- Create mock subject and teacher.

#### Steps 

- Create lesson for the teacher on `Monday` from `10:40` to `12:10`.
- Create another lesson for the on `Monday` from `12:20` to `13:50`.

#### Assert

- [__Assertion__] A message informing of the missing lunch break on `Monday` is shown.