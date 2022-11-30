Hello. This is my ReadMe file for the SHU school system project.

Firstly, I will start off by apologising about this ReadMe file. This is the first time I have ever created one, and I wasn't able to get help from my colleagues on how to wite one effectively. So, I hope this is what is required. 

To help with this project, I have used Bootstrap and FontAwsome.

For this project, I have used Node.JS as this is the code I work with daily, and due to the demand from the workplace, this had been chosen.
In this file, i will explain briefly the different aspects of my code, as well as attaching this, right at the bottom of this document.

This project starts by using index.html, then I have created 2 files. Main.JS and Module.JS. As well as using a style.css sheet. 

index.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>School System</title>

    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css" integrity="sha384-xOolHFLEh07PJGoPkLv1IbcEPTNtaed2xpHsD9ESMhqIYd0nLMwNLD69Npy4HI+N" crossorigin="anonymous">
    <script src="https://kit.fontawesome.com/181e17f400.js" crossorigin="anonymous"></script>
    <link rel="stylesheet" href="./style.css">

</head>
<body>

<div class="container text-center">
    <h1 class="bg-light py-4 text-info"><i class="fas fa-school"></i> School System</h1>
</div>

<div class="d-flex justify-content-center">
    <form class="w-50">
        <input type="text" id="studentid" class="form-control" readonly placeholder="Student ID">
        <input type="text" id="studentname" class="form-control" placeholder="Student Name">
        <input type="text" id="subject" class="form-control" placeholder="Subject">
        
        
        <div class="row">
            <div class="col">
                <input type="text" id="grades" class="form-control m-0" placeholder="Grade Results">
            </div>
            <div class="col">
                <input type="date" id="dates" class="form-control m-0" placeholder="Exam Date">
            </div>
        </div>
    </form>
</div>

<!--This is the code used to create, update, delete and view the data, using buttons-->
<div class="d-flex justify-content-center">
    <button class="btn btn-success"id="btn-create">Create Student Information</button>
    <button class="btn btn-primary"id="btn-view">View Student Information</button>
    <button class="btn btn-warning"id="btn-update">Update Student Information</button>
    <button class="btn btn-danger"id="btn-delete">Delete Student Information</button>
</div>

<div class="container d-flex">
    <table class="table table-striped">
        <thead>
          <tr>
            <th scope="col">Student ID</th>
            <th scope="col">Student Name</th>
            <th scope="col">Subject</th>
            <th scope="col">Grade Results</th>
            <th scope="col">Exam Date</th>
            <th scope="col">Update</th>
            <th scope="col">Delete</th>
            
          </tr>
          
        </thead>
        <tbody id="tbody">
            
          <tr>
            <th scope="row">1</th>
            <td>John Doe</td>
            <td>History</td>
            <td>A*</td>
            <td>01/08/2021</td>
            <td><i class="fas fa-edit btnupdate"></i></td>
            <td><i class="fas fa-trash-alt btndelete"></i></td>
            

          </tr>
          <tr>
            <th scope="row">2</th>
            <td>Jacob Test</td>
            <td>Science</td>
            <td>A</td>
            <td>01/03/2021</td>
            <td><i class="fas fa-edit btnupdate"></i></td>
            <td><i class="fas fa-trash-alt btndelete"></i></td>
          </tr>
          <tr>
            <th scope="row">3</th>
            <td>Joe Bloggs</td>
            <td>Maths</td>
            <td>C</td>
            <td>01/01/2021</td>
            <td><i class="fas fa-edit btnupdate"></i></td>
            <td><i class="fas fa-trash-alt btndelete"></i></td>
          </tr>
        
          
        </tbody>
      </table>
      <div></div>
</div>



   
    <script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.14.7/dist/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@4.3.1/dist/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"
></script>

<!--Dexie API-->

<script src="https://cdnjs.cloudflare.com/ajax/libs/dexie/2.0.4/dexie.min.js" integrity="sha512-OPW5ku+bS0iQpI37fP9JjFoo2o5YUuxDOcA4UyIG9GpTHpY/Yat+rnJGTjynyeQzAQclbYWja9d2Rs8NbzhhOQ==" crossorigin="anonymous" referrerpolicy="no-referrer"
></script>

<!--Bespoke javascript, Main.JS-->

<script src="../js/main.js" type="module"></script>

</body>
</html>


Main.js

import schooldb,{
    bulkcreate, 
    getData,
    createEle
} from './module.js'


let db = schooldb("schooldb",{
    school: `++studentid, studentname, subject, grades, dates`
});

//input tags
const studentid = document.getElementById("studentid");
const studentname = document.getElementById("studentname");
const subject = document.getElementById("subject");
const grades = document.getElementById("grades");
const dates = document.getElementById("dates");

//buttons
const btncreate = document.getElementById("btn-create");
const btnview = document.getElementById("btn-view");
const btnupdate = document.getElementById("btn-update");
const btndelete = document.getElementById("btn-delete");






//inserting values based on the click of the create button

btncreate.onclick =(event)=>{
    bulkcreate(db.school,{
        studentname : studentname.value,
        subject : subject.value,
        grades : grades.value,
        dates : dates.value
    })
    
    /*studentname.value = "";
    subject.value = "";
    grades.value ="";
    dates.value ="";
    */
   studentname.value = subject.value = grades.value = dates.value ="";
   getData(db.school,(data)=>{
    studentid.value=data.studentid +1||1;
   })
}

//Create Event on the view button
btnview.onclick = table;

function table(){
    const tbody=document.getElementById("tbody");
    getData(db.school,(data)=>{
        if(data){
            createEle("tr", tbody, tr=>{

               for(const value in data){
                createEle("td",tr,td=>{
                    td.textContent = data[value];
                })

               }
            })
        }
    })
}

    
    
Module.js


const schooldb = (dbname,table) =>{
    //creation of the database

    const db = new Dexie(dbname)
    db.version(1).stores(table);
    db.open();

    /*
const db = new Dexie('myDb');
db.version(1).stores({
    friends: `name,age`
})
*/
return db;


}

// insert function
const bulkcreate = (dbtable, data)=>{
    let flag = empty(data);
    if (flag){
        dbtable.bulkAdd([data]);
        console.log("Data Inserted Sucessfully");
    }else{
        console.log("Please Provide Data");    
    }
    return flag;
    
}

//check textbox validation
const empty = object =>{
    let flag = false;

    for(const value in object){
        if(object[value]!=""&& object.hasOwnProperty(value)){
            flag = true;
        }else{
            flag = false;
        }    
    }    
    return flag;
}

//Get data from the db
const getData =(dbtable, fn)=>{
    let index = 0;
    let obj = {};

    
}

// Sorting data
const Sortobj = sortobj=>{
    let obj = {};
    obj = {
        studentid : sortobj.studentid,
        studentname : sortobj.studentname,
        subject : sortobj.subject,
        grades : sortobj.grades,
        dates : sortobj.dates
    }
    return obj;
}

//creating a dynamic element, to save time.
const createEle=(tagname,appendTo,fn)=>{
    const element = document.createElement(tagname);
    if(appendTo) appendTo.appendChild(element);
    if(fn)fn(element);

}

export default schooldb;
export{
    bulkcreate,
    getData,
    createEle

}


Style.CSS


.d-flex input{
    margin:.9em 0em;
}

d-flex button{
    margin:1.4em.5em;
    padding:0.3em 2.4em;
}

table .btnupdate{
    color: orange;
    cursor: pointer;
}

table .btndelete{
    color: crimson;
    cursor: pointer;
}
    
    






