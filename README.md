#Problem statement:
Employee - ID - Name 
Department - ID - Name 
1) 1 employee can be related to only 1 dept 
2) 1 dept can have multiple employees Expectation - Create an application which will 
satisfy following expectations - 1) CRUD operations on Emplyeee and Department through Rest API

#Springboot application with REST API, h2 database , jpa, lombok ,swagger2 UI, javax-validation,Hibernate ORM

#What I have done
1.created springboot application and added required dependencies.
2.Created Employee,Department entities.
3.created controller,service implemetation and repositories for the entities.
4.created dto's for returning data in rest call.
5.handled and throwed exceptions whenever required and handled null retrievals from database.
which might cause null pointer exceptions.
6.used h2 in-memory database.

## How to run the application :

1. download the zip file from the github link given
2. Springboot provides embedded tomcat service by default.
3. unzip and run the application in any IDE(eg:IntelliJ)
4. http://localhost:8080/swagger-ui.html#/   paste this link in web browser 
5. A swagger UI will be opened and we can test here performance of crud operations.
6. data will be vanished from h2 once we re-run the application.

##Testing ::

1.Click on department controller , you can find all crud operations of department class
2.Click on employee controller , you can find all crud operations of employee class

##Steps:
#Department
1.Add department (id:1, name : (any string))
2.update department
3.delete department(can not perform if dept id is in use by employee class)
4.get department details by dept id
5.get all departments information

#Employee
1.Add Employee( id, name:(any string), dept id) if dept id not present already will throw error.
2.update employee (name or dept id)
3.delete employee( input emp id)
4.get emp details(input emp id)
5.get all emp details.

### Sample outputs:::

# get all employee details
[
  {
    "id": 1,
    "empName": "ammu",
    "department": {
      "id": 1,
      "deptName": "cse"
    }
  },
  {
    "id": 2,
    "empName": "krishna",
    "department": {
      "id": 1,
      "deptName": "cse"
    }
  },
  {
    "id": 3,
    "empName": "quest",
    "department": {
      "id": 2,
      "deptName": "ece"
    }
  }
]

# get all departments
[
  {
    "deptName": "cse",
    "deptId": 1
  },
  {
    "deptName": "ece",
    "deptId": 2
  }
]

# delete department (if dept id is used in employee table)
JdbcSQLIntegrityConstraintViolationException: Referential integrity constraint violation: "FKBEJTWVG9BXUS2MFFSM3SWJ3U9: PUBLIC.EMPLOYEE FOREIGN KEY(DEPARTMENT_ID) REFERENCES PUBLIC.DEPARTMENT(ID) (1)"; SQL statement:
delete from department where id=? [23503-200]

#update department
curl -X PUT "http://localhost:8080/department/update_department" -H "accept: application/json" -H "Content-Type: application/json" -d "{ \"deptName\": \"ece\", \"id\": 1}"
{
  "deptName": "ece",
  "id": 1
}

#create department
input:
{
  "deptName": "cse",
  "id": sri
}
response:
{
  "timestamp": "2020-12-01T20:09:03.749+00:00",
  "status": 400,
  "error": "Bad Request",
  "message": "",
  "path": "/department/create_department"
}

