<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>سایت مانی</title> 
	<style>header {
        background-color: #333;
        color: #fff;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        padding: 10px;
    }
    
    nav ul {
        list-style: none;
        margin: 0;
        padding: 0;
    }
    
    nav li {
        display: inline-block;
        margin-right: 20px;
    }

    nav a {
        color: #fff;
        text-decoration: none;
    }
    
    #clock {
        font-size: 2em;
        font-weight: bold;
    }
    .timer-container {
        position: relative;
        width: 200px;
        height: 200px;
        margin: 50px auto;
      }

      .timer {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        transform: rotate(-90deg);
        transform-origin: center;
        border-radius: 50%;
        box-shadow: inset 0 0 50px rgba(0, 0, 0, 0.5);
        transition: stroke-dashoffset 0.1s linear;
      }

      .timer__fill {
        stroke-dasharray: 440;
        stroke-dashoffset: 0;
        stroke: #3498db;
      }

      .timer__text {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        font-size: 32px;
        font-weight: bold;
        color: #3498db;
        text-align: center;
      }

      .btn {
        display: inline-block;
        padding: 10px 20px;
        font-size: 16px;
        font-weight: bold;
        color: #fff;
        background-color: #3498db;
        border: none;
        border-radius: 5px;
        cursor: pointer;
      }

      .btn:hover {
        background-color: #2980b9;
      }
      h1 {
        color: #008080;
      }
      button {
        background-color: #008080;
        color: #ffffff;
        border: none;
        padding: 10px 20px;
        border-radius: 5px;
        cursor: pointer;
        transition: background-color 0.3s ease;
      }
      button:hover {
        background-color: #005757;
      }
      #water-count {
        font-size: 48px;
        color: #008080;
      }
      h1 {
      text-align: center;
      margin-top: 0;
    }
    .todo-list {
      list-style: none;
      padding: 0;
      margin: 0;
    }
    .todo-item {
      display: flex;
      align-items: center;
      padding: 10px;
      background-color: #fff;
      border-radius: 5px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
      margin-bottom: 10px;
    }
    .todo-item input[type=checkbox] {
      margin-right: 10px;
    }
    .todo-item .delete-btn {
      margin-left: auto;
      background-color: #ff0000;
      color: #fff;
      border: none;
      padding: 5px 10px;
      cursor: pointer;
      border-radius: 5px;
    }
    .completed {
      text-decoration: line-through;
      color: #999;
    }
    .hidden {
      display: none;
    }
    #hide-completed-btn {
      background-color: #000;
      color: #fff;
      border: none;
      padding: 5px 10px;
      cursor: pointer;
      margin-top: 20px;
      border-radius: 5px;
    }
    #hide-incomplete-btn {
      background-color: #000;
      color: #fff;
      border: none;
      padding: 5px 10px;
      cursor: pointer;
      margin-top: 20px;
      border-radius: 5px;
    }
    #add-item-form {
      display: flex;
      margin-top: 20px;
    }
    #add-item-form input[type=text] {
      flex: 1;
      padding: 5px;
      border-radius: 5px;
      border: none;
      margin-right: 10px;
    }
    #add-item-form button {
      background-color: #000;
      color: #fff;
      border: none;
      padding: 5px 10px;
      cursor: pointer;
      border-radius: 5px;
    }
      </style>
</head>
<body>
	<header>
		<nav>
			<ul>
				<li><a href="#">خانه</a></li>
				<li><a href="#">درباره ما</a></li>
				<li><a href="#" onclick="openNewPage()">بدست اوردن معدل </a></li>
			</ul>
		</nav>
		<div id="clock"></div>
	</header>
	<main>
		<h1>سلام به سایت مانی خوش امدید </h1>
	
	</main>
    <div class="timer-container">
        <svg class="timer" viewBox="0 0 100 100">
          <circle class="timer__bg" cx="50" cy="50" r="45" fill="none" stroke="#ddd" stroke-width="5"></circle>
          <circle class="timer__fill" cx="50" cy="50" r="45" fill="none" stroke-width="5"></circle>
        </svg>
        <div class="timer__text" id="timer-text"></div>
      </div>
      <div class="buttons-container">
        <form>
          <label for="minutes-input">Minutes:</label>
          <input type="number" id="minutes-input" name="minutes-input" min="1" max="60" value="10">
          <button class="btn" id="start-btn">Start</button>
          <button class="btn" id="stop-btn" disabled>Stop</button>
        </form>
      </div>
      <h1>تعداد دفعات آب خوردن </h1>
    <p>You have had <span id="water-count">0</span> لیوان های آب در روز </p>
    <button id="drink-btn">نوشیدن </button>
    <h1>To-Do List</h1>
  <ul class="todo-list">
    <li class="todo-item">
    </li>
