<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Morse Code Converter</title>
	<style>
		body {
			background-color: #f0f0f0;
			font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
			font-size: 16px;
			margin: 0;
			padding: 0;
			display: grid;
			grid-template-columns: 1fr;
			grid-template-rows: auto;
			grid-template-areas:
				"header"
				"form";
		}

		h1 {
			color: #333;
			font-size: 36px;
			margin: 20px 0;
			text-align: center;
			text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
			grid-area: header;
		}

		p {
			color: #333;
			font-size: 18px;
			margin: 20px 0;
			text-align: center;
			grid-area: form-text;
		}

		form {
			display: grid;
			grid-template-columns: 1fr;
			grid-template-rows: auto auto 1fr auto;
			grid-template-areas:
				"input"
				"output"
				"button";
			grid-area: form;
			justify-self: center;
			align-self: center;
			max-width: 600px;
			padding: 20px;
			background-color: #fff;
			border-radius: 4px;
			box-shadow: 0 2px 4px rgba(0,0,0,0.2);
		}

		@media only screen and (min-width: 600px) {
			body {
				grid-template-columns: 1fr 1fr;
				grid-template-rows: auto;
				grid-template-areas:
					"header header"
					"form form";
			}

			form {
				justify-self: start;
				align-self: start;
			}
		}

		label {
			display: block;
			font-size: 18px;
			margin-bottom: 10px;
		}

		textarea {
			border: 2px solid #ccc;
			border-radius: 4px;
			font-size: 18px;
			margin-bottom: 20px;
			padding: 10px;
			resize: none;
			width: 100%;
		}

		button {
			background-color: #333;
			border: none;
			border-radius: 4px;
			color: #fff;
			cursor: pointer;
			font-size: 18px;
			padding: 10px 20px;
			transition: background-color 0.3s ease;
			grid-area: button;
			align-self: end;
			justify-self: end;
		}

		button:hover {
			background-color: #555;
		}
	</style>
	<script>
		// تعریف یک شیء که حروف الفبا و کدهای مورس مربوط به آن‌ها را در خود ذخیره می‌کند
		const MorseCode = {
			"A": ".-", 
			"B": "-...", 
			"C": "-.-.", 
			"D": "-..", 
			"E": ".", 
			"F": "..-.", 
			"G": "--.", 
			"H": "....", 
			"I": "..", 
			"J": ".---", 
			"K": "-.-", 
			"L": ".-..", 
			"M": "--", 
			"N": "-.", 
			"O": "---", 
			"P": ".--.", 
			"Q": "--.-", 
			"R": ".-.", 
			"S": "...", 
			"T": "-", 
			"U": "..-", 
			"V": "...-", 
			"W": ".--", 
			"X": "-..-", 
			"Y": "-.--", 
			"Z": "--..", 
			"0": "-----", 
			"1": ".----", 
			"2": "..---", 
			"3": "...--", 
			"4": "....-", 
			"5": ".....", 
			"6": "-....", 
			"7": "--...", 
			"8": "---..", 
			"9": "----.", 
			".": ".-.-.-",
			",": "--..--",
			"?": "..--..",
			"'": ".----.",
			"!": "-.-.--",
			"/": "-..-.",
			"(": "-.--.",
			")": "-.--.-",
			"&": ".-...",
			":": "---...",
			";": "-.-.-.",
			"=": "-...-",
			"+": ".-.-.",
			"-": "-....-",
			"_": "..--.-",
			'"': ".-..-.",
			"$": "...-..-",
			"@": ".--.-."
		};

		// تابع تبدیل متن به کد مورس
		function textToMorse(text) {
			// تبدیل حروف متن به حروف بزرگ
			text = text.toUpperCase();

			// تبدیل هر حرف به کد مورس مربوط به آن
			let morseCode = "";
			for (let i = 0; i < text.length; i++) {
				let char = text[i];
				if (MorseCode[char]) {
					// اگر کد مورس برای این حرف وجود داشته باشد، به متن کد مورس اضافه می‌شود
					morseCode += MorseCode[char] + " ";
				} else {
					// در غیر این صورت، یک فاصله اضافه می‌شود
					morseCode += " ";
				}
			}

			return morseCode.trim();
		}

		// تابع تبدیل کد مورس به متن
		function morseToText(morseCode) {
			// تبدیل کد مورس به آرایه از کدهای هر حرف
			let codeArray = morseCode.trim().split(" ");

			// تبدیل هر کد مورس به حرف مربوطه
			let text = "";
			for (let i = 0; i < codeArray.length; i++) {
				let code = codeArray[i];
				// جستجوی حرف مربوط به این کد مورس
				for (let char in MorseCode) {
					if (MorseCode[char] == code) {
						text += char;
						break;
					}
				}
			}

			return text;
		}

		// تابعی برای پردازش فرم
		function processForm() {
			// دریافت مقدار فیلد متن
			let text = document.getElementById("text").value;

			// تبدیل متن به کد مورس
			let morseCode = textToMorse(text);

			// نمایش متن تبدیل شده در فیلد مخصوص آن
			document.getElementById("morse-code").value = morseCode;
		}
	</script>
</head>
<body>
	<h1>Morse Code Converter</h1>
	<form>
		<label for="text">Enter some text or Morse code below:</label>
		<textarea id="text" placeholder="Enter text or Morse code..."></textarea>
		<label for="morse-code">Morse code:</label>
		<textarea id="morse-code" placeholder="Morse code will appear here..." readonly></textarea>
		<button type="button" onclick="processForm()">Convert</button>
	</form>
</body>
</html>
