<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Task Board</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .board {
            display: flex;
            gap: 1rem;
            margin: 20px;
        }

        .column {
            background-color: #fff;
            border: 1px solid #ddd;
            border-radius: 5px;
            width: 200px;
            padding: 10px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }

        .column h3 {
            margin: 0;
            padding: 10px;
            text-align: center;
            background-color: #f7f7f7;
            border-bottom: 1px solid #ddd;
            border-radius: 5px 5px 0 0;
        }

        .task {
            padding: 10px;
            margin: 10px 0;
            background-color: #e9f5ff;
            border: 1px solid #cce4ff;
            border-radius: 5px;
        }

        .add-task {
            text-align: center;
            margin-top: 10px;
        }

        .add-task button {
            padding: 5px 10px;
            background-color: #4caf50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .add-task button:hover {
            background-color: #45a049;
        }

        /* Modal styles */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            width: 300px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }

        .modal-content h3 {
            margin-top: 0;
        }

        .modal-content label {
            display: block;
            margin: 10px 0 5px;
        }

        .modal-content input,
        .modal-content select {
            width: 100%;
            padding: 8px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }

        .modal-content button {
            padding: 10px 20px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        .modal-content button:hover {
            background-color: #0056b3;
        }

        .modal-close {
            display: block;
            text-align: right;
            margin-bottom: 10px;
            cursor: pointer;
            font-weight: bold;
            color: #333;
        }
    </style>
</head>
<body>
    <div class="board">
        <div class="column" data-status="todo">
            <h3>To Do</h3>
            <div class="tasks"></div>
            <div class="add-task">
                <button onclick="openModal('todo')">+ Add new</button>
            </div>
        </div>
        <div class="column" data-status="inprogress">
            <h3>In Progress</h3>
            <div class="tasks"></div>
            <div class="add-task">
                <button onclick="openModal('inprogress')">+ Add new</button>
            </div>
        </div>
        <div class="column" data-status="inreview">
            <h3>In Review</h3>
            <div class="tasks"></div>
            <div class="add-task">
                <button onclick="openModal('inreview')">+ Add new</button>
            </div>
        </div>
        <div class="column" data-status="completed">
            <h3>Completed</h3>
            <div class="tasks"></div>
            <div class="add-task">
                <button onclick="openModal('completed')">+ Add new</button>
            </div>
        </div>
    </div>

    <!-- Modal for adding tasks -->
    <div class="modal" id="taskModal">
        <div class="modal-content">
            <span class="modal-close" onclick="closeModal()">×</span>
            <h3>Add new task</h3>
            <label for="taskName">Name of the Task</label>
            <input type="text" id="taskName" placeholder="Enter task name">

            <label for="startDate">Start Date</label>
            <input type="date" id="startDate">

            <label for="deadline">Deadline</label>
            <input type="date" id="deadline">

            <label for="status">Status</label>
            <select id="status">
                <option value="todo">To Do</option>
                <option value="inprogress">In Progress</option>
                <option value="inreview">In Review</option>
                <option value="completed">Completed</option>
            </select>

            <button onclick="addTask()">Add</button>
        </div>
    </div>

    <script>
        let currentStatus = '';

        function openModal(status) {
            currentStatus = status;
            document.getElementById("taskModal").style.display = "flex";
        }

        function closeModal() {
            document.getElementById("taskModal").style.display = "none";
        }

        function addTask() {
            const taskName = document.getElementById("taskName").value;
            const startDate = document.getElementById("startDate").value;
            const deadline = document.getElementById("deadline").value;
            const status = document.getElementById("status").value || currentStatus;

            if (!taskName || !startDate || !deadline) {
                alert("Please fill all fields");
                return;
            }

            const task = document.createElement("div");
            task.className = "task";
            task.innerHTML = `
                <strong>${taskName}</strong><br>
                Start: ${startDate}<br>
                Deadline: ${deadline}
            `;

            const column = document.querySelector(`[data-status="${status}"] .tasks`);
            column.appendChild(task);

            closeModal();
        }
    </script>
</body>
</html>
