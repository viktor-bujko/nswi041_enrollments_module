# Test cases

## Test &ndash; Notification setup

### Test 1 &ndash; Basic case

#### Setup

- Set up a list of schedule change types, which support notifications sending 
  [time change, teacher change, classroom change ...].

- Prepare mockup changes for each available change type.

- Create a student's schedule mockup including the course which will be subject
  to changes.

#### Steps

- Configure "change types" which trigger notification sending.
  - Choose randomly a subset of change types (for automated tests) and keep information about
    selected change types for later use.
  - Let a user select change types.

- Fetch email address of recipient.
  - Find whether e-mail address is provided in the currently logged user's profile.
  - Provide an e-mail address.

- Confirm changes made to the system.
  
- Update the object responsible for observing changes made to the schedule.
  - [__Assertion__] Selected change types are available and supported. 
  - [__Assertion__] The fetched e-mail address has correct format.
  - Update notification system.

- Wait until system finished update.

- Simulate schedule change.
  - Choose a schedule change from mockup changes.
  - Store old values for comparison.
  - Change schedule item (e.g. time of a course in the schedule).
  - [__Assertion__] The schedule item now has a new value.

#### Assert

- Logged user has recieved the notification about the change in the schedule.

### Test 2 &ndash; E-mailová address with incorrect format

#### Setup
#### Steps
#### Assert

### Test 3 &ndash; Unsaved notification settings configuration

#### Setup
#### Steps
#### Assert