# Email Parsing Flow

## Introduction
This Power Automate flow automates the process of handling leave request emails. The flow extracts information from incoming leave request emails, updates an Excel file with the extracted data, and uses this Excel file to update a Power Bi report.

## Usage
### Triggering the Flow
The flow is triggered automatically when a reply to a new leave request email is sent and contains one of the following words: ``YES, OK, ACCEPT, or APPROVE``. Note that only one of these exact words can be used in the reply email; variations such as ``APPROVED`` are not accepted. Additionally, the reply must contain only one of these words and no other text. Reply must also be in the ``Sent items`` folder and not somehow sent to another folder the leave request email must also be in the ``Inbox`` email folder

### Leave Request Email Format
For the flow to correctly extract information, the leave request emails must follow a specific format. Below are the details of the required format:

#### Subject Line
The subject line must be in the following format:
```
Action Required: Leave [req type] for [Name]
```
Where ``[req type]`` can be one of the following:

```
Creation
Alteration
Cancellation
``` 

and ``[Name]`` must be one of the names from the ``Name for Leave Calendar`` file.

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

add section saying name has to be from the name for calendar list


give me high level overview
then go through each main 3 child flows
