
<html>
<head>
  <title>Menu Calculator</title>
    <style>
    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 250vh;
      text-align: center;
    }
	.total-box {
		display: flex;
		justify-content: center; /* Center horizontally */
		align-items: center; /* Center vertically */
		margin-top: 20px;
	}}
	
	 .calculate-button {
      width: 150px; /* Adjust the desired width */
      height: 50px; /* Adjust the desired height */
    }
	
	.submit-button {
      width: 150px; /* Adjust the desired width */
      height: 40px; /* Adjust the desired height */
    }
	
	.reset-button {
      width: 150px; /* Adjust the desired width */
      height: 30px; /* Adjust the desired height */
    }
    
    h1 {
      margin-bottom: 20px;
    }
    
    h2 {
      margin-top: 20px;
    }
	
	h3 {
      border: 1px solid black; /* Adjust the border style as needed */
      padding: 5px; /* Add padding to create space around the heading */
    }
    
    .menu-items {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      gap: 10px;
      margin-bottom: 10px;
    }
    
    .menu-items div {
      display: flex;
      align-items: center;
    }
    
    .total-box {
      display: flex;
      justify-content: flex-end;
      align-self: Center;
      margin-top: 20px;
    }
    
    .button-container {
      display: flex;
      gap: 10px;
      margin-top: 20px;
    }
	
	.menu-items div img {
      width: 50px; /* Adjust the desired width */
      height: 50px; /* Adjust the desired height */
      margin-left: 10px; /* Add margin as per your preference */
    }
    {
    button {
      margin-top: 20px;
	}}}}}}
  </style>
  <script>
    function calculateTotal() {
    var total = 0;
    var checkboxes = document.querySelectorAll('input[type="checkbox"]:checked');

    checkboxes.forEach(function(checkbox) {
      var quantityInput = checkbox.parentNode.querySelector('input[type="number"]');
      var quantity = parseInt(quantityInput.value);
      var price = parseFloat(checkbox.value);

      if (checkbox.value === '-25%') {
        var itemPrice = total * 0.25;
        total -= itemPrice;
      } else if (checkbox.value === '-30%') {
        var itemPrice = total * 0.3;
        total -= itemPrice;
      } else if (checkbox.value === '-50%') {
        var itemPrice = total * 0.5;
        total -= itemPrice;
      } else {
        total += price * quantity;
      }
    });

    var totalElement = document.getElementById('total');
    totalElement.textContent = total.toFixed(2);

    var discountTotalElement = document.getElementById('discount-total');
    var discount = total * 0.10;
    discountTotalElement.textContent = discount.toFixed(2);
  }


    
    function submitOrder() {
    var name = document.getElementById('name').value;
    if (name.trim() === '') {
      alert('Please enter a name.');
      return;
    }

    // Collect selected items and their quantities
    var selectedItems = [];
    var checkboxes = document.querySelectorAll('input[type="checkbox"]:checked');
    checkboxes.forEach(function (checkbox) {
      var itemName = checkbox.nextElementSibling.textContent;
      var quantityInput = checkbox.parentNode.querySelector('input[type="number"]');
      var quantity = parseInt(quantityInput.value);
      var price = parseFloat(checkbox.value);
      selectedItems.push({ name: itemName, quantity: quantity, price: price });
    });

    var total = 0;
    var discountTotal = 0;

    selectedItems.forEach(function (item) {
      if (item.price < 0) {
        var discountPercentage = Math.abs(item.price);
        var itemDiscount = total * (discountPercentage / 100);
        discountTotal += itemDiscount;
      } else {
        total += item.price * item.quantity;
      }
    });

    var commission = (total * 0.10).toFixed(2);
    var totalWithDiscount = total - discountTotal;

    alert('Order submitted!');

    var discordWebhookURL = 'https://discordapp.com/api/webhooks/1169867134982180864/Q3tZ3QVIQ_n2ttXcMaAGzvz31AxqquH3x6sYJ1J1QnOW4U-sZpk8xe_uAF6y_vS68rth';

    var xhr = new XMLHttpRequest();
    xhr.open('POST', discordWebhookURL, true);
    xhr.setRequestHeader('Content-Type', 'application/json');

    var message = {
      content: 'New order!',
      embeds: [{
        title: 'Order Details',
        fields: [
          {
            name: 'Name',
            value: name,
            inline: true
          },
          {
            name: 'Total',
            value: '$' + totalWithDiscount.toFixed(2),
            inline: true
          },
          {
            name: 'Discount Total',
            value: '$' + discountTotal.toFixed(2),
            inline: true
          },
          {
            name: 'Commission (10%)',
            value: '$' + commission,
            inline: true
          },
          {
            name: 'Ordered Items',
            value: selectedItems.map(item => `${item.name} x${item.quantity} - $${(item.price * item.quantity).toFixed(2)}`).join('\n'),
            inline: false
          }
        ]
      }]
    };

    xhr.send(JSON.stringify(message));
  }

