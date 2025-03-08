# Email Parsing Flow

## Introduction
This Power Automate flow automates the process of handling leave request emails. The flow extracts information from incoming leave request emails, updates an Excel file with the extracted data, and uses this Excel file to update a Power Bi report.

## Usage
The flow is triggered automatically when a reply to a new leave request email is sent and contains one of the following words: YES, OK, ACCEPT, or APPROVE. Note that only one of these exact words can be used in the reply email; variations such as "APPROVED" are not accepted.

## Usage
