# Creating New License Keys API Documentation

## Overview
This document provides detailed instructions on how to create new license keys for applications using our RESTful API. This API allows authorized users to generate license keys with specified validity durations.

## Prerequisites
Before you proceed, ensure you have:
- A valid API access token.
- The application ID for which you want to generate licenses.

## API Endpoint

### Request Details
**Endpoint:** `/backend/dashboard/api/v1/apps/{appId}/licenses`
**Method:** POST
**URL Format:** `http://{SERVER_IP}:{PORT}/backend/dashboard/api/v1/apps/{APP_ID}/licenses`
Replace `{SERVER_IP}` with your server's IP address, `{PORT}` with your server's port, and `{APP_ID}` with the application ID.

### Headers
Include the following headers in your request:
- `Content-Type: application/json`
- `Authorization: YOUR_ACCESS_TOKEN` (Replace `YOUR_ACCESS_TOKEN` with your actual token.)

### Body Parameters
Provide the following details:
- `duration`: INTEGER (Validity duration of the licenses in days)
- `quantity`: INTEGER (Number of licenses to generate)

### Example Request
Configure your request in API testing tools like Talend API Tester with the URL constructed as shown above.
**Method:** POST
**Headers:**
- `Content-Type: application/json`
- `Authorization: YOUR_ACCESS_TOKEN`

**Body:**
{
"duration": 30,
"quantity": 1
}

## Handling Responses
The API will return a JSON response indicating the request status:
- **200 OK:** Licenses successfully generated; details included in the response.
- **401 Unauthorized:** Invalid or expired access token.
- **400 Bad Request:** Possible error in request format or missing parameters.
- **500 Internal Server Error:** Server-side error during request processing.
