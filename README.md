[![](https://raw.githubusercontent.com/shuftipro/ShuftiProSDK/master/shufti_pro_sdk.png)](https://www.shuftipro.com/)

# Introduction

Shufti Pro has designed this Verification API document for its customers that have signed up for our next-generation service pack. This document will explain various kinds of verification services included in this service pack, how they are provided and what kind of data is required from our clients to perform these verifications successfully.

**Shufti Pro’s AI & HI hybrid technology ensures 99.6% accurate results and quickest response time.**

Shufti Pro’s API supports two verification types, i.e. on-site and off-site. 

## On-site Verification
On-site verification means that the customer will come on Shufti Pro’s site and perform verification there. They will not perform it through the merchant’s site. Shufti Pro will collect the information directly from customer. 
	
* ### With OCR
Merchant provides us with the keys, not the data. Example: name: “ ”.
This means that the merchant has opted for name verification but has not sent any data.
We have to extract the data, from the user’s provided documents, at our end, and then verify it as well. 
Consult [This Document](on-site_with_ocr/on-site_with_ocr.md) for complete On-site Verification with OCR.
	
* ### Without OCR
Merchant provides us with the keys, along with the data. Example: issue_date: “2016-07-16”. This means that the merchant has opted for issue date verification with the verification data. We have to simply verify that information, no data extraction is required. 
Consult [This Document](on-site_without_ocr/on-site_without_ocr.md) for complete On-site Verification without OCR.

## Off-site Verification
Off-site verification means that the customer will not come on Shufti Pro’s site to get verified. They will do it through the merchant’s platform. Merchant will collect the information and send us the data for verification. Merchant provides us with the proofs (images/videos). We will not collect them directly from the user. 

    
* ### With OCR
In off-site verification with OCR means that the merchant has not provided us proofs (images/videos) and also no data in some keys. In this verification Shufti Pro will perform extraction of data from those proofs and finally verify the data. 
Consult [This Document](off-site_with_ocr/off-site_with_ocr.md) for complete Off-site Verification with OCR. 
	
* ### Without OCR
If Merchant gives us the data in keys as well as all the proofs required then Shufti Pro just have to verify the data. No customer interaction takes place in this kind of verification.
Consult [This Document](off-site_without_ocr/off-site_without_ocr.md) for complete Off-site Verification without OCR.

# Authorization

The Shufti Pro Verification API authenticates clients with a **Basic Auth** header. Provide your **Client ID as Username** and **Secret Key as Password**. This header is required in every request that has been made to the API.

Fields               | Required | Description
---------------------|----------|-------------
username             | Yes      | Enter Client ID as username.
password             | Yes      | Enter your Secret Key as password.

# Verification Request Sample 

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/8338f548d03d02831cab)

```json
POST /HTTP/1.1  
Host: https://shuftipro.com/api/
  Content-Type: application/json
  Authorization: Basic NmI4NmIyNzNmZjM0ZmNlMTlkNmI4WJRTUxINTJHUw== 

{
	"reference": "" ,
	"country": "", 
	"language": "", 
	"email": "", 
	"callback_url": "", 
	"redirect_url": "", 

	"verification_mode": "",

	"face": { 
		"proof": "" 
	}, 

	"document": { 
		"proof": "", 
		"additional_proof": "", 
		"supported_types": [] ,
		"name": { 
			"first_name": "", 
			"last_name": "", 
			"middle_name": "" ,
			"fuzzy_match": ""
		}, 
		"dob": "", 
		"document_number": "", 
		"expiry_date": "", 
		"issue_date": ""
	}, 

	"address":{ 
		"proof":"" ,
		"full_address":"", 
		"name": { 
			"first_name":"", 
			"middle_name":"", 
			"last_name":"", 
			"fuzzy_match":"" 
		}, 
		"supported_types":[]
	},
	
	"consent":{ 
		"proof":"" ,
		"format":"", 
		"text":"", 
	}, 

	"phone": {
		"phone_number": "",
		"random_code": "",
		"text": ""
	},

	"background_checks": {
		"name": {
			"first_name": "",
			"middle_name": "",
			"last_name": ""
		},
		"dob": ""
	}
}
```

# Verification Request

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/8338f548d03d02831cab)

