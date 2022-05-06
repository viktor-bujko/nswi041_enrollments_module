# Test cases

## Test &ndash; Notification setup

### Test 1 &ndash; Basic case

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

### Test 2 &ndash; E-mail address with incorrect format

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

### Test 3 &ndash; Unsaved notification settings configuration

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

- [__Assertion__] Both notification system configurations are the same (the old and the new one) &ndash; notification sending rules have not changed.