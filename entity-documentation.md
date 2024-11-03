# Salon Management System - Entity Documentation
## Version 1.0
### Table of Contents
1. [Introduction](#introduction)
2. [Entity Classes](#entity-classes)
3. [Entity Relationships](#entity-relationships)
4. [Data Types and Constraints](#data-types-and-constraints)

---

## 1. Introduction <a name="introduction"></a>

This document provides detailed information about the entity classes used in the Salon Management System. These entities represent the core data structures of the application and their relationships.

---

## 2. Entity Classes <a name="entity-classes"></a>

### 2.1 Vendor Registration
**Class Name**: `Vendor_Registration`
**Purpose**: Manages salon vendor registration information

**Attributes**:
| Field Name | Data Type | Description |
|------------|-----------|-------------|
| vendorId | Long | Primary identifier for the vendor |
| fullName | String | Full name of the vendor |
| salonName | String | Name of the salon |
| vendorEmail | String | Email address of the vendor |
| password | String | Encrypted password |
| mobileNumber | Long | Contact number |

### 2.2 Service Category
**Class Name**: `ServiceCategory`
**Purpose**: Defines categories of services offered

**Attributes**:
| Field Name | Data Type | Description |
|------------|-----------|-------------|
| categoryId | Integer | Primary identifier for the category |
| categoryName | String | Name of the service category |
| vendorId | Long | Reference to the vendor |
| serviceProducts | List<ServiceProduct> | List of services in this category |

**Annotations**:
- `@OneToMany` relationship with ServiceProduct
- Uses `CascadeType.ALL` for automatic persistence
- `@JsonManagedReference` for handling JSON serialization

### 2.3 Service Product
**Class Name**: `ServiceProduct`
**Purpose**: Defines specific services within categories

**Attributes**:
| Field Name | Data Type | Description |
|------------|-----------|-------------|
| serviceId | Integer | Primary identifier for the service |
| serviceName | String | Name of the service |
| serviceCategory | ServiceCategory | Reference to parent category |
| vendorId | Long | Reference to the vendor |
| subCategories | List<ProductSubCategory> | List of sub-categories |

### 2.4 Product Sub Category
**Class Name**: `ProductSubCategory`
**Purpose**: Defines variations of services

**Attributes**:
| Field Name | Data Type | Description |
|------------|-----------|-------------|
| subCategoryId | Integer | Primary identifier |
| subCategoryName | String | Name of the sub-category |
| price | Integer | Price of the service |
| serviceProduct | ServiceProduct | Reference to parent service |
| vendorId | Long | Reference to the vendor |

### 2.5 Shop Gallery Images
**Class Name**: `ShopGalleryImages`
**Purpose**: Stores salon images

**Attributes**:
| Field Name | Data Type | Description |
|------------|-----------|-------------|
| id | Integer | Primary identifier |
| vendorId | Long | Reference to the vendor |
| fileName | String | Name of the image file |
| fileType | String | Type of the image file |
| data | byte[] | Binary data of the image |

### 2.6 Shop Gallery Videos
**Class Name**: `ShopGalleryVideos`
**Purpose**: Stores salon videos

**Attributes**:
| Field Name | Data Type | Description |
|------------|-----------|-------------|
| shopGalleryVideoId | Integer | Primary identifier |
| vendorId | Long | Reference to the vendor |
| fileName | String | Name of the video file |
| fileType | String | Type of the video file |
| data | byte[] | Binary data of the video |

### 2.7 Bank Account
**Class Name**: `BankAccount`
**Purpose**: Manages vendor bank account information

**Attributes**:
| Field Name | Data Type | Constraints | Description |
|------------|-----------|-------------|-------------|
| id | Long | Primary Key | Unique identifier |
| vendorId | Long | Not Null | Reference to vendor |
| accountHolderName | String | Not Null | Name on account |
| bankAccountNumber | Long | Not Null | Account number |
| bankName | String | Not Null | Name of bank |
| ifscCode | String | Not Null | IFSC code |
| emailAddress | String | Not Null | Email address |
| mobileNumber | Long | Not Null | Contact number |
| address | String | Not Null | Bank address |
| bankSelection | String | Not Null | Selected bank type |

### 2.8 Amenity
**Class Name**: `Amenity`
**Purpose**: Defines salon amenities

**Attributes**:
| Field Name | Data Type | Description |
|------------|-----------|-------------|
| amenityId | Long | Primary identifier |
| name | String | Name of the amenity |
| vendors | Set<Vendor_Registration> | Associated vendors |

### 2.9 Business Document
**Class Name**: `BusinessDocument`
**Purpose**: Stores business-related documents

**Attributes**:
| Field Name | Data Type | Description |
|------------|-----------|-------------|
| id | Long | Primary identifier |
| vendorId | Long | Reference to vendor |
| identyFileType | String | Type of identity document |
| identyFileName | String | Name of identity file |
| identityProofData | byte[] | Binary data of identity proof |
| agreementfileType | String | Type of agreement file |
| agreementFileName | String | Name of agreement file |
| agreementData | byte[] | Binary data of agreement |

### 2.10 Admin Coupons
**Class Name**: `AdminCoupons`
**Purpose**: Manages system-wide coupons

**Attributes**:
| Field Name | Data Type | Description |
|------------|-----------|-------------|
| couponId | Integer | Primary identifier |
| adminId | Long | Reference to admin |
| couponName | String | Name of coupon |
| couponPrice | Long | Value of coupon |
| couponCreationTime | LocalDate | Creation timestamp |
| couponExpirationTime | LocalDate | Expiry timestamp |
| numberOfUsages | Integer | Usage limit |
| numberOfDays | Integer | Validity period |
| isActive | boolean | Active status |
| applicableForAllVendors | boolean | Universal applicability |
| applicableVendors | Set<Vendor_Registration> | Specific vendors |

### 2.11 Coupon Usage
**Class Name**: `CouponUsage`
**Purpose**: Tracks coupon usage

**Attributes**:
| Field Name | Data Type | Description |
|------------|-----------|-------------|
| id | Integer | Primary identifier |
| customerId | Long | Reference to customer |
| coupon | VendorCoupons | Reference to coupon |

### 2.12 OTP Verification
**Class Name**: `OtpVerification`
**Purpose**: Manages OTP verification process

**Attributes**:
| Field Name | Data Type | Description |
|------------|-----------|-------------|
| id | Long | Primary identifier |
| vendorEmail | String | Email for verification |
| otp | int | OTP code |
| expirationTime | LocalDateTime | OTP expiry time |

---

## 3. Entity Relationships <a name="entity-relationships"></a> Database relationship

### One-to-Many Relationships
1. ServiceCategory → ServiceProduct
   - One category can have multiple services
   - Cascade type: ALL
   - Bidirectional mapping

2. ServiceProduct → ProductSubCategory
   - One service can have multiple sub-categories
   - Cascade type: ALL
   - Orphan removal enabled

### Many-to-One Relationships
1. ServiceProduct → ServiceCategory
   - Each service belongs to one category
   - JSON back reference configured

2. ProductSubCategory → ServiceProduct
   - Each sub-category belongs to one service

### Many-to-Many Relationships
1. Vendor_Registration ↔ Amenity
   - Vendors can have multiple amenities
   - Amenities can be associated with multiple vendors

2. AdminCoupons ↔ Vendor_Registration
   - Coupons can be applicable to multiple vendors
   - Vendors can have multiple applicable coupons
   - Lazy fetching enabled

---

## 4. Data Types and Constraints <a name="data-types-and-constraints"></a>

### Primary Keys
- Most entities use auto-generated identity strategy
- IDs are typically Integer or Long type

### Binary Data Storage
- Images and videos use LONGBLOB data type
- Stored as byte arrays with @Lob annotation

### Date/Time Fields
- LocalDate used for coupon dates
- LocalDateTime used for OTP expiration

### Relationships
- Proper indexing through foreign keys
- Cascade operations where appropriate
- Lazy loading for large collections

---


