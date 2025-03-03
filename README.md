API Documentation
This document explains how to interact with the API endpoints for authentication, retrieving a secure module (encrypted image), and fetching variables. All requests are sent to the host 45.13.227.206 on port 3845.

Note: SSL verification is disabled in the provided examples (i.e., CURLOPT_SSL_VERIFYPEER is set to 0). It is recommended to enable SSL verification in production environments.

Table of Contents
Authentication Endpoint
Secure Module (Image) Endpoint
Variable Retrieval Endpoint
Usage Workflow
Additional Notes
1. Authentication Endpoint
URL:
http://45.13.227.206:3845/backend/client/api/v1/authenticate
Method:
POST

Parameters (Form Data):
license: Your license key (string).
token: Your hardware ID (HWID). This value is typically retrieved from the system (e.g., using a user SID).
Description:
Submit your license key and HWID to authenticate. A successful response returns license details, a session token, and application information.

Example Request using cURL:
curl -X POST "http://45.13.227.206:3845/backend/client/api/v1/authenticate" \
     -d "license=YOUR_LICENSE_KEY&token=YOUR_HWID"
Example Successful Response:

json
{
  "status": "success",
  "license": {
    "id": "license_id",
    "hwid": "your_hwid",
    "expiry": "expiry_date",
    "created_on": "creation_date",
    "duration": 12345
  },
  "token": "session_token",
  "app": {
    "id": "app_id",
    "name": "app_name",
    "version": "app_version",
    "status": "app_status",
    "created_on": "app_creation_date"
  }
}
2. Secure Module (Image) Endpoint
URL:
http://45.13.227.206:3845/backend/client/api/v1/module?token=<session_token>
Method:
GET

Parameters:
token: The session token obtained from the authentication response.
Description:
This endpoint returns an encrypted module (referred to as an image). The response includes an array of unsigned 32-bit integers that represent the encrypted data.

Decryption Process
Derive the Decryption Key:
The key is calculated by summing the ASCII values of each character in your license key.

Decrypt the Image:
Each element in the image array is XORed with the derived key.

Example Request using cURL:
curl "http://45.13.227.206:3845/backend/client/api/v1/module?token=SESSION_TOKEN"

3. Variable Retrieval Endpoint
URL:
http://45.13.227.206:3845/backend/client/api/v1/variables/<variable_id>?license=YOUR_LICENSE_KEY
Method:
GET

Parameters:

variable_id: The identifier for the variable you wish to retrieve.
license: Your license key (string).
Description:
Retrieve details about a specific variable. On success, the response includes the variable’s name and content.

Example Request using cURL:
curl "http://45.13.227.206:3845/backend/client/api/v1/variables/VARIABLE_ID?license=YOUR_LICENSE_KEY"
Example Successful Response:

json
{
  "status": "success",
  "variable": {
    "name": "variable_name",
    "content": "variable_content"
  }
}
Usage Workflow
Authenticate:

Call the /authenticate endpoint with your license and HWID to receive your session token, license details, and application info.
Retrieve the Secure Module:

Use the session token from authentication to request the secure module using the /module endpoint.
Derive the decryption key from your license (by summing its ASCII values) and decrypt the returned image by XORing each value with the key.
Retrieve Variables:

Use the /variables/<variable_id> endpoint with your license key and the variable ID to fetch variable details.
Additional Notes
SSL Verification:
The provided examples disable SSL verification. For production, make sure to enable SSL verification to ensure secure communication.

Error Handling:
If the authentication response contains an error message with "Restart", the request is automatically retried. Other errors result in displaying an error message and terminating the application.

Response Format:
All responses are in JSON format. Use a JSON parser to handle the response data in your application.
