# ServiceNow Configuration - Storing Email Analysis in ServiceNow Requests
This functionality is used for processing and parsing email headers to be included in a ServiceNow request. When an end user receives a phishing email, they may forward the email as an attachment in a ServiceNow ticket. This functionality will create a security request in ServiceNow, parse the phishing email attachment automatically, post it to the work notes of a security request. If using ServiceNow, this helps an analyst save time analyzing an email header.

# Security
There are no details on how the security analysis is done in this script. Instead, the functionality included here is only for parsing out the headers, as well as running a check with Virus Total, to add more context to a security incident ticket stored in ServiceNow.

# Details of Code Files
The code files in this repository may be used in conjunction with ServiceNow functionality to process tickets. The details parsed out of the email are:

1. Message headers
2. The hops (different servers that the message has passed through)
3. A check with an external third party service called Virus Total 

This repository contains 4 files

<b>Inbound Email Action - Security Request.txt</b>

This is an Inbound Email action on Security Request table. This email action is used to parse the emails from end users and create Security Requests and attach the phishing email as an attachment to the request.


<b>Business Rule - Security Request.txt</b>

This is an onInsert Business Rule on Security Request. Once the request is created, this async business rule runs on the background and automatically analyzes the email by calling a script include function. The result is posted to the work notes of the request.


<b>UI Action - Security Request.txt</b>

This is a UI action on the security request table, which can be used to manually analyze an email attached to the security request.


<b>Script Include - Security Scope Common.txt</b>

This script is invoked by the business rule or UI action, to analyze the email header. It also holds the functionality to call a Virus Total API to check the safelinks in the phishing emails. You need a Virus Total API key inside the function runVirusTotal() to use Virus Total API.

# License
Copyright 2019 eBay Inc. 
Use of this source code is governed by an MIT-style license that can be found in the LICENSE file or at https://opensource.org/licenses/MIT.

# 3rd Party Code/Services

## ServiceNow
The code files provided here are usable as code in conjunction with ServiceNow. ServiceNow is a third party tool, not provided with this code, and will need to be licensed separately. For details, see: https://www.servicenow.com/

## Virus Total
At least one code file provided includes an API call to Virus Total.  Virus Total is a third party service, not provided with this code, and has a separate Terms of Service and license.  For details, see: https://www.virustotal.com/gui/home/upload.  Terms of Service are available here: https://support.virustotal.com/hc/en-us/articles/115002145529-Terms-of-Service.
