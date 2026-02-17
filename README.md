<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vastramanjiri | Shop</title>
    <style>
        :root { --maroon: #800000; --gold: #d4af37; }
        body { margin: 0; font-family: 'Georgia', serif; background: #fffaf0; }
        
        header { background: var(--maroon); color: var(--gold); padding: 20px; text-align: center; }
        .grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; padding: 20px; }
        
        .card { background: white; padding: 15px; border-radius: 10px; border: 1px solid var(--gold); text-align: center; }
        .card img { width: 100%; height: 300px; object-fit: cover; border-radius: 5px; }

        .controls { display: flex; align-items: center; justify-content: center; margin: 10px 0; gap: 10px; }
        .qty-btn { background: var(--maroon); color: white; border: none; width: 25px; height: 25px; border-radius: 50%; cursor: pointer; }
        
        .pay-btn { background: #27ae60; color: white; border: none; padding: 12px; width: 100%; border-radius: 5px; cursor: pointer; font-weight: bold; }
        
        /* Modal */
        #payment-modal { display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.9); justify-content:center; align-items:center; z-index:2000; color: white; }
        .modal-box { background: white; color: black; padding: 20px; border-radius: 15px; width: 85%; max-width: 400px; text-align: center; }
    </style>
</head>
<body>

<header>
    <h1>VASTRAMANJIRI</h1>
    <p>Premium Saree Collection</p>
</header>

<div class="grid">
    <div class="card">
        <img src="https://images.unsplash.com/photo-1610030469983-98e550d6193c?w=400" alt="Saree">
        <h3>Kanchipuram Silk</h3>
        <p>₹5,000</p>
        <div class="controls">
            <button class="qty-btn" onclick="updateQty('q1', -1)">-</button>
            <span id="q1">1</span>
            <button class="qty-btn" onclick="updateQty('q1', 1)">+</button>
        </div>
        <button class="pay-btn" onclick="openPayment('Kanchipuram Silk', 5000, 'q1')">PAY ORDER</button>
    </div>

    <div class="card">
        <img src="https://images.unsplash.com/photo-1583391733956-3750e0ff4e8b?w=400" alt="Saree">
        <h3>Banarasi Silk</h3>
        <p>₹7,000</p>
        <div class="controls">
            <button class="qty-btn" onclick="updateQty('q2', -1)">-</button>
            <span id="q2">1</span>
            <button class="qty-btn" onclick="updateQty('q2', 1)">+</button>
        </div>
        <button class="pay-btn" onclick="openPayment('Banarasi Silk', 7000, 'q2')">PAY ORDER</button>
    </div>
</div>

<div id="payment-modal">
    <div class="modal-box">
        <h2 style="color:var(--maroon)">Scan to Pay</h2>
        <div id="summary"></div>
        <img src="https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=upi://pay?pa=vastramanjiri@upi" alt="QR">
        <p>UPI: vastramanjiri@upi</p>
        <button class="pay-btn" onclick="sendInstagramDM()">SEND ORDER TO INSTAGRAM INBOX</button>
        <button onclick="closeModal()" style="margin-top:10px; border:none; background:none; color:red; cursor:pointer;">Cancel</button>
    </div>
</div>

<script>
    let orderDetails = {};

    function updateQty(id, val) {
        let el = document.getElementById(id);
        let current = parseInt(el.innerText);
        if(current + val >= 1) el.innerText = current + val;
    }

    function openPayment(name, price, qtyId) {
        let qty = document.getElementById(qtyId).innerText;
        let total = price * qty;
        orderDetails = { name, qty, total };
        
        document.getElementById('summary').innerHTML = `
            <p><strong>Saree:</strong> ${name}</p>
            <p><strong>Quantity:</strong> ${qty}</p>
            <p><strong>Total:</strong> ₹${total}</p>
        `;
        document.getElementById('payment-modal').style.display = 'flex';
    }

    function closeModal() { document.getElementById('payment-modal').style.display = 'none'; }

    function sendInstagramDM() {
        const instaUser = "vastramanjiri"; // <-- YOUR INSTAGRAM USERNAME
        const message = `Hello Vastramanjiri! I want to order:%0AItem: ${orderDetails.name}%0AQuantity: ${orderDetails.qty}%0ATotal Amount: ₹${orderDetails.total}%0A%0AI have paid via QR. Please confirm!`;
        
        // This opens your Instagram Profile DM
        window.open(`https://www.instagram.com/direct/t/${instaUser}/?text=${message}`, '_blank');
        
        // Backup: If direct DM link is restricted, this goes to your profile
        setTimeout(() => {
            alert("If the chat didn't open, please DM this message to @vastramanjiri: \n\n" + decodeURIComponent(message));
            window.location.href = `https://instagram.com/${instaUser}`;
        }, 1000);
    }
</script>
</body>
</html>
