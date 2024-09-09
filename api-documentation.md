# API Documentation
# Server-IP- http://54.224.210.106:9090 (prefix)
# example for testing http://localhost:9090/vendor/new/registration
TO
# http://54.172.41.93:9090/vendor/new/registration

# NOTE: Video uploads are currently limited to a maximum size of 4 MB, and image uploads are limited to a maximum size of 5 MB.
# Do not test OTP and email verification/validation; I am working on it.

# EC2 Linux Machine
  stop and kill the process 
   * sudo lsof -i :8080 | replace 8080 port to your application port
   * sudo kill -9 1234


## 1. Vendor Registration

### Description:
This API registers a new vendor in the system.

- **Request URL**: `localhost:9090/vendor/new/registration`
- **Request Method**: `POST`
- {
  "vendorId": 0,
  "fullName": "string",
  "salonName": "string",
  "vendorEmail": "string",
  "mobileNumber": 0,
  "vendorAddress": "string",
  "vendorCountry": "string",
  "vendorState": "string",
  "pincode": 0,
  "vensorCity": "string"
}
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
- {
  "vendorId": 0,
  "fullName": "string",
  "salonName": "string",
  "vendorEmail": "string",
  "mobileNumber": 0,
  "vendorAddress": "string",
  "vendorCountry": "string",
  "vendorState": "string",
  "pincode": 0,
  "vensorCity": "string"
}
  
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

---

## 6. Shop Gallery (Images)

### Description:
This API uploads images to the shop gallery.

- **Request URL**: `localhost:9090/shop/gallery/upload/images`
- **Request Method**: `POST`
- {
  "files": [
    "string"
  ]
}
  
- **Response**: 
  - **Type**: `String`
  - **Description**: Returns a confirmation message indicating the success or failure of the image upload.

---

## 7. Shop Gallery (Videos)

### Description:
This API uploads videos to the shop gallery. Currently, there is an issue with video uploads, which will be fixed soon.

- **Request URL**: `localhost:9090/shop/gallery/upload/videos`
- **Request Method**: `POST`
- {
  "files": [
    "string"
  ]
}
  
- **Response**: 
  - **Type**: `String`
  - **Description**: Returns a message indicating the status of the video upload.
  
**Note**: There is a known issue with uploading videos to the database.

---

## 8. Add Category (e.g., FEMALE, MEN, OTHERS)

### Description:
This API adds a new category to the listing service.

- **Request URL**: `localhost:9090/listing-service/add/category`
- **Request Method**: `POST`

- {
  "categoryId": 0,
  "categoryName": "string"
}
  
- **Response**: 
  - **Type**: `String`
  - **Description**: Returns a message confirming the successful addition of the category.

---

## 9. Add Product or Service Inside Category

### Description:
This API adds a product or service to a specific category.

- **Request URL**: `localhost:9090/listing-service/add-service/{categoryId}`
- **Request Method**: `POST`

- {
  "serviceId": 0,
  "serviceName": "string",
  "serviceCategory": {
    "categoryId": 0,
    "categoryName": "string"
  }
}
- **Path Parameter**:
  - `categoryId`: The ID of the category to which the product or service is being added.
  
- **Response**: 
  - **Type**: `String`
  - **Description**: Returns a message confirming the successful addition of the product or service.

---

## 10. Add Sub Product or Service Inside Product Category

### Description:
This API adds a sub-product or sub-service to a specific product category.

- **Request URL**: `localhost:9090/listing-service/add-sub/category/{productServiceId}`
- **Request Method**: `POST`

- {
  "subCategoryId": 0,
  "subCategoryName": "string",
  "serviceProduct": {
    "serviceId": 0,
    "serviceName": "string",
    "serviceCategory": {
      "categoryId": 0,
      "categoryName": "string"
    }
  },
  "price": 0
}
- **Path Parameter**:
  - `productServiceId`: The ID of the product or service to which the sub-product or sub-service is being added.
  
- **Response**: 
  - **Type**: `String`
  - **Description**: Returns a message confirming the successful addition of the sub-product or sub-service.

---

## 11. Show All Data by Category (e.g., FEMALE, MALE, OTHERS)

### Description:
This API retrieves and displays all data organized by category.

- **Request URL**: `localhost:9090/listing-service/category/{categoryName}`
- **Request Method**: `GET`
- **Path Parameter**:
  - `categoryName`: The name of the category (e.g., FEMALE, MALE, OTHERS) for which the data is to be displayed.
  
- **Response**: 
  - **Type**: `JSON`
  - {
  "serviceProduct": {
    "serviceId": 1,
    "serviceName": "Hair & Style",
    "serviceCategory": {
      "categoryId": 1,
      "categoryName": "FEMALE"
    }
  },
  "productSubCategory": {
    "subCategoryId": 1,
    "subCategoryName": "Boy Cut",
    "serviceProduct": {
      "serviceId": 1,
      "serviceName": "Hair & Style",
      "serviceCategory": {
        "categoryId": 1,
        "categoryName": "FEMALE"
      }
    },
    "price": 300
  },
  "message": "Data Found..!!"
}
  - **Description**: Returns a list of all data (products or services) under the specified category.
