[![](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.2/master/assets/banner.jpg)](https://www.shuftipro.com/)

# On-site Verification without OCR

This *Onsite verification without OCR* requires direct interaction between the provider and the end-user. We collect the image or video proofs from end-users. Merchant collects the values for selected parameters from the end-user. In the verification request, Merchant specifies the keys and values for the parameters to be verified. Shufti Pro uses a unique *template matching technique* to match these values to the data on identity documents. Next, Shufti Pro’s intelligently driven system verifies the collected documents for authenticity.

**Shufti Pro’s AI & HI hybrid technology ensures 99.6% accurate results and quickest response time.**

# Authorization

The Shufti Pro Verification API authenticates clients with a **Basic Auth** header. Provide your **Client ID as Username** and **Secret Key as Password**. This header is required in every request that will be made to the API.

Fields               | Required | Description
---------------------|----------|-------------
username             | Yes      | Enter Client ID as username.
password             | Yes      | Enter your Secret Key as password.

# Verification Request Example

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/7685361fe51b9053c8f1)

```json
POST /HTTP/1.1  
Host: https://shuftipro.com/api/
  Content-Type: application/json
  Authorization: Basic NmI4NmIyNzNmZjM0ZmNlMTlkNmI4WJRTUxINTJHUw== 

{       
	"reference": "17374217" ,
	"country": "GB",  
	"language": "EN", 
	"email": "johndoe@example.com",  
	"callback_url": "http://www.example.com",  
	"redirect_url": "http://www.example.com", 

	"verification_mode": "any",

	"face": "",

	"document": { 
		"supported_types": [
			"passport", 
			"id_card", 
			"driving_license", 
			"credit_or_debit_card"
		] ,
		"name": { 
			"first_name": "John", 
			"last_name": "Carter", 
			"middle_name": "Doe" ,
		}, 
		"dob": "1992-10-10", 
		"document_number": "2323-5629-5465-9990", 
		"expiry_date": "2025-10-10", 
		"issue_date": "2015-10-10"
	},  

	"address":{ 
		"full_address":"3339 Maryland Avenue, Largo, Florida", 
		"name": { 
			"first_name": "John", 
			"last_name": "Carter", 
			"middle_name": "Doe" ,
			"fuzzy_match": "1"
		}, 
		"supported_types":[
			"id_card", 
			"utiltiy_bill", 
			"bank_statement"
		]
	},

	"consent":{ 
		"format":"printed", 
		"text":"This is a customized text", 
	}, 

	"phone": {
		"phone_number": "+4400000000",
		"random_code": "23123",
		"text": "Your verification code is 23123"
	},

	"background_checks": {
		"name": { 
			"first_name": "John", 
			"last_name": "Carter", 
			"middle_name": "Doe" ,
		}, 
		"dob": "1992-10-10", 
	}
}
```


# Verification Request

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/7685361fe51b9053c8f1)

Whenever a request for verification from a user is received, Shufti Pro’s intelligent system determines the nature of verification through parameters given below. These parameters enable Shufti Pro to:

1. Identify its customers

2. Check authenticity of client’s credentials

3. Read client’s data

4. Decide what information is being sent to perform that verification 

# Request Parameters

It is important to note here that each service module is independent of other and each one of them is activated according to the nature of request received from you. There are a total of six services which include face, document, address, consent, phone and background_checks.

All verification services are optional. You can provide Shufti Pro a single service or mixture of several services for verifications. All keys are optional too but values are required with the given keys.  

* ## reference

	Required: **Yes** Type: **string** Minimum: **6 characters** Maximum: **250 characters**

	This is the unique reference ID of request, which we will send you back with each response, so you can verify the request. Only alphanumeric values are allowed. This reference can be used to get status of already performed verification requests.


* ## country

	Required: **Yes** Type: **string** Length: **2 characters**

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

	Verification mode defines what types of proofs are allowed for a verification. In case of 'video_only' user will upload videos and images if verification mode is 'image_only'.

<!-- -------------------------------------------------------------------------------- -->
* ## face

	The easiest of all verifications is done by authenticating the face of the users. In case of on-site verification, end-user will have to show their face in front of a webcam or camera of their phone that essentially makes it a selfie verification.