Shufti Pro is performing variety of verifications for its customers. Our diverse services suite allows us to validate the identity of users through facial verification, documents verification and address verification. We can also check the authenticity of customised documents like official IDs and perform background checks for AML compliance. A mix of various service modules can also be acquired to perform multifaceted verifications like facial and document verification can help you perform a thorough KYC procedure.  

Whenever a request for verification from a customer is received, the intelligent system of Shufti Pro ascertains the nature of verification through following parameters. These parameters enable Shufti pro to identify its customers, authenticity of client credentials, read client data, what kind of verification is required  (off-site or on-site) and what material is being sent to perform that verification. Some of these parameters are necessarily required while others are optional. 

# Request Parameters

It is important to note here that each service module is independent of other and each one of them is activated according to the nature of request received from you. There are a total of six services which include face, document, address, consent, phone and background_checks.

All keys are optional. If a key is given in document or address sevice and no value is provided then OCR will be performed for those keys. 

* ## reference

	Required: **Yes**  
	Type: **string**  
	Minimum: **6 characters**  
	Maximum: **250 characters**  

	This is the unique reference ID of request, which we will send you back with each response, so you can verify the request. Only alphanumeric values are allowed. This reference can be used to get status of already performed verification requests.


* ## country

	Required: **Yes**  
	Type: **string**  
	Length: **2 characters**

	Send the 2 characters long [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements) country code of where your customer is from. Please consult [Supported Countries](countries.md) for country codes.

* ## language

	Required: **No**  
	Type: **string**  
	Length: **2 characters**

	Send the 2 characters long language code of your preferred language to display the verification screens accordingly. Please consult [Supported Languages](languages.md) for language codes. Default language english will be selected if this key is missing in the request.

* ## email

	Required: **No**  
	Type: **string**  
	Minimum: **6 characters**  
	Maximum: **128 characters**

	This field represents email of the end-user. If it is missing in a request, than Shuftpro will ask the user for its email in an on-site request.

* ## callback_url

	Required: **Yes**  
	Type: **string**  
	Minimum: **6 characters**  
	Maximum: **250 characters**

	During a verification request, we make several server to server calls to keep you updated about the verification state. This way you can update the request status at your end even if the customer is lost midway through the process.

* ## redirect_url

	Required: **No**  
	Type: **string**  
	Minimum: **6 characters**  
	Maximum: **250 characters**

	Once an on-site verification is complete, User is redirected to this link after showing the results.

* ## verification_mode

	Required: **No**  
	Type: **string**  
	Accepted Values: **any, image_only, video_only**

	Verification mode defines what types of proofs are allowed for a verification. In case of 'video_only' mode, you can only send base64 of videos where format should be MP4 or MOV in proofs. In 'any' mode mixture of images and videos can be provided in proofs. Default mode 'any' will be selected if this key is missing.

<!-- -------------------------------------------------------------------------------- -->
* ## face

	The easiest of all verifications is done by authenticating the face of the users. In case of on-site verification, end-user will have to show their face in front of a webcam or camera of their phone that essentially makes it a selfie verification.

	* <h3>proof</h3>

	Required: **No**  
	Type: **string**  
	Image Format: **JPG/PNG** Maximum: **16MB**  
	Video Format: **MP4/MOV** Maximum: **20MB**

	Provide valid **BASE64** encoded string. Leave empty for an on-site verification.

