# Email Parsing Flow

## Introduction
This Power Automate flow automates the process of handling leave request emails. The flow extracts information from incoming leave request emails, updates an Excel file with the extracted data, and uses this Excel file to update a Power Bi report.

## Usage
### Triggering the Flow
The flow is triggered automatically when a reply to a new leave request email is sent and contains one of the following words (case sensitive): ``YES, OK, ACCEPT, or APPROVE``. Note that only one of these exact words can be used in the reply email; variations such as ``APPROVED`` are not accepted and will cause errors or unexpected behaviour. Additionally, the reply must contain only one of these words and no other text. The reply must also be in the ``Sent Items`` folder and not redirected to another folder. The leave request email must remain in the ``Inbox`` folder.

### Leave Request Email Format
For the flow to correctly extract information, the leave request emails must follow a specific format. Below are the details of the required format:

#### Subject Line
The subject line must be in the following format:
```
Action Required: Leave [req type] for [Name]
```
Where ``[req type]`` must be one of the following (case sensitive):

```
Creation
Alteration
Cancellation
``` 

and ``[Name]`` must be one of the full names from the ``Full Name`` column in the ``Name for Leave Calendar`` file (case sentitive).

<div style="page-break-after: always;"></div>

#### Email Body
The email body must be in the following format:
```
A Leave request has been assigned to you for your approval.

Employee Code: [Employee Code]
Employee Name: [Employee Name]
Leave Type: [Leave Type]
Leave Application No: [Leave Application No]
Leave From: [Leave From Date]
Leave To: [Leave To Date]
Leave From Session: [Leave From Session]
Leave To Session: [Leave To Session]
Leave Units: [Leave Units]
Leave Reason: [Leave Reason]

Manager and employee are to ensure that the leave request and approval is in line with the prevailing company policy

Thanks and Regards

Action through Email:
For Approval : YES / OK / ACCEPT / APPROVE
For Rejection : NO / CANCEL / REJECT
(Reply with the above key words in the first line of the mail)

For Container Page : ESS-Time-Off-My Team
```

* ``[Employee Code]``: This should be a valid employee code.
* ``[Employee Name]``: Must be one of the full names from the ``Full Name`` column in the ``Name for Leave Calendar`` file (case sentitive).
* ``[Leave Type]``: Must be one of the leave types from the ``Leave Type`` column in the `Leave Type for Leave Calendar` file (case sensitive).
* ``[Leave From Date]``: Must be equal to or before `[Leave To Date]`. This should be in the format dd MMMM yyyy (e.g., 20 March 2025).
* ``[Leave To Date]``: Must be equal to or after `[Leave From Date]`. This should be in the format dd MMMM yyyy (e.g., 20 March 2025).
* ``[Leave From Session]``: Must be equal to ``[Leave To Session]``. Can only be ``"I Session", "II Session", "Whole Day"``.
* ``[Leave To Session]``: Must be equal to ``[Leave From Session]``. Can only be ``"I Session", "II Session", "Whole Day"``.
* `[Leave Units]`: The number of leave units being taken (e.g., 0.50).
* ``[Leave Reason]``: Optional field - reason of leave.

#### Special Requirements for Leave Alteration and Cancellation Email Requests
For leave alteration and cancellation requests to work, there must already be an existing leave created. Additionally, the leave alteration and cancellation email must include the same leave application number and refer to the same employee code as the original request.

<div style="page-break-after: always;"></div>

## Workflow

#### Introduction
This workflow features a parent email parsing flow that processes incoming emails and routes them to specific child flows: Child Flow - Leave Creation, Child Flow - Leave Alteration, and Child Flow - Leave Cancellation, depending on the content of the email. The routing is facilitated by a switch operator, which directs the flow to one of the three distinct flows, each designed to handle different types of requests. Within each of these child flows, there are additional sub-flows that perform essential tasks, such as locating and extracting the leave request email body along with the conversation ID, parsing the extracted email body for relevant details and converting the full name into a display name that showcases both the short name and leave type of the requestor. 

The Workflow section of this report has been divided into the following subsections, each labeled for easy reference:

[Parent Email Parsing Flow](#parent-email-parsing-flow)\
[Child Flow - Leave Creation](#child-flow---leave-creation)\
[Child Flow - Leave Alteration](#child-flow---leave-alteration)\
[Child Flow - Leave Cancellation](#child-flow---leave-cancellation)

#### Parent Email Parsing Flow
The flowchart below illustrates the parent email parsing flow.

![](https://github.com/haowern98/readme/blob/main/Parent%20Email%20Parsing%20Flow-Flowchart.drawio.svg)

#### Child Flow - Leave Creation

![](https://github.com/haowern98/readme/blob/main/leave_creation_child_flowchart.drawio.svg)

<ins>Overview</ins>

This flow is resposnsible for the processing of leave creation requests received via email and creating a new leave entry in the Leave Excel file 

<ins>Implementation</ins>

This flow takes in the conversation ID, `ConvoID` that was extracted in the `Parent Email Parsing Flow` and passes it to the `Child Flow - Get Email with ConvoID` child flow to locate the specific email. Then, passes the output of `Child Flow - Get Email with ConvoID ` into the `Email Parsing Method ` child flow to parse the email body content using the to retrieve necessary details. Next, convertion of the leave requestor's full name into a display name that includes both the short name and leave type using `Child Flow - Name Conversion`. Finally, the flow creates a new entry in an Excel file and sends a response back to the originating Power App or flow, confirming successful completion.

#### Child Flow - Leave Alteration

![](https://github.com/haowern98/readme/blob/main/leave_alteration_childflow.drawio.svg)

#### Child Flow - Leave Cancellation

![](https://github.com/haowern98/readme/blob/main/leave_cancellation_flowchart.drawio.svg)


