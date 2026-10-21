# Serverless Foundations — Raw Notes

## Exercise
- Platform: AWS Skill Builder SimuLearn
- Exercise: Serverless Foundations
- Function name: `LabFunction`
- Runtime: Python 3.11
- Language: Python

## Scenario
Use AWS Lambda to process visitor feedback without provisioning or managing servers, paying only for compute time used.

## Requirements
- Create a Lambda function.
- Deploy the function.
- Test the function.
- Modify the handler to map `emoji_type` values to feeling labels.

## Original Implementation
The handler reads two fields from the incoming event:
- `emoji_type`
- `message`

It prints both values and uses conditional logic to create a `custom_message`.

Original mapping:
- `emoji_type == 0`: Prefix the message with `Message for code 0: `
- `emoji_type == 1`: Prefix the message with `Message for code 1: `
- Other values: Prefix the message with `Message for all other codes: `

The function returns a dictionary containing `message` and `custom_message`.

## DIY Modification
Changed the conditional logic to map:
- `emoji_type == 0`: `positive`
- `emoji_type == 1`: `neutral`
- Other values: `negative`

The response retains the original `message` and includes the calculated `custom_message`.

## Architecture
The supplied diagram shows a client invoking a Lambda function and receiving a response. The exercise uses synchronous invocation.

## AWS Services
- AWS Lambda: Runs the Python handler.
- Amazon CloudWatch: Used to inspect the function's log events.

## Validation
- Created a test event.
- Invoked the function.
- Inspected CloudWatch log events.
- Captured the updated code and successful function update.

Exact test results and the number of test cases: To be confirmed from the saved screenshots.

## Personal Learning
- Lambda passes event data to the handler.
- The handler can read values from the event and use them in conditional logic.
- The function can return a response to a synchronous caller.
- Changing the conditional logic changes the returned feeling label.

## Evidence
- Exercise overview and supplied architecture diagram
- Function creation settings
- Successful function creation
- Original function code
- Test event and result
- CloudWatch log events
- DIY code modification

## Scope
This documents an AWS Skill Builder SimuLearn exercise, not an independently designed production system.