<!-- -------------------------------------------------------------------------------- -->
* ## document

	Shufti Pro provides document verification through various types of documents. The supported formats are passports, ID Cards, driving licenses and debit/credit cards. You can opt for more than 1 document type as well. In that case, Shufti Pro will give an option to end-users to verify their data from any of the given document types.  

	In case of off-site verification, you can provide more than 1 document image and use “additional proof” parameter for this. This is to ensure that the required credentials are easily visible e.g. a document might have name and image of individual at the front but the date of birth of that person is printed at the back of the document or on another page of the passport. If you opt for both facial and document verification, face of individual from document will be used to validate uploaded selfie.
	
	* <h3>proof</h3>

	Required: **No**  
	Type: **string**  
	Image Format: **JPG/PNG** Maximum: **16MB**  
	Video Format: **MP4/MOV** Maximum: **20MB**

	Provide valid **BASE64** encoded string. Leave empty for an on-site verification.

	* <h3>additional_proof</h3>

	Required: **No**  
	Type: **string**  
	Image Format: **JPG/PNG** Maximum: **16MB**  
	Video Format: **MP4/MOV** Maximum: **20MB**

	Provide valid **BASE64** encoded string. Leave empty for an on-site verification.

	* <h3>supported_types</h3>

	Required: **Yes** 
	Type: **Array**

	Document verification have two parameters: proof and additional_proof. If these two are not set or empty, it means that it should be an on-site verification. You can provide any one, two or more types of documents to verify the identity of user. For example, if you opt for both passport and driving license, then your user will be given an opportunity to verify data from either of these two documents. **Please provide only one document type if you are providing proof of that document with the request**. All supported types are listed below.

	Supported Types      |
	---------------------|
	passport             |
	id_card            |
	driving_license    |
	credit_or_debit_card |

	**Example 1** ["driving_license"]  
	**Example 2** ["id_card", "credit_or_debit_card", "passport"]

	* <h3>name</h3>

	Required: **No**  
	Type: **object**

	In name object used in document service, first_name and last_name is required if you don't want to perform OCR of the name parameter. Other fields are optional.

	* <h4>first_name</h4>

	 Required: **No**  
	 Type: **string**  
	 Minimum: **2 characters**  
	 Maximum: **32 chracters**

	 Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark. 
	 Example **John'O Harra**

	* <h4>middle_name</h4>

	 Required: **No**  
	 Type: **string**  
	 Minimum: **2 characters**  
	 Maximum: **32 chracters**

	 Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark.  
	 Example **Carter-Joe**

	* <h4>last_name</h4>

	 Required: **No**  
	 Type: **string**  
	 Minimum: **2 characters**  
	 Maximum: **32 chracters**

	 Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark. 
	 Example **John, Huricane Jr.**

	* <h4>fuzzy_match</h4>

	 Required: **No**  
	 Type: **string**  
	 Value Accepted: **1**

	 Provide 1 for enabling a fuzzy match of the name.

	* <h3>dob</h3>

	Required: **No**  
	Type: **string**  
	Format: **yyyy-mm-dd**

	Provide a valid date. Please note that the date should be before today. 
	Example 1990-12-31

	* <h3>document_number</h3>

	Required: **No**  
	Type: **string**  
	Minimum: **2 characters**  
	Maximum: **100 chracters**

	Allowed Characters are numbers, alphabets, dots, dashes, spaces, underscores and commas. 
	Examples 35201-0000000-0, ABC1234XYZ098

	* <h3>issue_date</h3>

	Required: **No**  
	Type: **string**  
	Format: **yyyy-mm-dd**

	Provide a valid date. Please note that the date should be before today. 
	Example 2015-12-31

	* <h3>expiry_date</h3>

	Required: **No**  
	Type: **string**  
	Format: **yyyy-mm-dd**

	Provide a valid date. Please note that the date should be after today. 
	Example 2025-12-31

<!-- -------------------------------------------------------------------------------- -->
* ## address

	Address of an individual can be verified from the document but they have to enter it before it can be verified from an applicable document image. Supported document formats include ID cards, utility bills and bank statements.

	* <h3>proof</h3>

	Required: **No**  
	Type: **string**  
	Image Format: **JPG/PNG** Maximum: **16MB**  
	Video Format: **MP4/MOV** Maximum: **20MB**

	* <h3>supported_types</h3>

	Required: **Yes**  
	Type: **Array**

	Provide any one, two or more document types in proof parameter in Address verification service. For example, if you choose id_card and utility_bill, then the user will be able to verify data using either of these two documents. **Please provide only one document type if you are providing proof of that document with the request**. Following is the list of supported types for address verification.

	Supported Types      |
	---------------------|
	id_card             |
	utiltiy_bill           |
	bank_statement   |

	**Example 1** [ "utility_bill" ]  
	**Example 2** [ "id_card", "bank_statement" ]

	* <h3>full_address</h3>

	 Required: **No**  
	 Type: **string**  
	 Minimum: **2 characters**  
	 Maximum: **250 chracters**

	 Allowed Characters are numbers, alphabets, dots, dashes, spaces, underscores, hashes and commas.

	* <h3>name</h3>

	Required: **No**  
	Type: **object**

	In name object used in address service, first_name and last_name is required if you don't want to perform OCR of the name parameter. Other fields are optional.

	* <h4>first_name</h4>

	 Required: **No**  
	 Type: **string**  
	 Minimum: **2 characters**  
	 Maximum: **32 chracters**

	 Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark. 
	 Example **John'O Harra**

	* <h4>middle_name</h4>

	 Required: **No**  
	 Type: **string**  
	 Minimum: **2 characters**  
	 Maximum: **32 chracters**

	 Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark.  
	 Example **Carter-Joe**

	* <h4>last_name</h4>

	 Required: **No**  
	 Type: **string**  
	 Minimum: **2 characters**  
	 Maximum: **32 chracters**

	 Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark. 
	 Example **John, Huricane Jr.**

	* <h4>fuzzy_match</h4>

	 Required: **No**  
	 Type: **string**  
	 Value Accepted: **1**

	 Provide 1 for enabling a fuzzy match of the name.

