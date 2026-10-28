# study-planner
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Study Planner</title>

    <style>
        body{
            font-family: Arial, sans-serif;
            background:#f4f6f9;
            margin:0;
            padding:20px;
        }

        .container{
            max-width:800px;
            margin:auto;
            background:white;
            padding:20px;
            border-radius:12px;
            box-shadow:0 0 10px rgba(0,0,0,0.1);
        }

        h1{
            text-align:center;
            color:#2563eb;
        }

        input,button{
            padding:10px;
            margin:5px;
        }

        input{
            width:30%;
        }

        button{
            background:#2563eb;
            color:white;
            border:none;
            border-radius:5px;
            cursor:pointer;
        }

        button:hover{
            background:#1d4ed8;
        }

        table{
            width:100%;
            border-collapse:collapse;
            margin-top:20px;
        }

        th,td{
            border:1px solid #ddd;
            padding:10px;
            text-align:center;
        }

        th{
            background:#2563eb;
            color:white;
        }

        .delete{
            background:red;
        }
    </style>
</head>

<body>

<div class="container">

    <h1>📚 Student Study Planner</h1>

    <input type="text" id="subject" placeholder="Subject">
    <input type="date" id="date">
    <input type="text" id="task" placeholder="Task">

    <button onclick="addTask()">Add Task</button>

    <table>
        <thead>
        <tr>
            <th>Subject</th>
            <th>Date</th>
            <th>Task</th>
            <th>Action</th>
        </tr>
        </thead>

        <tbody id="taskList"></tbody>

    </table>

</div>

<script>

    let tasks = JSON.parse(localStorage.getItem("tasks")) || [];

    function saveTasks(){
        localStorage.setItem("tasks", JSON.stringify(tasks));
    }

    function renderTasks(){

        let table = document.getElementById("taskList");
        table.innerHTML="";

        tasks.forEach((task,index)=>{

            table.innerHTML += `
        <tr>
            <td>${task.subject}</td>
            <td>${task.date}</td>
            <td>${task.task}</td>
            <td>
                <button class="delete" onclick="deleteTask(${index})">
                Delete
                </button>
            </td>
        </tr>
        `;
        });
    }

    function addTask(){

        let subject = document.getElementById("subject").value;
        let date = document.getElementById("date").value;
        let task = document.getElementById("task").value;

        if(subject==="" || date==="" || task===""){
            alert("Please fill all fields");
            return;
        }

        tasks.push({
            subject:subject,
            date:date,
            task:task
        });

        saveTasks();
        renderTasks();

        document.getElementById("subject").value="";
        document.getElementById("date").value="";
        document.getElementById("task").value="";
    }

    function deleteTask(index){
        tasks.splice(index,1);
        saveTasks();
        renderTasks();
    }

    renderTasks();

</script>

</body>
</html>
