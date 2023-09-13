# Introduction
This document explains how to run an API test with Postman against. 

# Summery    
I have Completed an API test of student details, Create Student, Get Specific Student, Create Technical Skills, Create Student Address.
https://thetestingworldapi.com/   
<p align="center">
  <img src="https://github.com/SHANJIDA-HRIDE/API-Testing-with-Postman/assets/62147630/257e086c-a3ef-431c-9ea8-b27ee39a8ab2" />
</p>
 

Here in this API student details viewed and different tests were performed like GET, POST, PUT,DELETE.

**Summary:** Test Scripts 6 and Total 20 assertions were done. All of them passed with 0 skipped tests. The number of iteration was 1.



# Requirements  
**Java**  
https://www.oracle.com/java/technologies/downloads/   
**Postman**   
https://www.postman.com/   
**Node JS**   
https://nodejs.org/en/    



# Assertions Details    
#### Get Student
##Test Script
```bash
var jsonData = pm.response.json()
var ststuscode = pm.response.code
console.log(jsonData.length)

if(ststuscode==200){
var jsonData = pm.response.json()
pm.test(" 200 OK", function(){
    pm.response.to.have.status(200);
});
}
else if(ststuscode==404){

    pm.test("Not Found", function(){
    pm.response.to.have.status(404);
    });
}

else if(ststuscode==200){

    pm.test("OK", function(){
    pm.response.to.have.status(200);
    });
}

else if(ststuscode==201){

    pm.test("Created", function(){
    pm.response.to.have.status(201);
    });
}

else if(ststuscode==202){

    pm.test("Accepted", function(){
    pm.response.to.have.status(202);
    });
}

else if(ststuscode==400){

    pm.test("Bad Request", function(){
    pm.response.to.have.status(400);
    });
}

else if(ststuscode==401){

    pm.test("Unauthorized", function(){
    pm.response.to.have.status(401);
    });
}

else if(ststuscode==403){

    pm.test("Fordidden", function(){
    pm.response.to.have.status(403);
    });
}

else if(ststuscode==405){

    pm.test("Method Not Allowed", function(){
    pm.response.to.have.status(405);
    });
}

else if(ststuscode==500){

    pm.test("Internal Server Error", function(){
    pm.response.to.have.status(500);
    });
}

else if(ststuscode==501){

    pm.test("Not Implimented", function(){
    pm.response.to.have.status(501);
    });
}

else if(ststuscode==502){

    pm.test("Bad Gateway", function(){
    pm.response.to.have.status(502);
    });
}

else if(ststuscode==503){

    pm.test("Service Unavailable", function(){
    pm.response.to.have.status(503);
    });
}

else{
    pm.test("Something Else!!!!")
}     
```
#### Create Student
##Body
```bash   
{
"first_name": "{{firstName}}", 
"middle_name": "{{middleName}}", 
"last_name": "{{lastName}}", 
"date_of_birth": "{{date_of_birth}}" 
}
```

##Pre-Request Scripts 

