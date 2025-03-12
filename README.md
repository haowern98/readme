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

#### Overview
This workflow consists of a parent email parsing flow that processes incoming emails and routes them to specific child flows based on the content of the email. The routing is managed using a switch operator, which directs the flow to one of three distinct flows, each handling different types of requests.

The Workflow section has been divided into the following subsections, each labeled for easy reference:

[Parent Email Parsing Flow](#parent-email-parsing-flow)

#### Parent Email Parsing Flow
The flowchart below illustrates the parent email parsing flow.

![](https://github.com/haowern98/readme/blob/main/Parent%20Email%20Parsing%20Flow-Flowchart.drawio.svg)




add section saying name has to be from the name for calendar list


give me high level overview
then go through each main 3 child flows

