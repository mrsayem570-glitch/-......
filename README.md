<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ad Dashboard Ultra Fixed</title>

<style>
body{
    margin:0;
    font-family:'Segoe UI',sans-serif;
    background: linear-gradient(135deg,#0f2027,#203a43,#2c5364);
    color:#fff;
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
}

.container{
    width:330px;
    background:rgba(255,255,255,0.06);
    backdrop-filter: blur(18px);
    border-radius:25px;
    padding:25px;
    box-shadow:0 15px 40px rgba(0,0,0,0.6);
    text-align:center;
}

h2{ margin:5px 0 10px; }

.dev{ font-size:13px; margin-bottom:10px; }
.dev a{ color:#00f7ff; text-decoration:none; }

input{
    width:100%;
    padding:10px;
    border:none;
    border-radius:12px;
    margin-bottom:10px;
    text-align:center;
    outline:none;
}

.username{ font-size:13px; opacity:0.8; margin-bottom:10px; }

.circle{
    width:160px;
    height:160px;
    border-radius:50%;
    margin:15px auto;
    display:flex;
    justify-content:center;
    align-items:center;
    font-size:24px;
    font-weight:bold;
    background:conic-gradient(#00f7ff 0%, #222 0%);
    box-shadow:0 0 25px rgba(0,255,255,0.6);
}

.stats{
    display:flex;
    justify-content:space-between;
    margin:10px 0;
}

.card{
    width:48%;
    padding:12px;
    border-radius:15px;
    background:rgba(255,255,255,0.08);
}

button{
    width:100%;
    padding:13px;
    border:none;
    border-radius:15px;
    background:linear-gradient(135deg,#00f7ff,#00c3ff);
    font-size:17px;
    font-weight:bold;
    cursor:pointer;
    transition:0.3s;
}

button:hover{ transform:scale(1.07); }

.footer{ margin-top:12px; font-size:12px; opacity:0.7; }

</style>
</head>

<body>

<div class="container">

    <h2>💎 Earn Rewards</h2>

    <div class="dev">
        Developer: <a href="https://t.me/SAYEM_690" target="_blank">@SAYEM_690</a>
    </div>

    <input type="text" id="username" placeholder="Enter Username">
    <div class="username" id="showUser">User: Guest</div>

    <div class="circle" id="circle">0%</div>

    <div class="stats">
        <div class="card">
            <p>Ads</p>
            <h3 id="ads">0</h3>
        </div>
        <div class="card">
            <p>Points</p>
            <h3 id="points">0</h3>
        </div>
    </div>

    <button id="btn" disabled>Loading...</button>

    <div class="footer">🚀 Watch ads & earn points</div>

</div>

<!-- ✅ Monetag Script (ZONE ID ঠিক রাখা হয়েছে) -->
<script src="https://libtl.com/sdk.js" data-zone="10852660" data-sdk="show_10852660"></script>

<script>
let ads = 0;
let points = 0;
let btn = document.getElementById("btn");
let usernameInput = document.getElementById("username");

// Username
usernameInput.oninput = function(){
    let name = usernameInput.value || "Guest";
    document.getElementById("showUser").innerText = "User: " + name;
}

// Update UI
function update(){
    document.getElementById("ads").innerText = ads;
    document.getElementById("points").innerText = points.toFixed(2);

    let p = Math.min((ads/10)*100,100);
    document.getElementById("circle").innerText = p + "%";
    document.getElementById("circle").style.background =
    `conic-gradient(#00f7ff ${p}%, #222 ${p}%)`;
}

// ✅ Strong SDK loader (fix for ad failed)
let checkSDK = setInterval(()=>{
    if(typeof window.show_10852660 === "function"){
        btn.innerText = "🎬 Watch Ad";
        btn.disabled = false;
        clearInterval(checkSDK);
    }
},1000);

// Click event
btn.onclick = function(){

    if(typeof window.show_10852660 === "function"){
        show_10852660()
        .then(()=>{
            ads++;
            points += 0.5;
            update();
        })
        .catch((err)=>{
            console.log("Ad Error:", err);
            alert("Ad failed ⚠️ Try again");
        });

    }else{
        alert("Ad not ready yet ❌");
    }
}

update();
</script>

</body>
</html>
