<html>
<head>
	<title>محاسبه معدل با چندین کد درس</title>
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
