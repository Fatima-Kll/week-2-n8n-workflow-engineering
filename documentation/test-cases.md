# Workflow Test Cases

## Purpose

Verify the workflow's main processing paths, integrations, and behavior when unexpected conditions occur.

## Test Results

Update the status column after executing each test. Do not mark a test as passed until you have verified its result.

| ID | Test Scenario | Expected Result | Status |
|---|---|---|---|
| TC-01 | Submit a valid service request | Request is added to Google Sheets and customer receives confirmation email | Passed |
| TC-02 | Trigger the rejection branch | Rejection metadata is generated and internal Gmail alert is sent | Passed |
| TC-03 | Submit a request with an invalid email format | Form validation prevents an invalid email submission | Not yet verified |
| TC-04 | Test a missing required field | Form validation prevents submission or IF routes the item to FALSE | Not yet verified |
| TC-05 | Test Google Sheets with unavailable or invalid credentials | Workflow reports an integration error | Not yet verified |
| TC-06 | Test Gmail with unavailable or invalid credentials | Workflow reports an email delivery error | Not yet verified |

## Notes

- TC-01 and TC-02 have been tested successfully.
- The form itself marks Full Name, Email, and Service as required. Consequently, missing fields may be blocked by the form before reaching the IF node.
- To test the IF rejection path, a controlled test condition can be used temporarily and then restored.
- Integration failure tests should be performed carefully, without changing production credentials permanently.

## Test Summary

The successful and rejection paths have been verified. Additional form-validation and integration-failure tests remain to be completed.
