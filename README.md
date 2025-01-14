# Reqres-API-Testing-with-Newman-Report
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations
  
### **Technology used:**
- Postman
- Newman

### **Prerequisite:**
- Node Js
- Newman
- Newman Html Report Library

### **Installation**

1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:
 ```console 
  git clone https://github.com/jasminakterr/Reqres-API-Testing-with-Newman-Report
```
3. Import the Postman collection:
    - Open Postman.
    - Click on the Import button.
    - Select the file from the repository.
4. Import the Postman environment:
    - In Postman, click on the gear icon in the top right corner.
    - Select **Import** and choose the file.
5. Newman and Report Installation Process:
    - Newman Install Command:
     ```console 
      npm install -g newman
    ```
    - Newman Html Report Install Command:
     ```console 
      npm install -g newman-reporter-htmlextra
    ```
### **Usage**
1. Select Environment:
    -   In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
3. Run Collection:
    -   Select the imported collection from the Collections sidebar.
    -   Click on the Runner button to open the collection runner.
    -   Select the desired environment.
    -   Click Start Test to run the collection.
8. View Results:
    -   Once the tests are complete, view the results in the Runner tab.
    -   Detailed test results can be viewed for each request.

## **Testing**

## Test Case Scenarios:

## _**1. Get User**_

### Request URL: https://reqres.in/api/users?page=2
### Request Method: Get
### Post-request Script:
```console 
   var jsonData = pm.response.json()

pm.environment.set("id", jsonData.data[1].id);

    pm.test("Validate the status code is 200 ", function(){
    pm.response.to.have.status(200);
})


pm.test("Verify the page value is 2", function(){
    const jsonData = pm.response.json();
   pm.expect(jsonData.page).to.eql(2);

  }) 

    pm.test("Validate that all user data contains the fields id, email, first_name, last_name, and avatar", function(){
    const jsonData = pm.response.json().data[0];
    pm.expect(jsonData).to.have.property('id');
    pm.expect(jsonData).to.have.property('email');
    pm.expect(jsonData).to.have.property('first_name');
    pm.expect(jsonData).to.have.property('last_name');
    pm.expect(jsonData).to.have.property('avatar');
});

 ## _**1. Create User**_
### Request URL: https://reqres.in/api/users
### Request Method: POST
### Request Body:
 ```console 
{
    "name": "John Doe",
    "job": "Software Engineer"
}
```
### Response Body
 ```console 
{
    "name": "John Doe",
    "job": "Software Engineer",
    "id": "987",
    "createdAt": "2025-01-14T08:34:22.511Z"
}
```
### Post-request Script:
```console 
var jsonData = pm.response.json();

//Status Code Validation    
  pm.test("Validate the status code is 201 ", function(){
    pm.response.to.have.status(201);
})

//Name & Job Validation
  pm.test("Verify the name and job fields in the response match the request payload", function(){
    var jsonData = pm.response.json();
    pm.expect(jsonData.name).to.eql("John Doe");
    pm.expect(jsonData.job).to.eql("Software Engineer");
});

//ID & Create Date Validation
  pm.test("Validate the presence of the id and createdAt fields in the response", function(){
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('id');
    pm.expect(jsonData).to.have.property('createdAt');
});


## _**3. Get User By ID.**_
### Request URL: https://reqres.in/api/users/8
### Request Method: GET
### Post-request Script:
```console
var jsonData = pm.response.json();
//Status Code Validation
    pm.test("Validate the status code is 200 ", function(){
    pm.response.to.have.status(200);
})

//ID, Email, First Name, Last Name, Avatar Validation
pm.test("Validate that all user data contains the fields id, email, first_name, last_name, and avatar", function(){
    const jsonData = pm.response.json().data;
    pm.expect(jsonData).to.have.property('id');
    pm.expect(jsonData).to.have.property('email');
    pm.expect(jsonData).to.have.property('first_name');
    pm.expect(jsonData).to.have.property('last_name');
    pm.expect(jsonData).to.have.property('avatar');
});

//URL & Text Validation
pm.test("Ensure the support section contains valid url and text fields", function(){
    const jsonData = pm.response.json().support;
    pm.expect(jsonData).to.have.property('url');
    pm.expect(jsonData).to.have.property('text');
});

```

 ## _**4. Update User**_
### Request URL: https://reqres.in/api/users/4
### Request Method: PUT
### Post-request Script:
```console 
    var jsonData = pm.response.json();

//Status Code Validation
    pm.test("Validate the status code is 200 ", function(){
    pm.response.to.have.status(200);
})

//Name & Job Validation
pm.test("Verify the name and job fields in the response match the request payload", function(){
    var jsonData = pm.response.json();
    pm.expect(jsonData.name).to.eql("Jasmin Akter");
    pm.expect(jsonData.job).to.eql("SQA Engineer");
});

//Update Date Validation
pm.test("Validate the presence of the id and createdAt fields in the response", function(){
    const jsonData = pm.response.json();

    pm.expect(jsonData).to.have.property('updatedAt');
});
```
  **Request Body:** 
 ```console 
 {
    "name": "Jasmin Akter",
    "job": "SQA Engineer"
}
```
  **Response Body:**
 ```console 
 {
    "name": "Jasmin Akter",
    "job": "SQA Engineer",
    "updatedAt": "2025-01-14T08:35:16.858Z"
}

```

 ## _**5. Delete User Record**_

### Request URL: https://reqres.in/api/users/4
### Request Method: DELETE
### Response Body: None
### Post-Request Body:
 ```console 
pm.test("Validate the status code is 204 ", function(){
    pm.response.to.have.status(204);
})

pm.test("Ensure the response body is empty", function () {
    pm.expect(pm.response.text()).to.equal("");
});
```

## Run Command:  
- Run Command for Console: 
```console 
newman run Practice_API_Testing.postman_collection.json -e Testing.postman_environment.json
```
- Run Command for Report: 
```console 
newman run Practice_API_Testing.postman_collection.json -e Testing.postman_environment.json -r htmlextra
```

## Newman Report Summary:
![Report ](https://github.com/user-attachments/assets/47c78726-440d-4377-9daf-198d92e50cea)

![Report 2 ](https://github.com/user-attachments/assets/9bf52462-d944-4751-a9c9-27a58e83f966)

![Report 3](https://github.com/user-attachments/assets/b7eaffa3-b1da-4e9a-b21e-7fba5ddde4c9)

![Report 4](https://github.com/user-attachments/assets/bacfe3f3-c581-46de-9f2d-bae3fad1eb51)