function resetCalculator() {
  var checkboxes = document.querySelectorAll('input[type="checkbox"]');
  var quantityInputs = document.querySelectorAll('input[type="number"]');
  
  checkboxes.forEach(function(checkbox) {
    checkbox.checked = false;
  });
  
  quantityInputs.forEach(function(quantityInput) {
    quantityInput.value = 1;
  });
  
  document.getElementById('total').textContent = '0.00';
}
	function submitAndReset() {
	submitOrder();
	resetCalculator();
}

  </script>
</head>
<body>
	
<div style="margin-bottom: 25px;"></div>
 
<body style="background-color:gray;">
	<img src="pawnshop.png" alt="Company Logo!">
  <h1>Menu Calculator</h1>
  
  <h2>Menu Items</h2>

  <div style="margin-bottom: 10px;"></div>
  
  <h3>Electronics</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="uwueats" value="275$">
    <label for="Velmachoice">Microwave - 275$</label>
    <input type="number" value="1" min="1">
  </div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="880$">
    <label for="Davechoice">PC - 880$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="1000$">
    <label for="Davechoice">TV- 1000$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="200$">
    <label for="Davechoice">Boombox - 200$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="2000$">
    <label for="Davechoice">Flatscreen - 2000$</label>
    <input type="number" value="1" min="1">
  </div>

    <h3>Jewlery</h3>

  <div style="margin-bottom: 10px;"></div>
  
  <div>
    <input type="checkbox" id="Davechoice" value="325$">
    <label for="Davechoice">Rolex - 325$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="120$">
    <label for="Davechoice">Ring - 120$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="120$">
    <label for="Davechoice">Gold Earrings - 120$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="160$">
    <label for="Davechoice">Gold Chains - 160$</label>
    <input type="number" value="1" min="1">
  </div>

    <h3>Valuable Goods</h3>

  <div style="margin-bottom: 10px;"></div>

   <div>
    <input type="checkbox" id="Davechoice" value="60$">
    <label for="Davechoice">Gold Coins - 60$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="280$">
    <label for="Davechoice">Golf Club Set - 280$</label>
    <input type="number" value="1" min="1">
  </div>
    
  <div>
    <input type="checkbox" id="Davechoice" value="2000$">
    <label for="Davechoice">Painting - 2000$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="1400$">
    <label for="Davechoice">Valuable Good - 1400$</label>
    <input type="number" value="1" min="1">
  </div>

      <h3>Bars</h3>

  <div style="margin-bottom: 10px;"></div>

  <div>
    <input type="checkbox" id="Davechoice" value="320$">
    <label for="Davechoice">Gold Bars - 320$</label>
    <input type="number" value="1" min="1">
  </div>

  <div>
    <input type="checkbox" id="Davechoice" value="130$">
    <label for="Davechoice">Silver Bars - 130$</label>
    <input type="number" value="1" min="1">
  </div>

  <div style="margin-bottom: 25px;"></div>

<div>
    <label for="name">Cashier's Name:</label>
    <input type="text" id="name">
  </div>
  

<div style="margin-bottom: 25px;"></div>
 
<div class="total-box">
  <span>Total: $</span>
  <span id="total">0.00</span>
</div>

<div class="total-box">
  <span>Commision (10%): $</span>
  <span id="discount-total">0.00</span>
</div>




 
  
  
  <div style="margin-bottom: 45px;"></div>
  

  <button class="calculate-button" onclick="calculateTotal()">Calculate Total</button>
  <button class="submit-button" onclick="submitAndReset()">Submit Order</button>
  <button class="reset-button" onclick="resetCalculator()">Reset</button>

 
  
  
  <div style="margin-bottom: 10px;"></div>
