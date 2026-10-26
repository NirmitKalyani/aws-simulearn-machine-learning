# Image and Video Analysis — Raw Notes

## Exercise
- Platform: AWS Skill Builder SimuLearn
- Exercise: Image and Video Analysis
- Language: Python
- Primary services: Amazon S3, AWS Lambda, Amazon Rekognition

## Scenario
The Space Administration Department wants to identify UFOs flying over a city.

The solution uses Amazon Rekognition to detect and label objects in images uploaded to Amazon S3. AWS Lambda processes the uploads and stores the analysis results as JSON in S3.

## Requirements
- Configure an S3 bucket with input and output locations.
- Create an AWS Lambda function to process uploaded images.
- Configure Amazon Rekognition label detection.
- Configure S3 event notifications to invoke Lambda when an image is uploaded.
- Support JPG and PNG image uploads.
- Validate that the resulting JSON file contains the expected labels.

## Implementation
- S3 stores uploaded images in the input location and analysis results in the output location.
- S3 PUT event notifications invoke the Lambda function when new images are uploaded.
- Lambda reads the bucket name and object key from the incoming S3 event.
- Lambda calls Amazon Rekognition's `DetectLabels` API with a minimum confidence threshold of `70`.
- Detected label names are converted to lowercase.
- The function checks whether the configured label appears in the detected labels.
- The result is serialized as JSON and written to `output/rekognition_response.json`.
- The supplied `lambda.zip` contains `index.py`. Its `LABEL` variable still contains a placeholder, so the final console version should be checked separately.

## DIY Modification
The DIY task is to modify the Lambda implementation to detect a new label, `spaceship`.

- Upload `spaceship.png` to the S3 input location.
- Validate that the resulting JSON response contains `spaceship` as a detected label.
- Screenshots documenting the code modification, upload, and response are available.

## Architecture
The workflow shown in the supplied SimuLearn diagram is:

1. A user uploads an image to the S3 input location.
2. An S3 PUT event invokes the Lambda function.
3. Lambda calls Amazon Rekognition to detect image labels.
4. Rekognition returns the detected labels.
5. Lambda checks for the configured label.
6. Lambda writes the JSON response to the S3 output location.

The architecture diagram is saved separately as `architecture.png`.

## AWS Services
- **Amazon S3:** Stores input images and generated JSON responses. S3 event notifications trigger Lambda when an image is uploaded.
- **AWS Lambda:** Processes S3 events, invokes Rekognition, checks detected labels, and writes the response to S3.
- **Amazon Rekognition:** Detects objects and labels in images using the `DetectLabels` API.

## Validation
- Uploaded the sample airplane image and inspected its response.
- Uploaded the sample horse image and inspected its response.
- Modified the implementation for the spaceship DIY task.
- Uploaded `spaceship.png` and inspected the response.
- Verified the output JSON using the available screenshots.

Exact detected labels and confidence scores have not yet been recorded from the JSON files.

## Personal Learning
- S3 event notifications can trigger serverless processing when objects are uploaded.
- Lambda can coordinate image processing by calling a managed AI service.
- Amazon Rekognition provides label detection without requiring a custom image-recognition model for this exercise.
- JSON output provides a way to inspect and validate processing results.
- Output naming and exception handling are important considerations when designing reliable event-driven workflows.

## Evidence
- `architecture.png` — cleaned-up architecture diagram.
- `lab-files/` — sample images, Lambda ZIP archive, and JSON response files.
- `screenshots/` — evidence of S3 configuration, Lambda creation and configuration, event notifications, image uploads, code modification, and output validation.

## Scope
This documents an AWS Skill Builder SimuLearn learning exercise, not an independently designed production system.