```bash   
var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
console.log("First Name Value:  "+ firstName)
pm.environment.set("firstName",firstName)

var middleName = pm.variables.replaceIn("{{$randomLastName}}")
console.log("Middle Name Value:  "+ middleName)
pm.environment.set("middleName",middleName)

var lastName = pm.variables.replaceIn("{{$randomLastName}}")
console.log("Last Name Value:  "+ lastName)
pm.environment.set("lastName",lastName)

const moment = require('moment')
const today = moment()
console.log(today.format("YYYY-MM-DD"))
pm.environment.set("date_of_birth",today.add(1,'d').format("YYYY-MM-DD"))
```
##Test Script
```bash
var jsonData = pm.response.json()
pm.environment.set("id", jsonData.id)

var ststuscode = pm.response.code
console.log(ststuscode)

if(ststuscode==201){
var jsonData = pm.response.json()
pm.test(" 201 Created", function(){
    pm.response.to.have.status(201);
});
}
else if(ststuscode==404){

    pm.test("Not Found", function(){
    pm.response.to.have.status(404);
    });
}

else if(ststuscode==200){

    pm.test("OK", function(){
    pm.response.to.have.status(200);
    });
}



else if(ststuscode==202){

    pm.test("Accepted", function(){
    pm.response.to.have.status(202);
    });
}

else if(ststuscode==400){

    pm.test("Bad Request", function(){
    pm.response.to.have.status(400);
    });
}

else if(ststuscode==401){

    pm.test("Unauthorized", function(){
    pm.response.to.have.status(401);
    });
}

else if(ststuscode==403){

    pm.test("Fordidden", function(){
    pm.response.to.have.status(403);
    });
}

else if(ststuscode==405){

    pm.test("Method Not Allowed", function(){
    pm.response.to.have.status(405);
    });
}

else if(ststuscode==500){

    pm.test("Internal Server Error", function(){
    pm.response.to.have.status(500);
    });
}

else if(ststuscode==501){

    pm.test("Not Implimented", function(){
    pm.response.to.have.status(501);
    });
}

else if(ststuscode==502){

    pm.test("Bad Gateway", function(){
    pm.response.to.have.status(502);
    });
}

else if(ststuscode==503){

    pm.test("Service Unavailable", function(){
    pm.response.to.have.status(503);
    });
}

else{
    pm.test("Something Else!!!!")
}
});
```   
#### Get Specific Student  
```bash
const response = pm.response.json();

// set environment isbn

pm.environment.set("isbn1", response.books[0].isbn);
pm.environment.set("isbn2", response.books[1].isbn);
pm.environment.set("isbn3", response.books[2].isbn);
pm.environment.set("forUpdatingOrderLater", response.books[3].isbn);

// Expected status code and response status code same or not
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});


// environment isbn and actual isbn same or not
pm.test("Test isbn1", function () {
    pm.expect(response.books[0].isbn).to.eql(pm.environment.get("isbn1"))
})
pm.test("Test isbn2", function () {
    pm.expect(response.books[1].isbn).to.eql(pm.environment.get("isbn2"))
})
pm.test("Test isbn3", function () {
    pm.expect(response.books[2].isbn).to.eql(pm.environment.get("isbn3"))
})
pm.test("Test For Updating Order Later", function () {
    pm.expect(response.books[3].isbn).to.eql(pm.environment.get("forUpdatingOrderLater"))
})
```   
#### Ordering Books    
```bash
// Expected status code and response status code same or not
pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
});

// environment isbn and actual isbn same or not

var jsonData = pm.response.json();

pm.test("Test Fist order", function () {
    pm.expect(jsonData.books[0].isbn).to.eql(pm.environment.get("isbn1"))
})
pm.test("Test Second Order", function () {
    pm.expect(jsonData.books[1].isbn).to.eql(pm.environment.get("isbn2"))
})
pm.test("Test Third Order", function () {
    pm.expect(jsonData.books[2].isbn).to.eql(pm.environment.get("isbn3"))
})
```   

#### Order Book Detail     
```bash
// Expected status code and response status code same or not
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});


// set environment fist_orderd_book_in_the_list
var jsonData = pm.response.json();
pm.environment.set("fist_orderd_book_in_the_list", jsonData.books[0].isbn);


// environment userID and actual userID same or not
pm.test("Test userID", function () {
    pm.expect(jsonData.userId).to.eql(pm.environment.get("userID"))
})


// environment userName and actual userName same or not

pm.test("Test username", function () {
    pm.expect(jsonData.username).to.eql(pm.environment.get("userName"))
})
```  

#### Book ISBN Detail      
```bash
const jsonData = pm.response.json();

// Expected status code and response status code same or not
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});


// environment fist_orderd_book_Name and actual fist_orderd_book_Name same or not

pm.test("Test Fist order Book in the list", function () {
    pm.expect(jsonData.isbn).to.eql(pm.environment.get("fist_orderd_book_in_the_list"))
})
```   
#### Edit ISBN   
```bash
const response = pm.response.json();

// Expected status code and response status code same or not
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```
#### Delete User   

```bash
// Expected status code and response status code same or not

pm.test("Status code is 204", function () {
    pm.response.to.have.status(204);
});
```

# Create Test Suites   

### Using Newman   


  Newman is a command-line Collection Runner for Postman. It enables you to run and test a Postman Collection directly from the command line.
#### Install Command    
```bash
npm install -g newman    
```
#### Run Command    
- newman run “Path/CollectionName.json” -e Path/EnvironmentName.json
- newman run “Collection Link” -e “Path”/EnvironmentName.json    

#### Create HTML Report  
 
#### Install Command      
```bash
npm install -g newman-reporter-html
```
**or**   
```bash
npm install -g newman-reporter-htmlextra    
```
#### Run Command      
- newman run “Collection Link” -e “Path”/EnvironmentName.json -r cli,html    
**or**    
- newman run “Collection Link” -e “Path”/EnvironmentName.json -r cli,htmlextra