<!-- -------------------------------------------------------------------------------- -->
* ## consent
	
	Customised documents/notes can also be verified by Shufti Pro. Company documents, employee cards or any other personalised note can be authenticated by this module. You can choose handwritten or printed document format but only one form of document can be verified in this verification module. Text whose presence on the note/customized document is to be verified, is also needed to be provided.

	* <h3>proof</h3>

	Required: **No**  
	Type: **string**  
	Image Format: **JPG/PNG** Maximum: **16MB**  
	Video Format: **MP4/MOV** Maximum: **20MB**

	* <h3>format</h3>

	Required: **Yes**  
	Type: **string**

	Text provided in the consent verification can be verified by handwritten documents or printed documents. If “any” is mentioned in the format parameter, then user can verify provided note using either of these two documents. Mention only one format from the following list.

	Formats              |
	---------------------|
	handwritten          |
	printed            |
	any                |

	**Example 1**  "printed"  
	**Example 2**  "any"

	* <h3>text</h3>

	Required: **No**  
	Type: **string**  
	Minimum: **2 characters**  
	Maximum: **100 chracters**

	Provide text in the string format which will be verified from a given proof.

<!-- -------------------------------------------------------------------------------- -->
* ## phone

	Verify the phone number of end-users by sending a random code to their number from Shufti Pro. Once the sent code is entered into the provided field by end-user, phone number will stand verified. It is primarily an on-site verification and you have to provide phone number of the end-user to us, in addition to the verification code and the message that is to be forwarded to the end-user. Shufti Pro will be responsible only to send the message along with verification code to the end user and verify the code entered by the end-user.

	* <h3>phone_number</h3>

	Required: **No**  
	Type: **string**  
	Minimum: **2 characters**  
	Maximum: **64 chracters**

	Allowed Characters: numbers and plus sign at the beginning. Provide a valid customer’s phone number with country code. Shufti Pro will directly ask the end-user for phone number if this field is missing or empty.

	* <h3>random_code</h3>

	Required: **No**  
	Type: **string**  
	Minimum: **2 characters**  
	Maximum: **64 chracters**

	Provide a random code. If this field is missing or empty. Shufti Pro will generate a random code.

	* <h3>text</h3>

	Required: **No**  
	Type: **string**  
	Minimum: **2 characters**  
	Maximum: **100 chracters**

	Provide a short description and random code in this field. This message will be sent to customers. ***This field should contain random_code***. If random_code field is empty than Shufti Pro will generate a random code and append the code with this message at the end.

<!-- -------------------------------------------------------------------------------- -->
* ## background_checks

	It is a verification process that will require you to send us the full Name of end user in addition to date of birth. Shufti Pro will perform AML based background checks based on this information. Please note that the name and dob keys will be extracted from document service if these keys are empty.

	* <h3>name</h3>

	Required: **No**  
	Type: **object**

	In name object used in background checks service, first_name and last_name is required and other fields are optional.

	* <h4>first_name</h4>

	 Required: **No**  
	 Type: **string**  
	 Minimum: **2 characters**  
	 Maximum: **32 chracters**

	 Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark. 
	 Example **John'O Harra**

	* <h4>middle_name</h4>

	 Required: **No**  
	 Type: **string**  
	 Minimum: **2 characters**  
	 Maximum: **32 chracters**

	 Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark.  
	 Example **Carter-Joe**

	* <h4>last_name</h4>

	 Required: **No**  
	 Type: **string**  
	 Minimum: **2 characters**  
	 Maximum: **32 chracters**

	 Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark. 
	 Example **John, Huricane Jr.**

	* <h3>dob</h3>

	Required: **No**  
	Type: **string**  
	Format: **yyyy-mm-dd**

	Provide a valid date. Please note that the date should be before today. 
	Example 1990-12-31


