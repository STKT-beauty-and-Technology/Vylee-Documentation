# API Documentation

## 1. Vendor Registration

### Description:
This API registers a new vendor in the system.

- **Request URL**: `localhost:9090/vendor/new/registration`
- **Request Method**: `POST`
- **Request Body**: JSON object containing vendor details (name, email, phone number, etc.)
  
- **Response**: 
  - **Type**: `String`
  - **Description**: Returns a confirmation message indicating the success or failure of the vendor registration.

---

## 2. Vendor Update Address

### Description:
This API updates the address of an existing vendor.

- **Request URL**: `localhost:9090/vendor/update/address`
- **Request Method**: `PUT`
- **Request Body**: JSON object containing updated address details.
  
- **Response**: 
  - **Type**: `String`
  - **Description**: Returns a message confirming the successful update of the vendor's address.

---

## 3. Send OTP

### Description:
This API sends an OTP (One-Time Password) to the vendor's registered mobile number.

- **Request URL**: `localhost:9090/vendor/send/otp/{mobileNumber}`
- **Request Method**: `GET`
- **Path Parameter**:
  - `mobileNumber`: The mobile number to which the OTP will be sent.
  
- **Response**: 
  - **Type**: `String`
  - **Description**: Returns a message confirming that the OTP has been sent to the specified mobile number.

---

## 4. Validate OTP

### Description:
This API validates the OTP sent to the vendor's mobile number.

- **Request URL**: `localhost:9090/validate/OTP`
- **Request Method**: `POST`
- **Request Body**: JSON object containing the mobile number and OTP.
  
- **Response**: 
  - **Type**: `String`
  - **Description**: Returns a success or failure message depending on the validity of the OTP.

---

## 5. Check Mobile Number (New or Existing User)

### Description:
This API checks if a mobile number belongs to a new or existing vendor.

- **Request URL**: `localhost:9090/validate/mobile/{mobileNumber}`
- **Request Method**: `GET`
- **Path Parameter**:
  - `mobileNumber`: The mobile number to check.
  
- **Response**: 
  - **Type**: `String`
  - **Description**: If the mobile number is valid, it will send an OTP (similar to the "Send OTP" API) and proceed with OTP validation (similar to the "Validate OTP" API). The process follows the same steps as mentioned in points 3 and 4.
