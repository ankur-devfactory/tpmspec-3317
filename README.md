# AWS Connect API's Demo
Application to use AWS Connect API's to create AWS Connect Contacts flow

# Prerequisites:
* An AWS account
* An existing Amazon Connect instance or instances
* Access to AWS IAM, CloudFront, S3 services

# Steps:
* Create a CloudFormation stack from the Template
* Once done Cloudformation would deploy the website on AWS Cloudfront and you would get its access URL from Output parameter of CloudFormation.
* Configure the application with required credentials:
   - Populate access key/secret key as your Access key and secret key.
   - Backup DB: Name of the dynamo db table for backing up contact flows
   - ARN Mapping: Name of the dynamo db table created for mapping ARNs of objects between the two Amazon Connect instances
   - Instance ID: Would be your AWS Connect Instance ID. Follow this link to know how to get the AWS Connect Instance ID.
   - Region: AWS Region
* For Target Instance, you can use the same credentials or create a new AWS Connect Instance and use that as Instance ID.

# Testing
* Get all the contact flows in each instances by clicking on Get all Contact Flows
   - To view the Flow language JSON Output of a flow click on "Details".
   - To rename a Flow, click on "Rename"
   - To copy the flow to Target AWS Connect click on "Promote".
   - To Backup the selected flow on Dynamo DB, first select the flow you want to backup and then click on "Backup Selected Flows".
* Create a contact flow by using Create Contact Flow functionality in the app.
   - To create a contract flow use following options: 
      1. Choose the correct Amazon Connect Instance from the dropdown.
      2. Name: any-unique-name
      3. Type: Customer-whisper
      4. Description: any-valid-description
      5. AWS Flow Language JSON:

  ```
  {
   Version: "2019-10-30",
   StartAction: "8614b74d-3946-4bb3-9808-0e47df651838",
   Metadata: {
      entryPointPosition: {
         x: 75,
         y: 20
      },
      snapToGrid: false,
      ActionMetadata: {
         "0da12357-da4c-4581-b21e-45b1ceee510d": {
            position: {
               x: 479,
               y: 181
            }
         },
         "8614b74d-3946-4bb3-9808-0e47df651838": {
            position: {
               x: 239,
               y: 100
            },
            useDynamic: false,
            promptName: "Beep.wav"
         }
      }
   },
   Actions: [
      {
         Identifier: "0da12357-da4c-4581-b21e-45b1ceee510d",
         Parameters: {},
         Transitions: {},
         Type: "EndFlowExecution"
      },
      {
         Identifier: "8614b74d-3946-4bb3-9808-0e47df651838",
         Parameters: {
            PromptId: "arn:aws:connect:us-west-2:162174280605:instance/cc8f8dc4-fb1a-46ee-a7b0-b418828a9714/prompt/9c638a6c-49bb-4b3f-a3e4-721efc4c8882"
         },
         Transitions: {
            NextAction: "0da12357-da4c-4581-b21e-45b1ceee510d",
            Errors: [],
            Conditions: []
         },
         Type: "MessageParticipant"
      }
   ]}