<!-- -------------------------------------------------------------------------------- -->
* ## document

	Shufti Pro provides document verification through various types of documents. The supported formats are passports, ID Cards, driving licenses and debit/credit cards. You can opt for more than 1 document type as well. In that case, Shufti Pro will give an option to end-users to verify their data from any of the given document types.  

	* <h3>supported_types</h3>

	Required: **Yes**  
	Type: **Array**

	You can provide any one, two or more types of documents to verify the identity of user. For example, if you opt for both passport and driving license, then your user will be given an opportunity to verify data from either of these two documents. All supported types are listed below.

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

	In name object used in document service, first_name is required if you want to perform a name verification from a document. Other fields are optional. All services having name fields include the following parameters.

	**Example 1**  { "first_name" : "John", "last_name" : "Doe" }  
	**Example 2**  { "first_name" : "John", "last_name" : "Doe", "fuzzy_match" : "1"}

	* <h4>first_name</h4>
	Required: **Yes**  
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

	Provide 1 for enabling a fuzzy match of the name. Enabling fuzzy matching attempts to find a match which is not a 100% accurate.

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

	Address of an individual can be verified from the document but they have to enter it before it can be verified from an applicable document image. 

	* <h3>supported_types</h3>

	Required: **Yes**  
	Type: **Array**

	Provide any one, two or more document types in supported_types parameter in Address verification service. For example, if you choose id_card and utility_bill, then the user will be able to verify data using either of these two documents. Following is the list of supported types for address verification.

	Supported Types      |
	---------------------|
	id_card              |
	passport             |
	driving_license      |
	utility_bill         |
	bank_statement       |
	rent_agreement       |
	employer_letter      |
	insurance_agreement  |
	tax_bill             |

	**Example 1** [ "utility_bill" ]  
	**Example 2** [ "id_card", "bank_statement" ]

	* <h3>full_address</h3>

	Required: **Yes**  
	Type: **string**  
	Minimum: **2 characters**  
	Maximum: **250 chracters**

	Allowed Characters are numbers, alphabets, dots, dashes, spaces, underscores, hashes and commas.

	* <h3>name</h3>

	Required: **No**  
	Format **object**

	In name object used in address service, first_name is required if name verification is required. Other fields are optional. All services having name fields include the following parameters.

	**Example 1**  { "first_name" : "John", "last_name" : "Doe" }  
	**Example 2**  { "first_name" : "John", "last_name" : "Doe", "fuzzy_match" : "1"}

	* <h4>first_name</h4>

	Required: **Yes**  
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
	Values Accepted: **1**

	Provide 1 for enabling a fuzzy match of the name. Enabling fuzzy matching attempts to find a match which is not a 100% accurate.

<!-- -------------------------------------------------------------------------------- -->
* ## consent
	
	Customised documents/notes can also be verified by Shufti Pro. Company documents, employee cards or any other personalised note can be authenticated by this module. You can choose handwritten or printed document format but only one form of document can be verified in this verification module. Text whose presence on the note/customized document is to be verified, is also needed to be provided.

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

	Required: **Yes**  
	Type: **string**  
	Minimum: **2 characters**  
	Maximum: **100 chracters**

	Provide text in the string format which will be verified from the document uploaded by the end-user.

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

	It is a verification process that will require you to send us the full Name of end user in addition to date of birth. Shufti Pro will perform AML based background checks based on this information. Name and dob keys are requied if these keys are not provided in a dcoument verification. 

	* <h3>name</h3>

	Required: **No**  
	Format: **object**

	In name object used in background checks service, first_name is required and other fields are optional.

	**Example 1**  { "first_name" : "John", "last_name" : "Doe" }  
	**Example 2**  { "first_name" : "John", "middle_name" : "Carter", "last_name" : "Doe"}

	* <h4>first_name</h4>

	Required: **Yes**  
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

	Required: **Yes**  
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

The Shufti Pro Verification API will send you two types of responses if a request for verification is made. First is the HTTP response sent against your request, and the second is the callback response. Both HTTP and callback responses will be in the JSON format with header `application/json`. The response header also includes a key sp_signature. This key is used for validating the source of response. Be sure to validate the request by [generating signature](#response-signature) and matching it with sp_signature value from the response header.  
Responses will contain the following parameters:

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
Content-Type: application/json
  sp_signature: NmI4NmIyNzNmZjM0ZmNl

{
    "reference":"17374217",
    "event":"request.pending",
    "error":"",
    "verification_url":"https://shuftipro.com/api/verify/474f51710fb60fdf9688f44ea0345eda28a9f55212a83266fb5d237babff2"
}
```

## Status Response

The Shufti Pro Verification API will send a JSON response if a status request is made. Make sure to validate the request by [generating signature](#response-signature) and matching it with **sp_signature** value from response header.

* <h3>reference</h3>
	Your unique request reference, which you provided us at the time of request, so that you can identify the response in relation to the request made.

* <h3>event</h3>
	This is the request event which shows status of request. Event is changed in every response. Please consult [Events](status_codes.md#events) for more information.

<aside class="notice">
Note: <b>request.invalid</b> response with <b>HTTP status code 400</b> means the request is invalid.
</aside>

>Sample Response  

```json
Content-Type: application/json
  sp_signature: NmI4NmIyNzNmZjM0ZmNl

{
    "reference": "17374217",
    "event": "request.invalid"
}
```

## Response Signature
Every HTTP and Callback responses will be in application/json with a key **sp_signature** in the header. It can be used to validate the source of the request. Make a signature using the following procedure:

1. Concatinate Secret Key at the end of the response string. (i.e. response + secret_key).
2. Take **SHA256** of concatinated string.
3. Match the SHA256 string with **sp_signature** value from the header of the response.

In short, make signature as `hash('sha256', response . your_secret_key)` and match it with the signature provided in the header in **sp_signature** key.


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
09 Oct 2018     | 1. Last name field is optional in all name objects. <br> 2. Added signature in response headers to validate the source of responses.