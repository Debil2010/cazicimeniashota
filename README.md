<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>Казик имени Ашота</title>
	<style> 
		body{
		font-family: 'Arial', sans-serif;
		margin: 0;
		color: white;
		text-align: center;
		padding: 20px;
		height: 100vh;
		background: linear-gradient(135deg, #2c3e50, #3498db);
		box-siding: border-box;
		}
		.balance{
			font-size: 24px;
			margin: 20px 0;
			text-shadow: 2px 2px 1px #000;
		}
		#bet{
			width: 100px;
			padding: 8px;
			font-size: 16px;
			border-radius: 5px;
			margin: 0 10px;
		}
		.slot{
			width: 100px;
			height: 100px;
			border-radius: 10px;
			background-color: #fff;
			box-shadow: 4px 4px 8px #000;
			overflow: hidden;
		}
		.slot img{
			width: 100%;
			helght: 100%;
		}
		.drum{
			display: flex;
			justify-content: center;
			gap: 20px;
			padding: 40px 0;
		}
		button{
		    background-color: #e74c3c;
		    color: white;
		    border: none;
		    padding: 15px 30px;
		    font-size: 18px;
		    border-radius: 25px;
		    cursor: pointer;
		    text-transform: uppercase;
		    letter-spacing: 2px;
		}

		button:hover {
		    background: #c0392b;
		    transform: scale(1.05);
		}

		button:disabled {
		    background-color: #7f8c8d;
		    cursor: not-allowed;
		}     
	</style>
</head>
<body>
	<div class="balance">
		Баланс: <span id="balance">450 ₼</span>
	</div>
	<div class="bet-class">
		Ставка: <input type="number" class="bet" id="bet" value="100" min="1" onchange="changeBet(0)">
			<button onclick="changeBet(100)">+100</button>
			<button onclick="changeBet(-100)">-100</button>
	</div>
	<div class="drum">
		<div class="slot" id="slot1"></div>
		<div class="slot" id="slot2"></div>
		<div class="slot" id="slot3"></div>
	</div>
	<button id="start" onclick="startGame()">Крути!</button>
	<script>
		function rand(min, max){
			return Math.floor(Math.random() * (max - min) + min);

		}

		function startGame(){
			let num1 = rand(1, 7);
			let num2 = rand(1, 7);
			let num3 = rand(1, 7);
			document.getElementById('slot1').innerHTML = '<img src="b'+num1+'.png">';
			document.getElementById('slot2').innerHTML = '<img src="b'+num2+'.png">';
			document.getElementById('slot3').innerHTML = '<img src="b'+num3+'.png">';		
			let balance = document.getElementById('balance').innerHTML;
			balance = parseInt(balance)
			let bet = document.getElementById('bet').value;
			bet = parseInt(bet)
			if(num1 == num2 && num2 == num3){
				balance = balance + Math.floor( bet * 3);
			}else if(num1 == num2 || num2 == num3 || num3 == num1){
				balance = balance + Math.floor( bet * 1.5);
			}else{
				balance = balance - bet
			}
			if(balance < 0 || balance == 0){
				alert('Поздравляем! Вы банкрот! Приходите ещё!')
				document.getElementById('start').setAttribute('disabled', 'disabled')
			}
			document.getElementById('balance').innerHTML = balance;
		}

		function changeBet(count) {
	    let betInput = document.getElementById('bet');
	    let currentBet = parseInt(betInput.value);
	    let newBet = currentBet + count;
	    if (newBet >= 1) {
	        betInput.value = newBet;
	    }
		}




	</script>
</body>
</html>
