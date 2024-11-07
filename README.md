Postman Collection Documentation
================================

**Collection Overview**
-----------------------

This collection contains API tests for the **Restful Booker** API hosted at the domain https://restful-booker.herokuapp.com/. The tests cover various endpoints such as authentication, booking creation, updating, retrieving, and deleting bookings. Each request is equipped with automated test scripts that verify the correctness of the API responses.

**API Main Domain**
-------------------

*   **Base URL**: https://restful-booker.herokuapp.com/
    

All requests are made to this domain with the appropriate endpoints for authentication, booking operations, and other functionalities.

**1\. Authentication (POST /auth)**
-----------------------------------

### **Request Details**

*   **Endpoint**: POST https://restful-booker.herokuapp.com/auth
    
*   **Headers**:
    
    *   Content-Type: application/json
        
*   jsonCopy code{ "username": "admin", "password": "password123"}
    

### **Test Scripts**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   javascriptCopy code// Test: Status code is 200  pm.test("Status code is 200", function () {      pm.response.to.have.status(200);  });  // Test: Response content type is JSON  pm.test("Response should be JSON", function () {      pm.response.to.have.header("Content-Type", /application\/json/);  });  // Test: Token is present in the response  pm.test("Token is present in the response", function () {      var responseJson = pm.response.json();      pm.expect(responseJson).to.have.property("token");      pm.environment.set("auth_token", responseJson.token); // Store token for use in subsequent requests  });   `

### **Expected Results**

*   **Status Code**: 200 (OK)
    
*   **Content-Type**: application/json
    
*   **Response Body**: The response body should contain a token field.
    

**2\. Create Booking (POST /booking)**
--------------------------------------

### **Request Details**

*   **Endpoint**: POST https://restful-booker.herokuapp.com/booking
    
*   **Headers**:
    
    *   Content-Type: application/json
        
    *   Cookie: token={{auth\_token}} (Dynamically populated from authentication)
        
*   jsonCopy code{ "firstname": "John", "lastname": "Doe", "totalprice": 200, "depositpaid": true, "bookingdates": { "checkin": "2023-12-01", "checkout": "2023-12-10" }, "additionalneeds": "Lunch"}
    

### **Test Scripts**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   javascriptCopy code// Test: Status code is 200  pm.test("Status code is 200", function () {      pm.response.to.have.status(200);  });  // Test: Response content type is JSON  pm.test("Response should be JSON", function () {      pm.response.to.have.header("Content-Type", /application\/json/);  });  // Test: Response contains booking ID  pm.test("Response contains booking ID", function () {      var responseJson = pm.response.json();      pm.expect(responseJson).to.have.property("bookingid");      pm.environment.set("booking_id", responseJson.bookingid); // Store booking ID for use in subsequent requests  });   `

### **Expected Results**

*   **Status Code**: 200 (OK)
    
*   **Content-Type**: application/json
    
*   **Response Body**: The response should contain a bookingid field, which will be stored for later use.
    

**3\. Update Booking (PUT /booking/{bookingId})**
-------------------------------------------------

### **Request Details**

*   **Endpoint**: PUT https://restful-booker.herokuapp.com/booking/{{booking\_id}}
    
    *   The booking\_id is dynamically set in the environment and is the ID from the previous "Create Booking" step.
        
*   **Headers**:
    
    *   Content-Type: application/json
        
    *   Cookie: token={{auth\_token}}
        
*   jsonCopy code{ "firstname": "James", "lastname": "Brown", "totalprice": 111, "depositpaid": true, "bookingdates": { "checkin": "2018-01-01", "checkout": "2019-01-01" }, "additionalneeds": "Breakfast"}
    

### **Test Scripts**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   javascriptCopy code// Test: Status code is 200  pm.test("Status code is 200", function () {      pm.response.to.have.status(200);  });  // Test: Response content type is JSON  pm.test("Response should be JSON", function () {      pm.response.to.have.header("Content-Type", /application\/json/);  });  // Test: Response contains updated booking data  pm.test("Response contains updated booking data", function () {      var responseJson = pm.response.json();      pm.expect(responseJson.firstname).to.eql("James");      pm.expect(responseJson.lastname).to.eql("Brown");      pm.expect(responseJson.totalprice).to.eql(111);      pm.expect(responseJson.depositpaid).to.eql(true);      pm.expect(responseJson.bookingdates.checkin).to.eql("2018-01-01");      pm.expect(responseJson.bookingdates.checkout).to.eql("2019-01-01");      pm.expect(responseJson.additionalneeds).to.eql("Breakfast");  });   `

### **Expected Results**

*   **Status Code**: 200 (OK)
    
*   **Content-Type**: application/json
    
*   **Response Body**: The updated booking details should reflect the changes made in the request body.
    

**4\. Get Booking (GET /booking)**
----------------------------------

### **Request Details**

*   **Endpoint**: GET https://restful-booker.herokuapp.com/booking?firstname=sally&lastname=brown
    
*   **Headers**:
    
    *   Content-Type: application/json
        

### **Test Scripts**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   javascriptCopy code// Test: Status code is 200  pm.test("Status code is 200", function () {      pm.response.to.have.status(200);  });  // Test: Response content type is JSON  pm.test("Response should be JSON", function () {      pm.response.to.have.header("Content-Type", /application\/json/);  });  // Test: Response contains an array of booking IDs  pm.test("Response body contains an array of booking IDs", function () {      var responseJson = pm.response.json();      pm.expect(responseJson).to.be.an("array");      if (responseJson.length > 0) {          pm.expect(responseJson[0]).to.have.property("bookingid");      }  });   `

### **Expected Results**

*   **Status Code**: 200 (OK)
    
*   **Content-Type**: application/json
    
*   **Response Body**: An array of booking objects, each containing a bookingid.
    

**5\. Delete Booking (DELETE /booking/{bookingId})**
----------------------------------------------------

### **Request Details**

*   **Endpoint**: DELETE https://restful-booker.herokuapp.com/booking/{{booking\_id}}
    
    *   The booking\_id is dynamically set in the environment, referencing the ID stored from the "Create Booking" or "Update Booking" steps.
        
*   **Headers**:
    
    *   Content-Type: application/json
        
    *   Cookie: token={{auth\_token}}
        

### **Test Scripts**

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   javascriptCopy code// Test: Status code is 200 (or 204 depending on the response)  pm.test("Status code is 200", function () {      pm.response.to.have.status(200);  });  // Test: Response content type is JSON  pm.test("Response should be JSON", function () {      pm.response.to.have.header("Content-Type", /application\/json/);  });  // Test: Verify the booking has been deleted (response should not contain booking data)  pm.test("Booking should be deleted", function () {      var responseJson = pm.response.json();      pm.expect(responseJson).to.not.have.property("bookingid");  });   `

### **Expected Results**

*   **Status Code**: 200 (OK) or 204 (No Content), depending on the API behavior.
    
*   **Content-Type**: application/json
    
*   **Response Body**: The booking should be deleted, and the response should reflect this (e.g., no bookingid in the response body).
    

**How to Execute the Collection**
---------------------------------

1.  **Open Postman** and go to the **Collections** tab.
    
2.  **Import the Collection**: If you received this markdown with a .json file, import the collection by clicking the **Import** button in Postman and selecting the file.
    
3.  **Set Up the Environment**: Ensure the environment variable auth\_token is correctly set.
    
4.  **Run the Collection**:
    
    *   Click the **Runner** button in Postman.
        
    *   Select your collection and click **Run**.
        
5.  **Review Results**: Check the **Test Results** section after execution to confirm that the tests have passed.