</ul>
<button id="hide-completed-btn">Hide Completed Items</button>
<button id="hide-incomplete-btn">Hide Incomplete Items</button>
<form id="add-item-form">
  <input type="text" id="item-title" placeholder="Item Title" />
  <input type="text" id="item-description" placeholder="Item Description" />
  <button type="submit">Add Item</button>
</form>
    <script>
        // Get the list of todo items
        const todoList = document.querySelector('.todo-list');
    
        // Add event listener to listen for checkbox change events
        todoList.addEventListener('change', (event) => {
          // If the changed element is a checkbox
          if(event.target.type === 'checkbox') {
            // Get the parent li element
            const todoItem = event.target.parentElement;
    
            // Toggle the completed class on the parent li element
            todoItem.classList.toggle('completed');
          }
        });
    
        // Add event listener to listen for delete button click events
        todoList.addEventListener('click', (event) => {
          // If the clicked element is a delete button
          if (event.target.classList.contains('delete-btn')) {
            // Get the parent li element
            const todoItem = event.target.parentElement;
    
            // Remove the parent li element from the list
            todoList.removeChild(todoItem);
          }
        });
    
        // Add event listener to listen for hide completed button click events
        const hideCompletedBtn = document.getElementById('hide-completed-btn');
        hideCompletedBtn.addEventListener('click', () => {
          // Get all completed todo items
          const completedItems = document.querySelectorAll('.completed');
    
          // Toggle the hidden class on each completed todo item
          completedItems.forEach((item) => {
            item.classList.toggle('hidden');
          });
        });
    
        // Add event listener to listen for hide incomplete button click events
        const hideIncompleteBtn = document.getElementById('hide-incomplete-btn');
        hideIncompleteBtn.addEventListener('click', () => {
          // Get all incomplete todo items
          const incompleteItems = document.querySelectorAll('li:not(.completed)');
    
          // Toggle the hidden class on each incomplete todo item
          incompleteItems.forEach((item) => {
            item.classList.toggle('hidden');
          });
        });
    
        // Add event listener to listen for form submit events
        const addItemForm = document.getElementById('add-item-form');
        addItemForm.addEventListener('submit', (event) => {
          // Prevent the default form submission behavior
          event.preventDefault();
    
          // Get the values of the title and description inputs
          const title = document.getElementById('item-title').value;
          const description = document.getElementById('item-description').value;
    
          // Create a new li element
          const newTodoItem = document.createElement('li');
          newTodoItem.classList.add('todo-item');
    
          // Create a new checkbox element
          const newCheckbox = document.createElement('input');
          newCheckbox.type = 'checkbox';
          newCheckbox.id = `todo-item-${todoList.children.length + 1}`;
    
          // Create a new label element
          const newLabel = document.createElement('label');
          newLabel.htmlFor = `todo-item-${todoList.children.length + 1}`;
          newLabel.textContent = title;
    
          // Create a new button element
          const newButton = document.createElement('button');
          newButton.classList.add('delete-btn');
          newButton.textContent = 'Delete';
    
          // Append the checkbox, label, and button elements to the new li element
          newTodoItem.appendChild(newCheckbox);
          newTodoItem.appendChild(newLabel);
          newTodoItem.appendChild(newButton);
    
          // Append the new li element to the list
          todoList.appendChild(newTodoItem);
    
          // Clear the values of the title and description inputs
          document.getElementById('item-title').value = '';
          document.getElementById('item-description').value = '';
        });
      </script>
  
	<script>function updateClock() {
        let now = new Date();
        let hour = now.getHours();
        let minute = now.getMinutes();
        let second = now.getSeconds();
        let date = now.toLocaleDateString('fa-IR');
        document.getElementById('clock').innerHTML = `${hour}:${minute}:${second} - ${date}`;
    }
    setInterval(updateClock, 1000);
    function openNewPage() {
			window.open('index.html');
		}
        ///تایمر معکوس
        let minutes = 10;
      let seconds = minutes * 60;
      let timerIntervalId = null;

      const timer = document.querySelector('.timer__fill');
      const timerText = document.querySelector('#timer-text');
      const startBtn = document.querySelector('#start-btn');
      const stopBtn = document.querySelector('#stop-btn');
      const minutesInput = document.querySelector('#minutes-input');

      function updateTimer() {
        timer.setAttribute('stroke-dashoffset', calculateDashOffset());
        timerText.innerText = formatTime(seconds);
        if (seconds > 0) {
          seconds--;
        } else {
          timerText.innerText = "Time's up!";
          stopTimer();
        }
      }

      function calculateDashOffset() {
        const circumference = 2 * Math.PI * 45;
        const progress = seconds / (minutes * 60);
        return circumference * (1 - progress);
      }

      function formatTime(time) {
        const minutes = Math.floor(time / 60);
        const seconds = time % 60;
        return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
      }

      function startTimer() {
        minutes = parseInt(minutesInput.value);
        seconds = minutes * 60;
        timerIntervalId = setInterval(updateTimer, 1000);
        startBtn.disabled = true;
        stopBtn.disabled = false;
      }

      function stopTimer() {
        clearInterval(timerIntervalId);
        startBtn.disabled = false;
        stopBtn.disabled = true;
      }

      startBtn.addEventListener('click', startTimer);
      stopBtn.addEventListener('click', stopTimer);
        </script>
      
        <script>
                   ///اب خوردن 
            let waterCount = 0;
            const waterCountElement = document.getElementById('water-count');
            const drinkBtn = document.getElementById('drink-btn');
      
            function updateWaterCount() {
              waterCount++;
              waterCountElement.innerText = waterCount;
            }
      
            drinkBtn.addEventListener('click', updateWaterCount);
          </script>
	<style>.container {
	max-width: 600px;
	margin: 0 auto;
	padding: 20px;
}

