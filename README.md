# Email Parsing Flow

## Introduction
This Power Automate flow automates the process of handling leave request emails. The flow extracts information from incoming leave request emails, updates an Excel file with the extracted data, and uses this Excel file to update a Power Bi report.

## Usage
### Triggering the Flow
The flow is triggered automatically when a reply to a new leave request email is sent and contains one of the following words: YES, OK, ACCEPT, or APPROVE. Note that only one of these exact words can be used in the reply email; variations such as "APPROVED" are not accepted. Additionally, the reply must contain only one of these words and no other text.

### Leave Request Email Format
For the flow to correctly extract information, the leave request emails must follow a specific format. Below are the details of the required format:
