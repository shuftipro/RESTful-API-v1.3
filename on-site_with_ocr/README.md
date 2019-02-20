[![](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.2/master/assets/banner.jpg)](https://www.shuftipro.com/)

# On-site Verification with OCR

This *Onsite verification with OCR* requires direct interaction between the provider and the end-user. We collect the image or video proofs from end-users. In the verification request, Merchant specifies the keys for the parameters to be verified. Shufti Pro extracts the values against each of those keys from the proofs presented by the end-user. These values can also be returned to fill the verification form automatically. This reduces the manual work for the end-user. Next, Shufti Pro’s intelligently driven system verifies the provided documents for authenticity.

**Shufti Pro’s AI & HI hybrid technology ensures 99.6% accurate results and quickest response time.**

# Authorization

The Shufti Pro Verification API authenticates clients with a **Basic Auth** header. Provide your **Client ID as Username** and **Secret Key as Password**. This header is required in every request that will be made to the API.

Fields               | Required | Description
---------------------|----------|-------------
username             | Yes      | Enter Client ID as username.
password             | Yes      | Enter your Secret Key as password.



# Verification Request Example

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/ce807dedd349e6c064ef)

```json
POST /api/ HTTP/1.1
Host: shuftipro.com
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
		"name": "",
		"dob": "", 
		"document_number": "", 
		"expiry_date": "", 
		"issue_date": ""
	},  

	"address":{ 
		"full_address":"", 
		"name": "",
		"supported_types":[
			"id_card", 
			"utility_bill", 
			"bank_statement"
		]
	},

	"consent":{ 
		"supported_types":[
			"printed",
			"handwritten"
		], 
		"text":"This is a customized text", 
	}, 

	"phone": {
		"phone_number": "+4400000000",
		"random_code": "23123",
		"text": "Your verification code is 23123"
	},

	"background_checks": {
		"name": "",
		"dob": "", 
	}
}
```

# Verification Request

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/ce807dedd349e6c064ef)

Whenever a request for verification from a user is received, Shufti Pro’s intelligent system determines the nature of verification through parameters given below. These parameters enable Shufti Pro to:

1. Identify its customers
2. Check authenticity of client’s credentials
3. Read client’s data
4. Decide what information is being sent to perform that verification 

# Request Parameters

It is important to note here that each service module is independent of other and each one of them is activated according to the nature of request received from you. There are a total of six services which include face, document, address, consent, phone and background_checks.

All verification services are optional. You can provide Shufti Pro a single service or mixture of several services for verifications. All keys are optional too. If a key is given in document or address sevice and no value is provided then OCR will be performed for those keys. 

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

	Verification mode defines what types of proofs are allowed for a verification. In case of 'video_only' user will upload videos and images if verification mode is 'image_only'.

* ## allow_offline

	Required: **No**  
	Type: **string**  
	Accepted Values: **0, 1**  
	Default Values: **1**  

	This parameter allows users to upload images or videos in case of nonavailability of a functional webcam.If value: 0, users can capture photos/videos with the camera only.	

* ## show_consent

	Required: **No**  
	Type: **string**  
	Accepted Values: **0, 1**  
	Default Values: **1**

	This parameter displays a screen to collect consent from end-user before the verification process starts. If the value is set 1, the screen will be displayed to end-user. If the value is set 0, the consent screen will not be displayed. Under the GDPR, we are bound to get user’s consent therefore the default value is 1 but you can set it to 0 if you’ve already acquired the user’s consent for this biometric verification.

* ## show_privacy_policy

	Required: **No**  
	Type: **string**  
	Accepted Values: **0, 1**  
	Default Values: **1**

	This parameter displays data privacy policy to end-user after the verification process is completed. If the value is set 1, the data privacy policy will be displayed to end-user. If the value is set 0, the data privacy policy will not be displayed. Under the GDPR, we acknowledge the end users right to request for data deletion therefore the default value is 1 but you can set it to 0 if you’ve have another alternative mechanism in place.

<!-- -------------------------------------------------------------------------------- -->
* ## show_results

	Required: **No**
	Type: **string**
	Accepted Values: **0, 1**
	Default Values: **1**

	If Value for this parameter is 1, verification result will be displayed to the end user, showing them whether their verification is accepted or declined. If the value of this parameter is set 0, verification results will not be shown to end-user.	

<!-- -------------------------------------------------------------------------------- -->
* ## face

	The easiest of all verifications is done by authenticating the face of the users. In case of on-site verification, end-user will have to show their face in front of a webcam or camera of their phone that essentially makes it a selfie verification.

	* <h3>allow_offline</h3>

	Required: **No**  
	Type: **string**  
	Accepted Values: **0, 1**  
	Default Values: **1**  

	This parameter allows user to upload their selfie in case of non-availability of a functional webcam. If value is 0, users can only perform Face Verification with the camera only.  

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

	In name object used in document service, first_name and last_name are extracted from the document uploaded if name is empty. 

	* <h4>first_name</h4>
	Required: **No**  
	Type: **string**  
	Minimum: **1 character**  
	Maximum: **32 chracters** 

	Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark. 
	Example **John'O Harra**

	* <h4>middle_name</h4>

	Required: **No**  
	Type: **string**  
	Minimum: **1 character**  
	Maximum: **32 chracters**

	Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark.  
	Example **Carter-Joe**

	* <h4>last_name</h4>

	Required: **No**  
	Type: **string**  
	Minimum: **1 character**  
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

	Leave empty to perform data extraction from uploaded proofs. Provide a valid date. Please note that the date should be before today. 
	Example 1990-12-31

	* <h3>document_number</h3>

	Required: **No**  
	Type: **string**  
	Minimum: **2 characters**  
	Maximum: **100 chracters**

	Leave empty to perform data extraction from the proof which will be uploaded by end-users. Allowed Characters are numbers, alphabets, dots, dashes, spaces, underscores and commas. 
	Examples 35201-0000000-0, ABC1234XYZ098

	* <h3>issue_date</h3>

	Required: **No**  
	Type: **string**  
	Format: **yyyy-mm-dd**

	Leave empty to perform data extraction from the proof which will be uploaded by end-users. Provide a valid date. Please note that the date should be before today. 
	Example 2015-12-31

	* <h3>expiry_date</h3>

	Required: **No**  
	Type: **string**  
	Format: **yyyy-mm-dd**

	Leave empty to perform data extraction from the proof which will be uploaded by end-users. Provide a valid date. Please note that the date should be after today. 
	Example 2025-12-31

	* <h3>allow_offline</h3>

	Required: **No**  
	Type: **string**  
	Accepted Values: **0, 1**  
	Default Values: **1**  

	This parameter allows user to upload their document in case of non-availability of a functional webcam. If value is 0, users can only perform Document Verification with the camera only.

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

	Required: **No**  
	Type: **string**  
	Minimum: **2 characters**  
	Maximum: **250 chracters**

	Leave empty to perform data extraction from the uploaded proof. Allowed Characters are numbers, alphabets, dots, dashes, spaces, underscores, hashes and commas.

	* <h3>name</h3>

	Required: **No**  
	Format **object**

	In name object used in address service, first_name is required if you don't want to perform OCR of the name parameter. Other fields are optional.

	* <h4>first_name</h4>

	Required: **No**  
	Type: **string**  
	Minimum: **11 character**  
	Maximum: **32 chracters**

	Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark. 
	Example **John'O Harra**

	* <h4>middle_name</h4>

	Required: **No**  
	Type: **string**  
	Minimum: **1 character**  
	Maximum: **32 chracters**

	Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark.  
	Example **Carter-Joe**

	* <h4>last_name</h4>

	Required: **No**  
	Type: **string**  
	Minimum: **1 character**  
	Maximum: **32 chracters**

	Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark. 
	Example **John, Huricane Jr.**

	* <h4>fuzzy_match</h4>

	Required: **No**  
	Type: **string**  
	Value Accepted: **1**

	Provide 1 for enabling a fuzzy match of the name. Enabling fuzzy matching attempts to find a match which is not a 100% accurate.

	* <h3>address_fuzzy_match</h3>

	Required: **No**  
	Type: **string**  
	Accepted Values: **0, 1**  
	Default Values: **1**

	Provide 1 for enabling a fuzzy match for address verification. Enabling fuzzy matching attempts to find a match which is not 100% accurate. Default value will be 0, which means that only 100% accurate address will be verified.

	* <h3>allow_offline</h3>

	Required: **No**  
	Type: **string**  
	Accepted Values: **0, 1**  
	Default Values: **1**  

	This parameter allows user to upload their Address Document in case of non-availability of a functional webcam. If value is 0, users can only perform Address Verification with the camera only.  

<!-- -------------------------------------------------------------------------------- -->
* ## consent
	
	Customised documents/notes can also be verified by Shufti Pro. Company documents, employee cards or any other personalised note can be authenticated by this module. You can choose handwritten or printed document format but only one form of document can be verified in this verification module. Text whose presence on the note/customized document is to be verified, is also needed to be provided.

	* <h3>supported_types</h3>

	Required: **Yes**  
	Type: **array**

	Text provided in the consent verification can be verified by handwritten documents or printed documents.

	Supported Types              |
	---------------------|
	handwritten          |
	printed            |

	**Example 1**  ["printed"]  
	**Example 2**  ["printed", "handwritten"]

	* <h3>text</h3>

	Required: **Yes**  
	Type: **string**  
	Minimum: **2 characters**  
	Maximum: **100 chracters**

	Provide text in the string format which will be verified from the document which the end-user will provide us.

	* <h3>allow_offline</h3>

	Required: **No**  
	Type: **string**  
	Accepted Values: **0, 1**  
	Default Values: **1**  

	This parameter allows user to upload their Consent Document (Handwritten Note/printed document) in case of non-availability of a functional webcam. If value is 0, users can only perform Consent Verification with the camera only.  

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
	Maximum: **10 chracters**

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
	Format: **object**

	In name object used in background checks service, first_name is required and other fields are optional.

	* <h4>first_name</h4>

	Required: **No**  
	Type: **string**  
	Minimum: **1 character**  
	Maximum: **32 chracters**

	Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark. 
	Example **John'O Harra**

	* <h4>middle_name</h4>

	Required: **No**  
	Type: **string**  
	Minimum: **1 character**  
	Maximum: **32 chracters**

	Allowed Characters are alphabets, - (dash), comma, space, dot and single quotation mark.  
	Example **Carter-Joe**

	* <h4>last_name</h4>

	Required: **No**  
	Type: **string**  
	Minimum: **1 character**  
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
POST /api/status HTTP/1.1
Host: shuftipro.com
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

# Delete Request sample  

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/28e1ab2e4c2831a9468e)

```json
POST /api/delete HTTP/1.1
Host: shuftipro.com
  Content-Type: application/json
  Authorization: Basic NmI4NmIyNzNmZjM0ZmNlMTlkNmI4WJRTUxINTJHUw== 

{      
	"reference" : "17374217",
	"comment"   : "testing comment"
}

```

## Delete Request

Once a verification request is completed, you may request at delete request endpoint to delete the verification data. You’ll have to provide reference ID for that request and you will be promptly informed about the deletion of the request.  

* ## reference

	Required: **Yes**  
	Type: **string**  
	Minimum: **5 characters**  
	Maximum: **250 characters**

	This is the unique reference ID of request which needs to be deleted.

* ## comment

	Required: **Yes**  
	Type: **string**  
	Minimum: **5 characters**  
	Maximum: **200 characters**

	Add a comment why the request is deleted.

# Responses

## Verification Response

The Shufti Pro Verification API will send you two types of responses if a request for verification is made. First is the HTTP response sent against your request, and the second is the callback response. Both HTTP and callback responses will be in the JSON format with header `application/json`. The response header also includes a key Signature. This key is used for validating the source of response. Be sure to validate the request by [generating signature](#response-signature) and matching it with Signature value from the response header.  
Responses will contain the following parameters:

* <h3>reference</h3>
	Your unique request reference, which you provided us at the time of request, so that you can identify the response in relation to the request made.

* <h3>event</h3>
	This is the request event which shows status of request. Event is changed in every response.  

	Please consult [Events](status_codes.md#events) for more information.

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
	It is only returned in case of a valid verification. This object will include the all the gathered data in a request process.  

	Check *verification.accepted* and *verification.declined* responses in [Events](status_codes.md#events) section for a sample response.

<aside class="notice">
Note: Callback response will be sent on the callback_url provided in the request callback_url parameter.
</aside>

>Sample Response  

```json
Content-Type: application/json
  Signature: NmI4NmIyNzNmZjM0ZmNl

{
    "reference":"17374217",
    "event":"request.pending",
    "error":"",
    "verification_url":"https://shuftipro.com/api/verify/474f51710fb60fdf9688f44ea0345eda28a9f55212a83266fb5d237babff2"
}
```

## Status Response

The Shufti Pro Verification API will send a JSON response if a status request is made. Make sure to validate the request by [generating signature](#response-signature) and matching it with **Signature** value from response header.

* <h3>reference</h3>
	Your unique request reference, which you provided us at the time of request, so that you can identify the response in relation to the request made.

* <h3>event</h3>
	This is the request event which shows status of request. Event is changed in every response.  
	  
	Please consult [Events](status_codes.md#events) for more information.

* <h3>proof</h3>
	This contains all the proofs that were used to verify data. The Proof URLs returned are temporary and valid for **15 minutes only**.

<aside class="notice">
Note: <b>request.invalid</b> response with <b>HTTP status code 400</b> means the request is invalid.
</aside>

>Sample Response  

```json
  Content-Type: application/json
  Signature: NmI4NmIyNzNmZjM0ZmNl

{
    "reference" : "17374217",
    "event"     : "verification.accepted",
    "proof"     : {
    	"face": {
            "proof": "https://shuftipro.com/api/storage/aZa8mncOFLrbtxXk7Ka/face/proof.png?access_token=1a6c9985e88051092b31d62d043"
        },
        "document": {
            "proof": "https://shuftipro.com/api/storage/aZa8mncOFLrbtxXk7Ka/document/proof.png?access_token=1a6c9985e88051092b31d62d043"
        },
        "address": {
            "proof": "https://shuftipro.com/api/storage/aZa8mncOFLrbtxXk7Ka/address/proof.png?access_token=1a6c9985e88051092b31d62d043"
        },
        "consent": {
            "proof": "https://shuftipro.com/api/storage/aZa8mncOFLrbtxXk7Ka/consent/proof.png?access_token=1a6c9985e88051092b31d62d043"
        } 
    }
}
```

## Delete Request Response

The Shufti Pro Verification API will send a JSON response if a delete request is made. Make sure to validate the request by [generating signature](#response-signature) and matching it with **Signature** value from response header.

* <h3>reference</h3>
	Your unique request reference, which you provided us at the time of request, so that you can identify the response in relation to the request made.

* <h3>event</h3>
	This is the request event which shows status of request. Event is changed in every response.  
	  
	Please consult [Events](status_codes.md#events) for more information.

<aside class="notice">
Note: <b>request.invalid</b> will be returned in case of invalid reference provided or the request is already deleted.
</aside>

>Sample Response  

```json
Content-Type: application/json
  Signature: NmI4NmIyNzNmZjM0ZmNl

{
    "reference": "17374217",
    "event": "request.deleted"
}
```

## Response Signature
Every HTTP and Callback responses will be in application/json with a key **Signature** in the header. It can be used to validate the source of the request. Make a signature using the following procedure:

1. Concatinate Secret Key at the end of the response string. (i.e. response + secret_key).
2. Take **SHA256** of concatinated string.
3. Match the SHA256 string with **Signature** value from the header of the response.

In short, make signature as `hash('sha256', response . your_secret_key)` and match it with the signature provided in the header in **Signature** key.


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



# Test IDs
Shufti Pro provides the users with a number of test documents. Customers may use these to test the demo, instead of presenting their actual information. <br><br>


[![](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/real-face.jpg)](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/real-face.jpg) 

[![](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/fake-face.jpg)](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/fake-face.jpg) 

[![](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/real-id-card.jpg)](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/real-id-card.jpg)

[![](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/fake-id-card.jpg)](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/fake-id-card.jpg)

[![](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/real-consent-document.jpg)](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/real-consent-document.jpg)

[![](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/fake-consent-document.jpg)](https://raw.githubusercontent.com/shuftipro/RESTful-API-v1.3/master/assets/fake-consent-document.jpg)

 <br>




# Revision History

Date            | Description 
--------------- | ------------
21 Dec 2018     | Correct the get status request url
20 Dec 2018     | Correct verification.cancelled event name from events listing
29 Nov 2018     | Update POSTMAN collection link, remove format key and add supported_types key for consent service in POSTMAN collection.
26 Nov 2018     | Add allow_offline key in request parameters.
17 Oct 2018     | Update Test IDs for demo/test verifications.
09 Oct 2018     | 1. Last name field is optional in all name objects. <br> 2. Added signature in response headers to validate the source of responses.
29 Oct 2018     | Changed format key to Supported_types in consent Service.
29 Oct 2018     | Allowed PDF documents as proofs in image_only and any verification modes.
24 Jan 2019     | Added a new callback with event `verification.status.changed`. It is sent to clients whenever a verification status is updated.
28 Jan 2019     | Added a new endpoint `/api/delete` to delete a request data.
28 Jan 2019     | Added a new event `request.deleted` which is returned whenever a request is deleted.
28 Jan 2019     | Status response now returns proofs also.
28 Jan 2019     | Added `show_results` key in request which allows end-susers see verification results.
18 Feb 2019     | `Signature` key added into SP Http, Callback headers for signature validation.
19 Feb 2019     | Added `show_consent` and `show_privacy_policy` parameters in verification request.
19 Feb 2019     | Added `address_fuzzy_match` parameter in address service.
19 Feb 2019     | Added `allow_offline` parameter in face, document, address and consent services.
20 Feb 2019     | Added `selected_type` key in address, document, consent services webhooh/callback response.