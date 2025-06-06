<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Inventory</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f0f0f0;
    }
    .container {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      padding: 10px;
    }
    .card {
      background-color: #fff;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      margin: 10px;
      padding: 20px;
      width: 100%;
      max-width: 300px;
      text-align: center;
    }
    .card img {
      width: 60px;
      height: 60px;
      margin-bottom: 10px;
    }
    .card h3 {
      margin: 10px 0;
      font-size: 1.2em;
    }
    .card p {
      color: #555;
    }
    @media only screen and (min-width: 600px) {
      .card {
        width: calc(50% - 40px);
      }
    }
    @media only screen and (min-width: 900px) {
      .card {
        width: calc(33.33% - 40px);
      }
    }
  </style>
</head>
<body>

<div class="container" id="inventory-container">

</div>

<script>
async function loadItems() {
  const response = await fetch('https://script.google.com/macros/s/AKfycbwApLlI6kY719sMjzt44srstVj0I4GS2fhnS5yI6A7YUuJZWltlVJCizSXb9pl2IfKp3Q/exec');
  const items = await response.json();

  const container = document.getElementById('inventory-container');
  container.innerHTML = ''; 

  items.forEach(item => {
    if (item.quantity > 0) {  
      const card = document.createElement('div');
      card.classList.add('card');

      card.innerHTML = `
        <img src="${item.image}" alt="${item.name}" onerror="this.src='https://via.placeholder.com/60';">
        <h3>${item.name}</h3>
        <p>Omborda mavjud: ${item.quantity} </p>
      `;

      container.appendChild(card);
    }
  });
}

document.addEventListener('DOMContentLoaded', loadItems);

</script>

</body>
</html>
