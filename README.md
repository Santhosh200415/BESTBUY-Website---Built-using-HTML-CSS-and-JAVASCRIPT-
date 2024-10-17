#HTML code 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Best Buy E-Commerce</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- Header -->
  <header>
    <div class="logo">Best Buy</div>
    <nav>
      <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">Products</a></li>
        <li><a href="#">Cart</a></li>
        <li><a href="#">Contact Us</a></li>
      </ul>
    </nav>
    <div class="cart">
      <span>🛒 Cart (<span id="cart-count">0</span>)</span>
    </div>
  </header>

  <!-- Product Grid -->
  <main>
    <h1>Featured Products</h1>
    <div class="product-grid">
      <div class="product" data-id="1">
        <img src="https://via.placeholder.com/150" alt="Product 1">
        <h3>Product 1</h3>
        <p>$199.99</p>
        <button class="add-to-cart">Add to Cart</button>
      </div>
      <div class="product" data-id="2">
        <img src="https://via.placeholder.com/150" alt="Product 2">
        <h3>Product 2</h3>
        <p>$299.99</p>
        <button class="add-to-cart">Add to Cart</button>
      </div>
      <div class="product" data-id="3">
        <img src="https://via.placeholder.com/150" alt="Product 3">
        <h3>Product 3</h3>
        <p>$399.99</p>
        <button class="add-to-cart">Add to Cart</button>
      </div>
    </div>
  </main>

  <!-- Cart Modal -->
  <div id="cart-modal" class="cart-modal">
    <div class="cart-content">
      <h2>Your Cart</h2>
      <ul id="cart-items"></ul>
      <p>Total: $<span id="cart-total">0.00</span></p>
      <button id="checkout">Checkout</button>
      <button id="close-cart">Close</button>
    </div>
  </div>

  <script src="script.js"></script>
</body>
</html>
#CSS code : 
/* General styles */
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  background-color: #f4f4f4;
}

header {
  background-color: #0033a0;
  color: white;
  display: flex;
  justify-content: space-between;
  padding: 15px;
}

header .logo {
  font-size: 24px;
}

nav ul {
  list-style: none;
  display: flex;
}

nav ul li {
  margin-right: 20px;
}

nav ul li a {
  color: white;
  text-decoration: none;
}

.cart {
  cursor: pointer;
}

.product-grid {
  display: flex;
  justify-content: space-around;
  padding: 20px;
}

.product {
  background-color: white;
  padding: 20px;
  text-align: center;
  border: 1px solid #ddd;
  width: 30%;
}

.product img {
  max-width: 100%;
}

button.add-to-cart {
  background-color: #0033a0;
  color: white;
  padding: 10px;
  border: none;
  cursor: pointer;
}

button.add-to-cart:hover {
  background-color: #0056b3;
}

/* Cart Modal */
.cart-modal {
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

.cart-content {
  background-color: white;
  padding: 20px;
  text-align: center;
  width: 50%;
}

.cart-content ul {
  list-style: none;
  padding: 0;
}

.cart-content button {
  background-color: #0033a0;
  color: white;
  padding: 10px;
  border: none;
  cursor: pointer;
  margin-top: 10px;
}
#Javascript code :
// Cart array to store products
let cart = [];
let cartCount = document.getElementById('cart-count');
let cartItemsList = document.getElementById('cart-items');
let cartTotal = document.getElementById('cart-total');

// Add product to cart
const products = document.querySelectorAll('.product');
products.forEach(product => {
  product.querySelector('.add-to-cart').addEventListener('click', () => {
    let productId = product.dataset.id;
    let productName = product.querySelector('h3').textContent;
    let productPrice = parseFloat(product.querySelector('p').textContent.replace('$', ''));
    
    addToCart(productId, productName, productPrice);
  });
});

// Update cart
function addToCart(id, name, price) {
  let item = cart.find(product => product.id === id);
  if (item) {
    item.quantity++;
  } else {
    cart.push({ id, name, price, quantity: 1 });
  }
  updateCartUI();
}

// Update cart UI
function updateCartUI() {
  cartCount.textContent = cart.length;
  cartItemsList.innerHTML = '';
  let total = 0;
  
  cart.forEach(item => {
    total += item.price * item.quantity;
    cartItemsList.innerHTML += `<li>${item.name} (x${item.quantity}) - $${(item.price * item.quantity).toFixed(2)}</li>`;
  });
  
  cartTotal.textContent = total.toFixed(2);
}

// Open and close cart modal
const cartModal = document.getElementById('cart-modal');
document.querySelector('.cart').addEventListener('click', () => {
  cartModal.style.display = 'flex';
});

document.getElementById('close-cart').addEventListener('click', () => {
  cartModal.style.display = 'none';
});