h1 {
	text-align: center;
}

table {
	border-collapse: collapse;
	width: 100%;
	margin-bottom: 20px;
}

th, td {
	padding: 10px;
	text-align: center;
}

th {
	background-color: #f2f2f2;
}

.course-code {
	width: 100%;
}

.grade-input {
	width: 80px;
}

tfoot td {
	font-weight: bold;
}

#add-row-button {
	background-color: #4CAF50;
	color: white;
	padding: 10px;
	border: none;
	border-radius: 5px;
	cursor: pointer;
}</style>
</head>
<body>
	<div class="container">
		<h1>محاسبه معدل با چندین کد درس</h1>
		<table id="grades-table">
			<thead>
				<tr>
					<th>کد درس</th>
					<th>نمره</th>
				</tr>
			</thead>
			<tbody>
				<tr>
					<td><input type="text" class="course-code" required></td>
					<td><input type="number" class="grade-input" min="0" max="20" step="0.01" required></td>
				</tr>
			</tbody>
			<tfoot>
				<tr>
					<td colspan="2"><button id="add-row-button">افزودن ردیف جدید</button></td>
				</tr>
				<tr>
					<td>معدل کل:</td>
					<td id="average">-</td>
				</tr>
			</tfoot>
		</table>
	</div>
	<script>const addRowButton = document.getElementById('add-row-button');
        const averageCell = document.getElementById('average');
        
        addRowButton.addEventListener('click', function() {
            const tableBody = document.querySelector('#grades-table tbody');
            const newRow = document.createElement('tr');
            newRow.innerHTML = `
                <td><input type="text" class="course-code" required></td>
                <td><input type="number" class="grade-input" min="0" max="20" step="0.01" required></td>
            `;
            tableBody.appendChild(newRow);
        });
        
        document.addEventListener('input', function(event) {
            if (event.target.classList.contains('grade-input')) {
                updateAverage();
            }
        });
        
        function updateAverage() {
            const gradeInputs = document.querySelectorAll('.grade-input');
            let total = 0;
            let count = 0;
            for (let i = 0; i < gradeInputs.length; i++) {
                if (gradeInputs[i].value !== '') {
                    total += parseFloat(gradeInputs[i].value);
                    count++;
                }
            }
            if (count > 0) {
                const average = total / count;
                averageCell.textContent = average.toFixed(2);
            } else {
                averageCell.textContent = '-';
            }
        }</script>
</body>
</html>
