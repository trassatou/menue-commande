<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Commande - Menus Gourmands</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      background: #f9f9f9;
    }
    h1 {
      text-align: center;
    }
    .menu {
      background: #fff;
      padding: 15px;
      border-radius: 10px;
      margin-bottom: 20px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }
    label, select, input, textarea {
      display: block;
      width: 100%;
      margin-top: 10px;
      padding: 8px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    button {
      margin-top: 20px;
      padding: 10px;
      background-color: #2c3e50;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .total {
      font-weight: bold;
      font-size: 18px;
      margin-top: 15px;
    }
    img {
      width: 100%;
      max-height: 200px;
      object-fit: cover;
      border-radius: 10px;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <h1>Commande ton menu 🍴</h1>

  <div class="menu">
    <label for="menu">Choisis ton menu :</label>
    <select id="menu" onchange="updateTotal(); updateImage();">
      <option value="">-- Sélectionne --</option>
      <option value="6000" data-name="Menu Fondant">Menu Fondant - 6 000 FCFA</option>
      <option value="6000" data-name="Menu Croustillant">Menu Croustillant - 6 000 FCFA</option>
      <option value="5500" data-name="Menu Croquant">Menu Croquant - 5 500 FCFA</option>
      <option value="6500" data-name="Menu Jambalaya">Menu Jambalaya - 6 500 FCFA</option>
      <option value="9000" data-name="Menu Duo Snack">Menu Duo Snack - 9 000 FCFA</option>
      <option value="10000" data-name="Menu Fusion">Menu Fusion - 10 000 FCFA</option>
      <option value="15000" data-name="Menu Mix Gourmand">Menu Mix Gourmand - 15 000 FCFA</option>
    </select>

    <img id="menuImage" src="" alt="Image du menu sélectionné" style="display:none;">

    <label for="dessert">Choix du dessert :</label>
    <select id="dessert" onchange="updateTotal()">
      <option value="0">Brownie (inclus)</option>
      <option value="500">Tiramisu (+500 FCFA)</option>
    </select>

    <div class="total">Total : <span id="total">0</span> FCFA</div>
  </div>

  <div class="menu">
    <label>Ton nom :</label>
    <input type="text" id="nom">

    <label>Numéro de téléphone :</label>
    <input type="text" id="tel">

    <label>Adresse de livraison :</label>
    <textarea id="adresse" rows="3"></textarea>

    <button onclick="envoyerCommande()">Envoyer la commande 📩</button>
    <button onclick="envoyerWhatsapp()">Commander sur WhatsApp 💬</button>
  </div>

  <script>
    const imageMap = {
      "Menu Fondant": "https://source.unsplash.com/800x600/?lasagna",
      "Menu Croustillant": "https://source.unsplash.com/800x600/?samosa",
      "Menu Croquant": "https://source.unsplash.com/800x600/?spring-rolls",
      "Menu Jambalaya": "https://source.unsplash.com/800x600/?jambalaya",
      "Menu Duo Snack": "https://source.unsplash.com/800x600/?snack",
      "Menu Fusion": "https://source.unsplash.com/800x600/?fusion-food",
      "Menu Mix Gourmand": "https://source.unsplash.com/800x600/?gourmet"
    };

    function updateTotal() {
      const menu = parseInt(document.getElementById("menu").value) || 0;
      const dessert = parseInt(document.getElementById("dessert").value) || 0;
      const total = menu + dessert;
      document.getElementById("total").textContent = total;
    }

    function updateImage() {
      const select = document.getElementById("menu");
      const selectedOption = select.options[select.selectedIndex];
      const menuName = selectedOption.getAttribute("data-name") || "";
      const img = document.getElementById("menuImage");
      if (imageMap[menuName]) {
        img.src = imageMap[menuName];
        img.style.display = "block";
      } else {
        img.style.display = "none";
      }
    }

    function envoyerCommande() {
      const nom = document.getElementById("nom").value;
      const tel = document.getElementById("tel").value;
      const adresse = document.getElementById("adresse").value;
      const menuText = document.getElementById("menu").options[document.getElementById("menu").selectedIndex].text;
      const dessertText = document.getElementById("dessert").options[document.getElementById("dessert").selectedIndex].text;
      const total = document.getElementById("total").textContent;

      const mailto = `mailto:traoreaissatou49@gmail.com?subject=Nouvelle commande&body=Nom: ${nom}%0D%0ATéléphone: ${tel}%0D%0AAdresse: ${adresse}%0D%0AMenu: ${menuText}%0D%0ADessert: ${dessertText}%0D%0ATotal: ${total} FCFA`;

      window.location.href = mailto;
    }

    function envoyerWhatsapp() {
      const nom = document.getElementById("nom").value;
      const tel = document.getElementById("tel").value;
      const adresse = document.getElementById("adresse").value;
      const menuText = document.getElementById("menu").options[document.getElementById("menu").selectedIndex].text;
      const dessertText = document.getElementById("dessert").options[document.getElementById("dessert").selectedIndex].text;
      const total = document.getElementById("total").textContent;

      const message = `Bonjour, je souhaite passer une commande.%0A%0ANom: ${nom}%0ATéléphone: ${tel}%0AAdresse: ${adresse}%0AMenu: ${menuText}%0ADessert: ${dessertText}%0ATotal: ${total} FCFA`;
      const whatsappUrl = `https://wa.me/221777561848?text=${message}`;
      window.open(whatsappUrl, '_blank');
    }
  </script>
</body>
</html>