# Status Request sample  

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/6f3b6d206ad0a3551a51)

```json
POST /HTTP/1.1  
Host: https://shuftipro.com/api/status/
  Content-Type: application/json
  Authorization: Basic NmI4NmIyNzNmZjM0ZmNlMTlkNmI4WJRTUxINTJHUw== 

{      
	"reference" : "17374217"
}

```

## Status Request

Once a verification request is completed, you may request at status end point to get the verification status. You’ll have to provide reference ID for status request and you will be promptly informed about the status of that verification. 

* ## reference

	Required: **Yes**  
	Type: **string**  
	Minimum: **6 characters**  
	Maximum: **250 characters**

	This is the unique reference ID of request, which we will send you back with each response, so you can verify the request. Only alphanumeric values are allowed.

# Responses

## Verification Response

The Shufti Pro Verification API will send you two types of responses if a request for verification is made. First is the HTTP response sent against your request, and the second is the callback response, respectively. Both HTTP and callback responses will be in the JSON format with header `application/json` and they will contain the following parameters:

* <h3>reference</h3>
	Your unique request reference, which you provided us at the time of request, so that you can identify the response in relation to the request made.

* <h3>event</h3>
	This is the request event which shows status of request. Event is changed in every response. Please consult [Events](status_codes.md#events) for more information.

* <h3>error</h3>
	Whenever there is an error in your request, this parameter will have the details of that error.

* <h3>token</h3>
	This is the unique request token of the request.

* <h3>verification_url</h3>
	A URL is generated for your customer to verify there documents. It is only generated in case of on-site request.  

* <h3>verification_result</h3>
	It is only returned in case of a valid verification. This includes results of each verification.  

	1 means **accepted**  
	0 means **declined**  
	null means **not processed**  

	Check *verification.accepted* and *verification.declined* responses in [Events](status_codes.md#events) section for a sample response.

* <h3>verification_data</h3>
	It is only returned in case of a valid verification. This object will include the all the gathered data in a request process. <br/> Check *verification.accepted* and *verification.declined* responses in [Events](status_codes.md#events) section for a sample response.

<aside class="notice">
Note: Callback response will be sent on the callback_url provided in the request callback_url parameter.
</aside>

>Sample Response  

```json
{
    "reference":"17374217",
    "event":"request.pending",
    "error":"",
    "verification_url":"https://shuftipro.com/api/verify/474f51710fb60fdf9688f44ea0345eda28a9f55212a83266fb5d237babff2"
}
```

## Status Response

The Shufti Pro Verification API will send a JSON response if a status request is made.

* <h3>reference</h3>
	Your unique request reference, which you provided us at the time of request, so that you can identify the response in relation to the request made.

* <h3>event</h3>
	This is the request event which shows status of request. Event is changed in every response. Please consult [Events](status_codes.md#events) for more information.

<aside class="notice">
Note: <b>request.invalid</b> response with <b>HTTP status code 400</b> means the request is invalid.
</aside>

>Sample Response  

```json
{
    "reference": "17374217",
    "event": "request.invalid"
}
```

# HTTP Status Codes and Events

Instant Capture & Verification API uses conventional HTTP response codes to indicate the success or failure of an API request. Every response is generated in JSON with a specific HTTP code. Go to [Status Codes](status_codes.md) for a complete list of status codes. Events are sent in responses which show the status of request. These events are sent in both HTTP and callback responses. Please consult [Events](status_codes.md#events) for a complete list of events.


# Supported Browsers and Devices

In case of on-site verification, a verification page is shown to users. This page is supported on the following list of browsers.


Browsers                  |  Minimum Version/SDK  
---------                 | --------------------  
Chrome (Recommended)      | 65
Firefox (Recommended)     | 58
Safari                    | 8 
Opera                     | 52
Internet Explorer         | 11 
Edge                      | 16

Here a list of supported operating systems on mobile devices.

Mobile OS                 |  Minimum Version/SDK  
---------                 | --------------------  
Android                   | 6.0 (Marshmallow)
iOS                       | 10

# Revision History

Date            | Description 
--------------- | ------------
