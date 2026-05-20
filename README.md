# thebestcars
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AutoStock Miami</title>

  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background: #f5f5f5;
    }

    header {
      background: #111;
      color: white;
      padding: 20px;
      text-align: center;
    }

    .container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 15px;
      padding: 15px;
    }

    .car {
      background: white;
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }

    .car img {
      width: 100%;
      height: 160px;
      object-fit: cover;
    }

    .car-info {
      padding: 10px;
    }

    .price {
      color: green;
      font-weight: bold;
      font-size: 18px;
    }

    .btn {
      display: block;
      text-align: center;
      margin-top: 10px;
      padding: 10px;
      background: #25D366;
      color: white;
      text-decoration: none;
      border-radius: 8px;
    }

    .btn:hover {
      background: #1ebe5d;
    }
  </style>
</head>

<body>

<header>
  <h1>🚗 AutoStock Miami</h1>
  <p>Carros disponibles en inventario</p>
</header>

<div class="container">

  <div class="car">
    <img src="https://via.placeholder.com/400x200" alt="carro">
    <div class="car-info">
      <h3>Honda Civic 2020</h3>
      <p>Millas: 55,000</p>
      <p class="price">$13,000</p>
      <a class="btn" href="https://wa.me/13050000000">Contactar</a>
    </div>
  </div>

  <div class="car">
    <img src="https://via.placeholder.com/400x200" alt="carro">
    <div class="car-info">
      <h3>Toyota Corolla 2018</h3>
      <p>Millas: 80,000</p>
      <p class="price">$9,500</p>
      <a class="btn" href="https://wa.me/13050000000">Contactar</a>
    </div>
  </div>

</div>

</body>
</html>