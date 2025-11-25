# E-Commerce Application

A comprehensive Java-based e-commerce platform built with JavaFX, featuring separate interfaces for clients and vendors. This project serves as a Software Testing course project, demonstrating modern Java application development with Firebase backend integration.

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Running Tests](#running-tests)
- [Usage Guide](#usage-guide)
- [Architecture](#architecture)
- [Troubleshooting](#troubleshooting)

## Project Overview

This e-commerce application provides a full-featured online shopping platform with two distinct user roles:

- **Clients**: Browse products, manage shopping carts, create wishlists, place orders, and leave reviews
- **Vendors**: Add and manage products, track inventory, view and process orders

The application uses Firebase Firestore as the backend database and Cloudinary for image hosting, providing a scalable and cloud-based solution.

## Features

### Client Features
-  User authentication (Login/Signup)
-  Product browsing and search
-  Shopping cart management
-  Wishlist functionality
-  Order placement and tracking
-  Product reviews and ratings
-  Profile management
-  Payment processing

### Vendor Features
-  Vendor authentication
-  Add new products with images
-  Edit existing products
-  Inventory management
-  View and manage orders
-  Vendor profile management

## Technology Stack

- **Language**: Java 21/23
- **UI Framework**: JavaFX 21
- **Build Tool**: Maven
- **Backend**: Firebase Firestore
- **Image Hosting**: Cloudinary
- **Testing**: JUnit 5, Mockito
- **Architecture**: MVC (Model-View-Controller) with FXML

## Project Structure

```
GitVersion/
├── testingGUI/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/org/example/
│   │   │   │   ├── Application.java          # Main entry point
│   │   │   │   ├── Main.java                 # Alternative entry point
│   │   │   │   ├── GlobalData.java           # Global state management
│   │   │   │   ├── FireBaseManager.java      # Firebase operations
│   │   │   │   ├── SceneController.java      # Scene navigation
│   │   │   │   │
│   │   │   │   ├── Models/
│   │   │   │   │   ├── User.java             # Base user class
│   │   │   │   │   ├── Client.java           # Client model
│   │   │   │   │   ├── Vendor.java           # Vendor model
│   │   │   │   │   ├── Item.java             # Product model
│   │   │   │   │   ├── Cart.java             # Shopping cart model
│   │   │   │   │   ├── Order.java            # Order model
│   │   │   │   │   └── Review.java           # Review model
│   │   │   │   │
│   │   │   │   ├── Controllers/
│   │   │   │   │   ├── LogInController.java
│   │   │   │   │   ├── SignUpController.java
│   │   │   │   │   ├── MainClientPageController.java
│   │   │   │   │   ├── MainVendorPageController.java
│   │   │   │   │   ├── CartController.java
│   │   │   │   │   ├── CheckoutController.java
│   │   │   │   │   ├── PaymentPageController.java
│   │   │   │   │   └── ... (other controllers)
│   │   │   │   │
│   │   │   │   └── Exceptions/
│   │   │   │       ├── LogInException.java
│   │   │   │       ├── RegistrationException.java
│   │   │   │       └── ... (other exceptions)
│   │   │   │
│   │   │   └── resources/org/example/testinggui/
│   │   │       ├── LogIn.fxml
│   │   │       ├── SignUp.fxml
│   │   │       ├── MainPageClient.fxml
│   │   │       ├── MainVendorPage.fxml
│   │   │       └── ... (other FXML files)
│   │   │
│   │   └── test/java/org/example/
│   │       ├── TestSuite.java                # Test suite runner
│   │       ├── ClientTest.java
│   │       ├── VendorTest.java
│   │       ├── OrderTest.java
│   │       ├── CartTest.java
│   │       ├── ItemTest.java
│   │       ├── ReviewTest.java
│   │       ├── UserTest.java
│   │       ├── IntegrationTest.java
│   │       └── ... (white-box testing files)
│   │
│   ├── firebase-credentials.json  # Firebase credentials
│   └── pom.xml                                # Maven configuration
│
└── README.md
```

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

1. **Java Development Kit (JDK) 21 or higher**
   - Download from [Oracle](https://www.oracle.com/java/technologies/downloads/) or [OpenJDK](https://openjdk.org/)
   - Verify installation: `java -version`

2. **Apache Maven 3.6+**
   - Download from [Maven Website](https://maven.apache.org/download.cgi)
   - Verify installation: `mvn -version`

3. **Firebase Project**
   - Create a project at [Firebase Console](https://console.firebase.google.com/)
   - Generate a service account key (JSON file)
   - Place the JSON file in the `testingGUI/` directory

4. **Cloudinary Account** (for image hosting)
   - Sign up at [Cloudinary](https://cloudinary.com/)
   - Note your cloud name, API key, and API secret

5. **IDE (Optional but recommended)**
   - IntelliJ IDEA, Eclipse, or VS Code with Java extensions

## Setup Instructions

### 1. Clone the Repository

```bash
git clone <repository-url>
cd e-commerce-app
```

### 2. Configure Firebase

1. Obtain your Firebase service account JSON file from the Firebase Console:
   - Go to Project Settings → Service Accounts
   - Click "Generate New Private Key"
   - Save the JSON file

2. Place the JSON file in the `testingGUI/` directory:
   ```
   testingGUI/firebase-credentials.json
   ```

3. Update the Firebase credentials path in `FireBaseManager.java`:
   ```java
   // Line 24 in FireBaseManager.java
   FileInputStream serviceAccount = new FileInputStream("path/to/your/firebase-credentials.json");
   ```

### 3. Configure Application Paths

Update the resource path in `GlobalData.java` to match your system:

```java
// Line 7 in GlobalData.java
public static String path = "/absolute/path/to/testingGUI/src/main/resources/org/example/testinggui/";
```

**For macOS/Linux:**
```java
public static String path = "/Users/YourUsername/path/to/GitVersion/testingGUI/src/main/resources/org/example/testinggui/";
```

**For Windows:**
```java
public static String path = "C:\\Users\\YourUsername\\path\\to\\GitVersion\\testingGUI\\src\\main\\resources\\org\\example\\testinggui\\";
```

### 4. Configure Cloudinary (Optional)

If you need to change Cloudinary credentials, update `FireBaseManager.java`:

```java
// Line 36 in FireBaseManager.java
Cloudinary cloudinary = new Cloudinary("cloudinary://API_KEY:API_SECRET@CLOUD_NAME");
```

### 5. Install Dependencies

Navigate to the `testingGUI` directory and install Maven dependencies:

```bash
cd testingGUI
mvn clean install
```

## Running the Application

### Method 1: Using Maven (Recommended)

From the `testingGUI` directory:

```bash
mvn clean javafx:run
```

### Method 2: Using IDE

1. Open the project in your IDE (IntelliJ IDEA, Eclipse, etc.)
2. Navigate to `org.example.Application`
3. Run the `main` method

### Method 3: Using Java Command Line

```bash
cd testingGUI
mvn clean compile
java --module-path /path/to/javafx/lib --add-modules javafx.controls,javafx.fxml -cp target/classes org.example.Application
```

**Note**: You'll need to download JavaFX SDK separately and specify the module path.

## Running Tests

### Run All Tests

```bash
cd testingGUI
mvn test
```

### Run Specific Test Class

```bash
mvn test -Dtest=ClientTest
```

### Run Test Suite

```bash
mvn test -Dtest=TestSuite
```

### View Test Reports

After running tests, view the reports at:
```
testingGUI/target/surefire-reports/
```

## Usage Guide

### First Time Setup

1. **Start the Application**
   - Run the application using one of the methods above
   - The login screen will appear

2. **Create an Account**
   - Click "Sign Up" on the login screen
   - Choose between Client or Vendor account
   - Fill in all required information:
     - Name
     - User ID (unique identifier)
     - Email
     - Password
     - Address
     - Phone Number
   - Click "Sign Up" to create your account

3. **Login**
   - Enter your User ID and Password
   - Click "Sign In"
   - You'll be redirected to your respective dashboard

### Client Workflow

1. **Browse Products**
   - View all available products on the main page
   - Click on a product to see details

2. **Add to Cart**
   - Click "Add to Cart" on any product
   - View your cart by clicking the "Cart" button

3. **Checkout**
   - Review items in your cart
   - Proceed to checkout
   - Enter payment information
   - Confirm your order

4. **Manage Profile**
   - Click "Profile" to view/edit your information
   - Update address, phone number, or password

5. **View Orders**
   - Access your order history from the profile page
   - Track order status and details

### Vendor Workflow

1. **Add Products**
   - Click "Add Product" on the vendor dashboard
   - Fill in product details:
     - Name
     - Description
     - Category
     - Price
     - Stock quantity
     - Product image (local file path)
   - Submit to add the product

2. **Manage Products**
   - View all your products on the dashboard
   - Click on a product to edit details
   - Update stock, price, or other information

3. **View Orders**
   - Access orders from your dashboard
   - View order details and customer information
   - Update order status

## Architecture

### Design Pattern
The application follows the **Model-View-Controller (MVC)** pattern:

- **Model**: Java classes (`User`, `Client`, `Vendor`, `Item`, `Cart`, `Order`, etc.)
- **View**: FXML files defining the UI layout
- **Controller**: JavaFX controllers handling user interactions and business logic

### Key Components

1. **FireBaseManager**: Singleton class managing all Firebase operations
2. **SceneController**: Handles navigation between different scenes
3. **GlobalData**: Manages global application state (current user, selected items, etc.)
4. **Exception Handling**: Custom exceptions for various error scenarios

### Data Flow

```
User Action (FXML) 
    → Controller 
    → Model/Business Logic 
    → FireBaseManager 
    → Firebase Firestore
```

## Troubleshooting

### Common Issues

1. **"Failed to initialize Firebase" Error**
   - Ensure the Firebase JSON file is in the correct location
   - Verify the file path in `FireBaseManager.java` is correct
   - Check that the JSON file has valid credentials

2. **"File not found" Error for FXML Files**
   - Update the `path` variable in `GlobalData.java` with the correct absolute path
   - Ensure the path uses forward slashes (/) or double backslashes (\\) for Windows

3. **JavaFX Runtime Not Found**
   - Ensure JavaFX dependencies are properly downloaded via Maven
   - If using command line, download JavaFX SDK separately and specify module path

4. **Maven Build Fails**
   - Check Java version: `java -version` (should be 21+)
   - Clean and rebuild: `mvn clean install`
   - Check internet connection for dependency downloads

5. **Tests Fail**
   - Ensure Firebase is properly configured
   - Check that test data exists in Firebase
   - Review test logs in `target/surefire-reports/`

6. **Image Upload Issues**
   - Verify Cloudinary credentials in `FireBaseManager.java`
   - Ensure image file paths are correct and accessible
   - Check internet connection for Cloudinary API calls

### Getting Help

If you encounter issues not listed here:
1. Check the console output for detailed error messages
2. Review Firebase console for database connection issues
3. Verify all configuration paths are correct
4. Ensure all prerequisites are properly installed

## Notes

- The application uses hardcoded paths in some places (`GlobalData.java`, `FireBaseManager.java`). These should be updated to match your system.
- Firebase credentials are sensitive - never commit them to version control in production.
- The application requires an active internet connection for Firebase and Cloudinary services.
- JavaFX applications may require additional VM arguments in some IDEs.

## License

This project is developed for educational purposes as part of a Software Testing course.

---
