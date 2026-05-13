<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>WORLD STITCHING - Premium Sportswear Pakistan</title>
<script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-database-compat.js"></script>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Rajdhani:wght@400;500;600;700&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
<style>
*{margin:0;padding:0;box-sizing:border-box}
:root{
    /* EXACT LOGO COLORS */
    --logo-red:#DC2626;        /* Red from logo */
    --logo-red-dark:#991b1b;
    --logo-dark:#1a1a1a;       /* Dark from logo */
    --logo-silver:#b0b0b0;     /* Metallic from logo */
    --logo-bg:#F8F9FA;         /* Off-white background */
    --card:#FFFFFF;
    --text:#1A1A1A;
    --text-light:#5a6478;
    --border:#e5e7eb;
    --whatsapp:#25D366;
}
body{font-family:'Inter',sans-serif;background:var(--logo-bg);color:var(--text);overflow-x:hidden}

/* NAV */
nav{position:sticky;top:0;z-index:1000;background:var(--logo-dark);border-bottom:3px solid var(--logo-red);padding:12px 24px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap}
.nav-logo{display:flex;align-items:center;gap:12px;cursor:pointer}
.nav-logo .logo-img{width:50px;height:50px;display:flex;align-items:center;justify-content:center}
.nav-logo .logo-img img{width:100%;height:100%;object-fit:contain}
.nav-brand{font-family:'Bebas Neue';font-size:22px;letter-spacing:3px;color:white}
.nav-brand span{display:block;font-family:'Inter',sans-serif;font-size:9px;letter-spacing:2px;color:var(--logo-silver);font-weight:400}
.nav-links{display:flex;gap:24px;align-items:center}
.nav-links a{color:rgba(255,255,255,0.75);text-decoration:none;font-size:13px;letter-spacing:1px;text-transform:uppercase;transition:0.3s;cursor:pointer}
.nav-links a:hover{color:var(--logo-silver)}
.nav-wa{background:var(--whatsapp);color:#fff!important;padding:8px 16px;border-radius:4px}
.cart-icon{position:relative;cursor:pointer;color:white}
.cart-count{position:absolute;top:-8px;right:-12px;background:var(--logo-red);color:#fff;font-size:10px;font-weight:bold;width:18px;height:18px;border-radius:50%;display:flex;align-items:center;justify-content:center}
.hamburger{display:none;flex-direction:column;cursor:pointer;gap:4px}
.hamburger span{width:25px;height:2px;background:white;transition:0.3s}

/* SLIDE MENU */
.slide-menu{position:fixed;top:0;right:-280px;width:280px;height:100%;z-index:2000;background:var(--logo-dark);border-left:1px solid rgba(255,255,255,0.1);transition:right 0.3s;padding:70px 20px}
.slide-menu.open{right:0}
.slide-menu-overlay{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.5);z-index:1999;display:none}
.slide-menu-overlay.active{display:block}
.slide-menu .cat-item{display:block;padding:12px;border-bottom:1px solid rgba(255,255,255,0.1);cursor:pointer;color:rgba(255,255,255,0.75)}
.slide-menu .cat-item:hover{background:rgba(220,38,38,0.1);color:var(--logo-silver)}
.slide-menu .close-menu{position:absolute;top:15px;right:20px;font-size:24px;cursor:pointer;color:white}

/* HERO */
.hero{min-height:75vh;display:flex;align-items:center;justify-content:center;text-align:center;background:linear-gradient(135deg,var(--logo-dark),#0a0a0a);position:relative;overflow:hidden}
.hero::before{content:'';position:absolute;top:-50%;right:-20%;width:600px;height:600px;background:var(--logo-red);border-radius:50%;opacity:0.05}
.hero-logo{width:180px;height:180px;margin:0 auto 20px;animation:float 3s ease-in-out infinite}
.hero-logo img{width:100%;height:100%;object-fit:contain;filter:drop-shadow(0 0 30px rgba(220,38,38,0.3))}
@keyframes float{0%,100%{transform:translateY(0px)}50%{transform:translateY(-8px)}}
.hero-eyebrow{font-size:11px;letter-spacing:5px;color:var(--logo-silver);text-transform:uppercase}
.hero-title{font-family:'Bebas Neue';font-size:clamp(42px,8vw,80px);line-height:0.95;letter-spacing:4px;color:white}
.hero-title span{color:var(--logo-red)}
.hero-sub{font-size:13px;letter-spacing:4px;color:rgba(255,255,255,0.6);text-transform:uppercase;margin:20px 0}
.hero-btns{display:flex;gap:16px;justify-content:center}
.btn-primary{background:var(--logo-red);color:#fff;padding:14px 32px;border-radius:3px;font-size:12px;letter-spacing:2px;text-transform:uppercase;font-weight:700;transition:0.3s;border:none;cursor:pointer}
.btn-primary:hover{transform:translateY(-2px);box-shadow:0 8px 25px rgba(220,38,38,0.3)}
.btn-outline{background:transparent;color:var(--logo-silver);padding:14px 32px;border-radius:3px;font-size:12px;letter-spacing:2px;text-transform:uppercase;font-weight:700;border:1px solid var(--logo-silver);transition:0.3s;cursor:pointer}
.btn-outline:hover{background:rgba(176,176,176,0.08);transform:translateY(-2px)}

/* STATS */
.stats{background:var(--logo-red);padding:24px;display:grid;grid-template-columns:repeat(4,1fr);gap:1px}
.stat{text-align:center;padding:20px}
.stat-num{font-family:'Bebas Neue';font-size:36px;color:white}
.stat-label{font-size:11px;letter-spacing:2px;color:rgba(255,255,255,0.8);text-transform:uppercase;margin-top:4px}

/* SECTIONS */
.section{padding:60px 24px;max-width:1200px;margin:0 auto}
.section-header{text-align:center;margin-bottom:48px}
.section-eyebrow{font-size:11px;letter-spacing:4px;color:var(--logo-red);text-transform:uppercase}
.section-title{font-family:'Bebas Neue';font-size:clamp(32px,5vw,48px);letter-spacing:3px;color:var(--logo-dark)}
.section-title span{color:var(--logo-red)}
.section-line{width:60px;height:3px;background:var(--logo-red);margin:16px auto 0}

/* CATEGORY TABS */
.cat-tabs{display:flex;gap:8px;justify-content:center;flex-wrap:wrap;margin-bottom:40px}
.cat-tab{padding:10px 24px;border-radius:30px;font-size:12px;letter-spacing:2px;text-transform:uppercase;cursor:pointer;border:1px solid var(--border);background:var(--card);color:var(--text-light);transition:0.3s}
.cat-tab.active,.cat-tab:hover{border-color:var(--logo-red);color:var(--logo-red)}
.gender-tabs{display:flex;justify-content:center;margin-bottom:32px;border:1px solid var(--border);border-radius:30px;width:fit-content;margin:0 auto 32px;background:white}
.gender-tab{padding:10px 28px;font-size:12px;letter-spacing:2px;text-transform:uppercase;cursor:pointer;background:var(--card);color:var(--text-light);border:none;border-right:1px solid var(--border);border-radius:0}
.gender-tab:first-child{border-radius:30px 0 0 30px}
.gender-tab:last-child{border-radius:0 30px 30px 0;border-right:none}
.gender-tab.active{background:var(--logo-dark);color:white}

/* PRODUCTS */
.products-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:25px}
.product-card{background:var(--card);border:1px solid var(--border);border-radius:12px;overflow:hidden;cursor:pointer;transition:0.3s}
.product-card:hover{transform:translateY(-5px);border-color:var(--logo-red);box-shadow:0 15px 35px rgba(26,26,26,0.08)}
.product-img{height:220px;background:#FAFAFA;overflow:hidden;position:relative}
.product-img img{width:100%;height:100%;object-fit:cover;transition:0.3s}
.product-card:hover .product-img img{transform:scale(1.03)}
.sale-badge{position:absolute;top:12px;right:12px;background:var(--logo-red);color:#fff;font-size:11px;font-weight:700;padding:5px 12px;border-radius:20px}
.trending-badge{position:absolute;top:12px;left:12px;background:var(--logo-silver);color:var(--logo-dark);font-size:11px;font-weight:700;padding:5px 12px;border-radius:20px}
.product-body{padding:16px}
.product-cat{font-size:10px;letter-spacing:2px;color:var(--logo-red);text-transform:uppercase;margin-bottom:6px}
.product-name{font-weight:700;margin-bottom:4px;color:var(--logo-dark)}
.product-desc{font-size:12px;color:var(--text-light);margin-bottom:10px}
.price-row{display:flex;align-items:center;gap:12px}
.original-price{font-size:14px;color:var(--text-light);text-decoration:line-through}
.sale-price{font-size:22px;font-weight:700;color:var(--logo-red);font-family:'Bebas Neue'}
.normal-price{font-size:22px;font-weight:700;color:var(--logo-dark);font-family:'Bebas Neue'}
.color-variants{display:flex;gap:8px;margin:12px 0}
.color-dot{width:25px;height:25px;border-radius:50%;cursor:pointer;border:2px solid var(--border);transition:0.2s}
.color-dot.active{transform:scale(1.12);border-color:var(--logo-red);box-shadow:0 0 6px var(--logo-red)}

/* CUSTOM SECTION */
.custom-section{background:var(--logo-dark);border:1px solid rgba(220,38,38,0.2);border-radius:12px;padding:48px 32px;text-align:center;margin-top:40px}
.custom-title{font-family:'Bebas Neue';font-size:42px;letter-spacing:3px;color:white}
.custom-title span{color:var(--logo-silver)}
.custom-features{display:flex;gap:16px;justify-content:center;flex-wrap:wrap;margin:32px 0}
.custom-feat{background:rgba(255,255,255,0.08);border:1px solid rgba(255,255,255,0.15);border-radius:40px;padding:10px 20px;font-size:12px;color:rgba(255,255,255,0.8)}
.custom-feat:hover{transform:translateY(-2px);background:rgba(176,176,176,0.1);border-color:var(--logo-silver)}

/* FOOTER */
footer{background:#050505;border-top:3px solid var(--logo-red);padding:40px 24px;text-align:center}
.footer-logo{font-family:'Bebas Neue';font-size:28px;letter-spacing:4px;color:white}
.footer-links{display:flex;gap:24px;justify-content:center;margin:24px 0}
.footer-links a{color:rgba(255,255,255,0.5);text-decoration:none;font-size:12px;text-transform:uppercase;transition:0.2s;cursor:pointer}
.footer-links a:hover{color:var(--logo-red)}
.wa-float{position:fixed;bottom:24px;right:24px;z-index:200;background:var(--whatsapp);color:#fff;border-radius:50%;width:55px;height:55px;display:flex;align-items:center;justify-content:center;font-size:28px;text-decoration:none;cursor:pointer;box-shadow:0 4px 12px rgba(0,0,0,0.15)}
.wa-float:hover{transform:scale(1.05)}
.toast{position:fixed;bottom:90px;right:24px;background:var(--logo-dark);color:#fff;border-radius:4px;padding:12px 20px;z-index:300;transform:translateX(120%);transition:0.3s;border-left:3px solid var(--logo-red)}
.toast.show{transform:translateX(0)}
.page{display:none}
.page.active{display:block}

/* PRODUCT DETAIL */
.product-detail{display:grid;grid-template-columns:1fr 1fr;gap:50px;max-width:1200px;margin:0 auto;padding:40px 20px}
.product-detail-img img{width:100%;border-radius:12px}
.product-detail-title{font-size:28px;margin-bottom:15px;color:var(--logo-dark)}
.product-detail-price{font-size:32px;color:var(--logo-red);font-weight:600;margin-bottom:15px}
.product-detail-price s{font-size:18px;color:var(--text-light);margin-right:10px}
.product-detail-desc{color:var(--text-light);line-height:1.6;margin-bottom:25px}
.detail-section-title{margin:20px 0 10px;font-size:14px;letter-spacing:2px;color:var(--logo-dark)}
.detail-size-options{display:flex;gap:10px;flex-wrap:wrap;margin-bottom:15px}
.detail-size-btn{padding:10px 25px;border:1px solid var(--border);background:var(--card);cursor:pointer;border-radius:4px}
.detail-size-btn.active{border-color:var(--logo-dark);background:var(--logo-dark);color:#fff}
.detail-color-options{display:flex;gap:12px;flex-wrap:wrap;margin-bottom:15px}
.detail-color-option{width:45px;height:45px;border-radius:50%;cursor:pointer;border:2px solid var(--border)}
.detail-color-option.active{border-color:var(--logo-red);box-shadow:0 0 0 2px var(--logo-red)}
.detail-qty-selector{display:flex;align-items:center;gap:15px;margin-bottom:20px}
.detail-qty-btn{width:40px;height:40px;border:1px solid var(--border);background:var(--card);cursor:pointer;font-size:18px}
.detail-qty-input{width:60px;text-align:center;border:1px solid var(--border);padding:10px}
.detail-stock-info{font-size:13px;color:var(--text-light);margin-bottom:20px}
.detail-action-buttons{display:flex;flex-wrap:wrap;gap:12px;margin-bottom:25px;align-items:center}
.detail-btn-add-cart{flex:1;background:var(--logo-dark);color:#fff;padding:14px;border:none;cursor:pointer;font-weight:600;border-radius:4px;transition:0.2s}
.detail-btn-add-cart:hover{background:#2d2d2d}
.detail-btn-buy-now{flex:1;background:var(--logo-red);color:#fff;padding:14px;border:none;cursor:pointer;font-weight:600;border-radius:4px;transition:0.2s}
.detail-btn-buy-now:hover{background:var(--logo-red-dark)}
.sizechart-btn{background:transparent;border:1px solid var(--logo-silver);color:var(--logo-silver);padding:8px 15px;border-radius:4px;cursor:pointer;font-size:12px;transition:0.2s;white-space:nowrap}
.sizechart-btn:hover{background:rgba(176,176,176,0.1)}
.related-products{margin-top:50px}
.related-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:20px}
.related-card{cursor:pointer;text-align:center;transition:0.2s}
.related-card:hover{transform:translateY(-3px)}
.related-card img{width:100%;border-radius:8px;aspect-ratio:1/1;object-fit:cover}
.related-card h4{font-size:13px;margin-top:8px}
.related-card p{font-size:13px;color:var(--logo-red);font-weight:600}

/* CART */
.cart-grid{display:grid;grid-template-columns:2fr 1fr;gap:40px;max-width:1200px;margin:0 auto;padding:20px}
.cart-items{border:1px solid var(--border);border-radius:12px;overflow:hidden;background:white}
.cart-header{display:grid;grid-template-columns:3fr 1fr 1fr 0.5fr;padding:15px;background:var(--logo-bg);font-size:12px;font-weight:600}
.cart-item{display:grid;grid-template-columns:3fr 1fr 1fr 0.5fr;align-items:center;padding:15px;border-bottom:1px solid var(--border)}
.cart-item-info{display:flex;gap:15px;align-items:center}
.cart-item-info img{width:80px;height:80px;object-fit:cover;border-radius:8px}
.cart-item-info h4{font-size:14px}
.cart-item-info p{font-size:12px;color:var(--text-light)}
.cart-summary{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:25px}
.summary-row{display:flex;justify-content:space-between;padding:10px 0}
.summary-total{font-size:18px;font-weight:700;border-top:1px solid var(--border);padding-top:15px}
.cart-qty-btn{width:28px;height:28px;border:1px solid var(--border);background:var(--card);cursor:pointer}
.cart-remove{color:var(--logo-red);cursor:pointer}

/* CHECKOUT */
.checkout-grid{display:grid;grid-template-columns:1fr 1.5fr;gap:40px;max-width:1200px;margin:0 auto;padding:20px}
.checkout-form{background:var(--card);border-radius:12px;padding:30px;border:1px solid var(--border)}
.checkout-form .form-row{display:grid;grid-template-columns:1fr 1fr;gap:15px;margin-bottom:15px}
.checkout-form .form-group{display:flex;flex-direction:column;gap:6px}
.checkout-form input{padding:12px;border:1px solid var(--border);border-radius:6px}
.jazzcash-box{background:linear-gradient(135deg,#25D36610,#fff);border:1px solid var(--whatsapp);border-radius:12px;padding:20px;text-align:center;margin-top:15px}
.jazzcash-box i{font-size:40px;color:var(--whatsapp)}
.jazzcash-box h3{font-size:24px;color:var(--whatsapp);margin:10px 0}
.back-link{display:inline-block;margin-top:15px;color:var(--text-light);text-decoration:none;font-size:12px;cursor:pointer}

/* ADMIN */
.admin-section{background:var(--card);border:1px solid var(--border);border-radius:12px;padding:25px;margin-top:40px}
.admin-toggle{cursor:pointer;display:flex;justify-content:space-between;align-items:center}
.password-box{background:var(--logo-bg);padding:20px;border-radius:8px;margin-top:15px;text-align:center}
.variant-row{background:var(--logo-bg);padding:15px;border-radius:8px;margin-bottom:15px}
.btn-add{background:var(--logo-red);color:white;border:none;padding:10px 20px;border-radius:4px;cursor:pointer}
.btn-add-variant{background:transparent;border:1px dashed var(--logo-silver);padding:10px;width:100%;border-radius:4px;margin:10px 0;cursor:pointer}
.manage-table{width:100%;border-collapse:collapse}
.manage-table th,.manage-table td{padding:10px;border-bottom:1px solid var(--border);text-align:left}

/* SIZE CHART */
.sizechart-modal{display:none;position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.8);z-index:10000;align-items:center;justify-content:center}
.sizechart-content{background:white;max-width:550px;width:90%;border-radius:12px;padding:25px;position:relative}
.sizechart-content h3{color:var(--logo-red);margin-bottom:20px;font-family:'Bebas Neue';letter-spacing:2px;text-align:center}
.sizechart-close{position:absolute;top:15px;right:20px;font-size:24px;cursor:pointer;color:#666}
.sizechart-tab{background:transparent;border:1px solid var(--logo-silver);color:var(--logo-silver);padding:8px 20px;border-radius:4px;cursor:pointer;font-size:12px;transition:0.2s}
.sizechart-tab.active{background:var(--logo-silver);color:#000}
.sizechart-panel{display:none}
.sizechart-panel.active{display:block}
.sizechart-table{width:100%;border-collapse:collapse;margin-top:15px}
.sizechart-table th,.sizechart-table td{padding:10px;border:1px solid #ddd;text-align:center}
.sizechart-table th{background:var(--logo-dark);color:white}

@media(max-width:768px){.nav-links{display:none}.hamburger{display:flex}.stats{grid-template-columns:repeat(2,1fr)}.products-grid{grid-template-columns:1fr}.product-detail{grid-template-columns:1fr}.cart-grid{grid-template-columns:1fr}.cart-header{display:none}.cart-item{display:flex;flex-direction:column;text-align:center}.checkout-grid{grid-template-columns:1fr}.related-grid{grid-template-columns:repeat(2,1fr)}.detail-action-buttons{flex-direction:column}}
</style>
</head>
<body>

<nav>
<div class="nav-logo" onclick="showPage('home')">
<div class="logo-img">
    <!-- 🔴 APKA LOGO YAHAN LAGAYA HAI -->
    <img src="https://i.postimg.cc/dtLpF6sy/WS-LOGO.png" alt="World Stitching Logo">
</div>
<div class="nav-brand">WORLD STITCHING <span>Sportswear Manufacturing</span></div>
</div>
<div class="nav-links">
<a onclick="showPage('home')">Home</a>
<a onclick="showPage('home');document.getElementById('products').scrollIntoView()">Products</a>
<a onclick="showPage('custom')">Customization</a>
<a class="nav-wa" onclick="openWA('Hi! I want to inquire.')">WhatsApp</a>
<div class="cart-icon" onclick="showPage('cart')"><i class="fas fa-shopping-bag"></i><span id="cartCount" class="cart-count">0</span></div>
<button id="adminShowBtn" style="background:var(--logo-silver);border:none;padding:6px 15px;border-radius:4px;cursor:pointer;font-size:11px;font-weight:600">Admin</button>
</div>
<div class="hamburger" id="hamburger"><span></span><span></span><span></span></div>
</nav>

<div class="slide-menu-overlay" id="slideOverlay"></div>
<div class="slide-menu" id="slideMenu">
<div class="close-menu" id="closeMenu">&times;</div>
<h3 style="color:white">MENU</h3>
<div class="cat-item" onclick="showPage('home');closeSlideMenu()">Home</div>
<div class="cat-item" onclick="showPage('home');document.getElementById('products').scrollIntoView();closeSlideMenu()">Products</div>
<div class="cat-item" onclick="showPage('cart');closeSlideMenu()">Cart</div>
<div class="cat-item" onclick="showPage('checkout');closeSlideMenu()">Checkout</div>
<div class="cat-item" onclick="showPage('custom');closeSlideMenu()">Custom Order</div>
<h3 style="color:white;margin-top:30px">HELP</h3>
<div class="cat-item" onclick="openWA('Hi! World Stitching inquiry.');closeSlideMenu()">WhatsApp</div>
</div>

<div id="homePage" class="page active">
<div class="hero">
<div class="hero-content">
    <div class="hero-logo">
        <!-- 🔴 HERO MEIN BHI APKA LOGO -->
        <img src="https://i.postimg.cc/dtLpF6sy/WS-LOGO.png" alt="World Stitching Logo">
    </div>
    <div class="hero-eyebrow">Premium Quality Sportswear</div>
    <h1 class="hero-title">WORLD<br><span>STITCHING</span></h1>
    <p class="hero-sub">Crafted for Champions — Made in Faisalabad, Pakistan</p>
    <div class="hero-btns"><button class="btn-primary" onclick="document.getElementById('products').scrollIntoView()">Shop Now</button><button class="btn-outline" onclick="openWA('Hi! I want bulk order.')">Bulk Order</button></div>
</div>
</div>
<div class="stats"><div class="stat"><div class="stat-num">500+</div><div class="stat-label">Products</div></div><div class="stat"><div class="stat-num">1000+</div><div class="stat-label">Happy Clients</div></div><div class="stat"><div class="stat-label">Based In</div><div class="stat-label" style="font-size:15px;font-weight:600">Faisalabad</div></div><div class="stat"><div class="stat-num">5★</div><div class="stat-label">Quality Rating</div></div></div>
<div class="section" id="products"><div class="section-header"><div class="section-eyebrow">Our Collection</div><h2 class="section-title">Shop By <span>Category</span></h2><div class="section-line"></div></div>
<div class="gender-tabs"><button class="gender-tab active" onclick="filterGender('all',this)">All</button><button class="gender-tab" onclick="filterGender('men',this)">Men</button><button class="gender-tab" onclick="filterGender('women',this)">Women</button><button class="gender-tab" onclick="filterGender('boys',this)">Boys</button><button class="gender-tab" onclick="filterGender('girls',this)">Girls</button></div>
<div class="cat-tabs" id="catTabs"><button class="cat-tab active" onclick="filterCat('all',this)">All Products</button><button class="cat-tab" onclick="filterCat('kit',this)">Sports Kits</button><button class="cat-tab" onclick="filterCat('trouser',this)">Trousers</button><button class="cat-tab" onclick="filterCat('shirt',this)">Shirts</button><button class="cat-tab" onclick="filterCat('jacket',this)">Varsity Jackets</button><button class="cat-tab" onclick="filterCat('tracksuit',this)">Tracksuits</button><button class="cat-tab" onclick="filterCat('summer',this)">Summer Wear</button></div>
<div class="products-grid" id="productsGrid"></div></div>
<div class="section" id="custom"><div class="custom-section"><div class="custom-title">Custom <span>Orders</span></div><p style="color:rgba(255,255,255,0.7);margin-top:16px">Team name, number, logo — sab kuch aapke hisaab se.</p><div class="custom-features"><div class="custom-feat">🎨 Custom Colors</div><div class="custom-feat">🔢 Player Numbers</div><div class="custom-feat">🏷️ Brand Logo</div><div class="custom-feat">📦 Bulk Orders</div><div class="custom-feat">🚀 Fast Delivery</div></div><button class="btn-primary" onclick="openWA('Hi! Custom order.')">Order Customize Now</button></div></div>
<div class="section" id="adminPanelSection" style="display:none"><div class="admin-section"><div class="admin-toggle" onclick="toggleAdminPanel()"><div class="admin-title">⚙ Admin Panel</div><span id="adminIcon">▼</span></div>
<div id="adminPasswordBox" class="password-box"><h3>🔐 Admin Access</h3><input type="password" id="adminPassword" placeholder="Password" style="padding:10px;width:250px;margin:10px auto;display:block"><button class="btn-primary" onclick="checkAdminPassword()">Submit</button><div id="adminError" style="color:red;display:none;margin-top:10px">Wrong password!</div></div>
<div id="adminForm" style="display:none"><h3>Add Product</h3><div class="form-row"><div class="form-group"><label>Name</label><input id="pName" placeholder="Product name"></div><div class="form-group"><label>Price</label><input id="pPrice" type="number" placeholder="Price"></div></div><div class="form-row"><div class="form-group"><label>Category</label><select id="pCat"><option value="kit">Sports Kit</option><option value="trouser">Trouser</option><option value="shirt">Shirt</option><option value="jacket">Jacket</option><option value="tracksuit">Tracksuit</option><option value="summer">Summer</option></select></div><div class="form-group"><label>Gender</label><select id="pGender"><option value="men">Men</option><option value="women">Women</option><option value="boys">Boys</option><option value="girls">Girls</option><option value="uni">Unisex</option></select></div></div><div class="form-group"><label>Description</label><input id="pDesc" placeholder="Description"></div>
<div id="variantsContainer"></div><button class="btn-add-variant" onclick="addVariantField()">+ Color Variant</button><button class="btn-add" onclick="addProductToFirebase()" style="margin-top:15px">Add Product</button><h3 style="margin-top:30px">Manage Products</h3><div style="overflow-x:auto"><table class="manage-table"><thead><th>Product</th><th>Category</th><th>Gender</th><th>Variants</th><th>Action</th></thead><tbody id="manageBody"></tbody></table></div></div></div></div>
<footer id="contact"><div class="footer-logo">WORLD STITCHING</div><div style="font-size:11px;letter-spacing:3px;color:rgba(255,255,255,0.5);margin-bottom:24px">Sportswear Manufacturing — Faisalabad, Pakistan</div><div class="footer-links"><a onclick="showPage('home')">Home</a><a onclick="showPage('home');document.getElementById('products').scrollIntoView()">Products</a><a onclick="openWA('Hi! World Stitching inquiry.')">WhatsApp</a></div><div class="footer-copy" style="font-size:11px;color:rgba(255,255,255,0.3)">© 2025 World Stitching Sportswear. All rights reserved.</div></footer>
</div>

<div id="productPage" class="page"><div class="product-detail" id="productDetailContainer"></div></div>
<div id="cartPage" class="page"><div id="cartContainer"></div></div>
<div id="checkoutPage" class="page"><div id="checkoutContainer"></div></div>
<div id="customPage" class="page"><div style="max-width:1200px;margin:0 auto;padding:40px 20px"><div class="back-link" onclick="showPage('home')">← Back to Home</div><div class="custom-section" style="margin-top:20px"><div class="custom-title">Custom <span>Sportswear</span></div><p style="color:rgba(255,255,255,0.7);margin:20px 0">Apna design, logo, colors — we manufacture exactly what you dream. Minimum order 10 pieces.</p><div class="custom-features"><div class="custom-feat">🎨 Any Color</div><div class="custom-feat">🔢 Player Numbers</div><div class="custom-feat">🏷️ Custom Logo</div><div class="custom-feat">📦 Bulk Discounts</div></div><button class="btn-primary" onclick="openWA('Hi! I want to discuss custom order.')">Discuss on WhatsApp →</button></div></div></div>

<!-- Size Chart Modal -->
<div id="sizeChartModal" class="sizechart-modal">
<div class="sizechart-content">
<span class="sizechart-close" onclick="closeSizeChart()">&times;</span>
<div style="display: flex; gap: 10px; justify-content: center; margin-bottom: 20px; flex-wrap: wrap;">
<button id="sizeTabShirt" class="sizechart-tab active" onclick="showSizeChart('shirt')">👕 Shirt Size Chart</button>
<button id="sizeTabTrouser" class="sizechart-tab" onclick="showSizeChart('trouser')">👖 Trouser Size Chart</button>
</div>
<div id="shirtSizeChart" class="sizechart-panel active">
<h3>📏 SHIRT SIZE CHART (inches)</h3>
<table class="sizechart-table">
<thead><th>SIZE</th><th>CHEST</th><th>LENGTH</th></thead>
<tbody><tr><td>S</td><td>36-38</td><td>27</td></tr><tr><td>M</td><td>38-40</td><td>28</td></tr><tr><td>L</td><td>40-42</td><td>29</td></tr><tr><td>XL</td><td>42-44</td><td>30</td></tr><tr><td>2XL</td><td>44-46</td><td>31</td></tr></tbody>
</table>
</div>
<div id="trouserSizeChart" class="sizechart-panel">
<h3>📏 TROUSERS SIZE CHART (inches)</h3>
<table class="sizechart-table">
<thead><th>SIZE</th><th>WAIST</th><th>LENGTH</th></thead>
<tbody><tr><td>S</td><td>28-30</td><td>38</td></tr><tr><td>M</td><td>30-32</td><td>39</td></tr><tr><td>L</td><td>32-34</td><td>40</td></tr><tr><td>XL</td><td>34-36</td><td>41</td></tr><tr><td>2XL</td><td>36-38</td><td>42</td></tr></tbody>
</table>
</div>
<p style="font-size:11px; color:#666; text-align:center; margin-top:15px">Measurements may vary by style. For custom size, WhatsApp us.</p>
</div>
</div>

<a class="wa-float" onclick="openWA('Hi! I am interested in World Stitching products.')">💬</a>
<div class="toast" id="toast"></div>

<script>
const firebaseConfig = {apiKey:"AIzaSyB8bartyXpHSMzxpJXMO9bc7BQt0DT7ByU",authDomain:"zyron-sportswear.firebaseapp.com",databaseURL:"https://zyron-sportswear-default-rtdb.asia-southeast1.firebasedatabase.app",projectId:"zyron-sportswear",storageBucket:"zyron-sportswear.firebasestorage.app",messagingSenderId:"1055409343755",appId:"1:1055409343755:web:e6af16c4395772a9ac660e"};
firebase.initializeApp(firebaseConfig);
const database = firebase.database();

let products = [], activeCat = 'all', activeGender = 'all', selectedVariants = {}, cart = [];
let currentProduct = null, currentVariant = null, selectedSize = 'M', currentQty = 1;
let variantFields = [], isAdminLoggedIn = false;
const ADMIN_PASSWORD = 'zyronadmin123';
const catNames = {kit:'Sports Kit',trouser:'Trouser',shirt:'Shirt',jacket:'Varsity Jacket',tracksuit:'Tracksuit',summer:'Summer Wear'};

function showPage(p){ document.querySelectorAll('.page').forEach(pg=>pg.classList.remove('active')); document.getElementById(p+'Page').classList.add('active'); if(p==='home') renderProducts(); if(p==='cart') renderCartPage(); if(p==='checkout') renderCheckoutPage(); closeSlideMenu(); window.scrollTo(0,0); }
function updateCartCount(){ const c=cart.reduce((s,i)=>s+i.quantity,0); document.getElementById('cartCount').innerText=c; }
function showToast(m){ const t=document.getElementById('toast'); t.innerText=m; t.classList.add('show'); setTimeout(()=>t.classList.remove('show'),3000); }
function openWA(m){ window.open(`https://wa.me/923256054759?text=${encodeURIComponent(m)}`,'_blank'); }
function openSizeChart(){ document.getElementById('sizeChartModal').style.display='flex'; }
function closeSizeChart(){ document.getElementById('sizeChartModal').style.display='none'; }
function showSizeChart(type){
    document.getElementById('sizeTabShirt').classList.toggle('active', type === 'shirt');
    document.getElementById('sizeTabTrouser').classList.toggle('active', type === 'trouser');
    document.getElementById('shirtSizeChart').classList.toggle('active', type === 'shirt');
    document.getElementById('trouserSizeChart').classList.toggle('active', type === 'trouser');
}
function openSlideMenu(){ document.getElementById('slideMenu').classList.add('open'); document.getElementById('slideOverlay').classList.add('active'); }
function closeSlideMenu(){ document.getElementById('slideMenu').classList.remove('open'); document.getElementById('slideOverlay').classList.remove('active'); }
document.getElementById('hamburger')?.addEventListener('click',openSlideMenu);
document.getElementById('closeMenu')?.addEventListener('click',closeSlideMenu);
document.getElementById('slideOverlay')?.addEventListener('click',closeSlideMenu);
document.getElementById('adminShowBtn')?.addEventListener('click',()=>{ document.getElementById('adminPanelSection').style.display='block'; });

function checkAdminPassword(){ if(document.getElementById('adminPassword').value===ADMIN_PASSWORD){ isAdminLoggedIn=true; document.getElementById('adminPasswordBox').style.display='none'; document.getElementById('adminForm').style.display='block'; showToast('Admin access granted!'); renderManage(); } else{ document.getElementById('adminError').style.display='block'; } }
function toggleAdminPanel(){ if(!isAdminLoggedIn){ showToast('Login first'); return; } const f=document.getElementById('adminForm'), ic=document.getElementById('adminIcon'); if(f.style.display==='block'){ f.style.display='none'; ic.innerText='▼'; } else{ f.style.display='block'; ic.innerText='▲'; renderManage(); } }
function renderManage(){ if(!isAdminLoggedIn) return; const tb=document.getElementById('manageBody'); tb.innerHTML=products.map(p=>`<tr><td><strong>${p.name}</strong></td><td>${catNames[p.cat]}</td><td>${p.gender}</td><td>${p.variants?Object.keys(p.variants).length:0} colors</td><td><button class="btn-danger" onclick="deleteProduct(${p.id})" style="background:var(--logo-red);color:white;border:none;padding:5px 10px;border-radius:4px;cursor:pointer">Delete</button></td></tr>`).join(''); }
async function deleteProduct(id){ if(confirm('Delete?')){ await database.ref(`products/${id}`).remove(); loadProductsFromFirebase(); showToast('Deleted!'); } }
function addVariantField(){ variantFields.push({}); renderVariantFields(); }
function renderVariantFields(){ const c=document.getElementById('variantsContainer'); c.innerHTML=variantFields.map((_,i)=>`<div class="variant-row"><div><span>Variant ${i+1}</span><button onclick="removeVariantField(${i})" style="float:right;background:var(--logo-red);color:white;border:none;padding:2px 10px;border-radius:4px">X</button></div><div class="form-row"><div class="form-group"><label>Color</label><input id="varColor_${i}" placeholder="Red"></div><div class="form-group"><label>Code</label><input id="varCode_${i}" placeholder="#DC2626"></div></div><div class="form-row"><div class="form-group"><label>Image URL</label><input id="varImage_${i}" placeholder="https://i.imgur.com/xxx.jpg"></div><div class="form-group"><label>Sale %</label><input id="varSale_${i}" type="number" placeholder="0"></div></div></div>`).join(''); }
function removeVariantField(i){ variantFields.splice(i,1); renderVariantFields(); }
async function addProductToFirebase(){ if(!isAdminLoggedIn){ showToast('Admin login required'); return; } const name=document.getElementById('pName').value.trim(); const price=parseInt(document.getElementById('pPrice').value); const cat=document.getElementById('pCat').value; const gender=document.getElementById('pGender').value; const desc=document.getElementById('pDesc').value.trim(); if(!name||!price){ showToast('Name and price required'); return; } if(variantFields.length===0){ showToast('Add color variant'); return; } const variants={}; for(let i=0;i<variantFields.length;i++){ const col=document.getElementById(`varColor_${i}`).value; if(!col){ showToast(`Color for variant ${i+1} required`); return; } variants[i]={ color:col, colorCode:document.getElementById(`varCode_${i}`).value||'#CCCCCC', image:document.getElementById(`varImage_${i}`).value, sale:parseInt(document.getElementById(`varSale_${i}`).value)||0, sizes:['S','M','L','XL','XXL'] }; } const existing=await database.ref('products').once('value'); let maxId=0; if(existing.val()) maxId=Math.max(...Object.keys(existing.val()).map(Number)); const newId=maxId+1; await database.ref(`products/${newId}`).set({ id:newId, name, cat, gender, description:desc||'Premium quality', originalPrice:price, trending:false, variants }); showToast('Product added!'); document.getElementById('pName').value=''; document.getElementById('pPrice').value=''; document.getElementById('pDesc').value=''; variantFields=[]; renderVariantFields(); loadProductsFromFirebase(); }

const defaultProducts = [
{id:1,name:'Elite Strike Football Jersey',cat:'kit',gender:'men',description:'Premium moisture-wicking fabric',originalPrice:3500,trending:true,variants:{0:{color:'Red',colorCode:'#DC2626',image:'https://images.unsplash.com/photo-1566577739112-5180d4bf9390?w=400',sale:25,sizes:['S','M','L','XL','XXL']},1:{color:'Navy',colorCode:'#1a1a1a',image:'https://images.unsplash.com/photo-1574629810360-7efbbe195018?w=400',sale:0,sizes:['S','M','L','XL','XXL']}}},
{id:2,name:'Pro Cricket Kit',cat:'kit',gender:'men',description:'Professional cricket uniform',originalPrice:4200,trending:false,variants:{0:{color:'Blue',colorCode:'#1a3460',image:'https://images.unsplash.com/photo-1531415074968-036ba1b575da?w=400',sale:15,sizes:['S','M','L','XL','XXL']},1:{color:'Green',colorCode:'#16A34A',image:'https://images.unsplash.com/photo-1518611012118-696072aa579a?w=400',sale:0,sizes:['S','M','L','XL','XXL']}}},
{id:3,name:'Varsity Heritage Jacket',cat:'jacket',gender:'uni',description:'Classic letterman jacket',originalPrice:6800,trending:true,variants:{0:{color:'Maroon',colorCode:'#8B1A1A',image:'https://images.unsplash.com/photo-1591047139829-d91aecb6caea?w=400',sale:30,sizes:['S','M','L','XL','XXL']},1:{color:'Black',colorCode:'#1A1A1A',image:'https://images.unsplash.com/photo-1551028714-9a1f1f3d8c1d?w=400',sale:20,sizes:['S','M','L','XL','XXL']}}},
{id:4,name:'Elite Tracksuit',cat:'tracksuit',gender:'men',description:'Full tracksuit set',originalPrice:4200,trending:false,variants:{0:{color:'Navy',colorCode:'#1a1a1a',image:'https://images.unsplash.com/photo-1556906781-9a412961c28c?w=400',sale:20,sizes:['S','M','L','XL','XXL']},1:{color:'Red',colorCode:'#DC2626',image:'https://images.unsplash.com/photo-1576566588028-4147f3842f27?w=400',sale:0,sizes:['S','M','L','XL','XXL']}}},
{id:5,name:'Women Active Top',cat:'shirt',gender:'women',description:'Stretchable performance',originalPrice:2000,trending:true,variants:{0:{color:'Pink',colorCode:'#E8829A',image:'https://images.unsplash.com/photo-1518611012118-696072aa579a?w=400',sale:20,sizes:['S','M','L','XL']},1:{color:'Black',colorCode:'#1A1A1A',image:'https://images.unsplash.com/photo-1556906781-9a412961c28c?w=400',sale:0,sizes:['S','M','L','XL']}}},
{id:6,name:'Girls Summer Top',cat:'summer',gender:'girls',description:'Lightweight top',originalPrice:1200,trending:false,variants:{0:{color:'Lavender',colorCode:'#C084FC',image:'https://images.unsplash.com/photo-1515488042361-ee00e0ddd4e4?w=400',sale:0,sizes:['XS','S','M','L']},1:{color:'Peach',colorCode:'#FDBA74',image:'https://images.unsplash.com/photo-1531415074968-036ba1b575da?w=400',sale:15,sizes:['XS','S','M','L']}}},
{id:7,name:'Boys Champion Kit',cat:'kit',gender:'boys',description:'Complete kids kit',originalPrice:2500,trending:true,variants:{0:{color:'Blue',colorCode:'#1a3460',image:'https://images.unsplash.com/photo-1574629810360-7efbbe195018?w=400',sale:0,sizes:['XS','S','M','L']},1:{color:'Red',colorCode:'#DC2626',image:'https://images.unsplash.com/photo-1566577739112-5180d4bf9390?w=400',sale:20,sizes:['XS','S','M','L']}}}
];

function loadProductsFromFirebase(){ database.ref('products').on('value',(snap)=>{ const d=snap.val(); if(d&&Object.keys(d).length>0) products=Object.values(d); else{ products=[...defaultProducts]; products.forEach(p=>database.ref(`products/${p.id}`).set(p)); } products.forEach(p=>{ if(selectedVariants[p.id]===undefined) selectedVariants[p.id]=0; }); renderProducts(); updateCartCount(); if(isAdminLoggedIn) renderManage(); }); }
function getFinalPrice(o,s){ return s>0 ? Math.round(o-(o*s/100)) : o; }
function renderProducts(){ const grid=document.getElementById('productsGrid'); let filtered=products.filter(p=> (activeCat==='all'||p.cat===activeCat) && (activeGender==='all'||p.gender===activeGender||p.gender==='uni')); if(filtered.length===0){ grid.innerHTML='<div style="text-align:center;padding:60px;color:var(--text-light)"><i class="fas fa-box-open" style="font-size:50px;margin-bottom:15px;display:block"></i>No products in this category.<br>Try another selection.</div>'; return; } grid.innerHTML=filtered.map(p=>{ const idx=selectedVariants[p.id]||0; const vars=Object.values(p.variants); const v=vars[idx]; const hs=v.sale>0; const fp=getFinalPrice(p.originalPrice,v.sale); return `<div class="product-card" onclick="viewProduct(${p.id})"><div class="product-img"><img src="${v.image}" onerror="this.src='https://placehold.co/400x400/1a1a1a/b0b0b0?text=${p.name}'">${hs?`<div class="sale-badge">${v.sale}% OFF</div>`:''}${p.trending&&!hs?`<div class="trending-badge">🔥 TRENDING</div>`:''}</div><div class="product-body"><div class="product-cat">${catNames[p.cat]} • ${p.gender==='uni'?'Unisex':p.gender.charAt(0).toUpperCase()+p.gender.slice(1)}</div><div class="product-name">${p.name}</div><div class="product-desc">${p.description}</div><div class="color-variants">${vars.map((c,i)=>`<div class="color-dot ${i===idx?'active':''}" style="background:${c.colorCode};" onclick="event.stopPropagation(); selectVariant(${p.id},${i})" title="${c.color}"></div>`).join('')}</div><div class="price-row">${hs?`<span class="original-price">PKR ${p.originalPrice.toLocaleString()}</span><span class="sale-price">PKR ${fp.toLocaleString()}</span>`:`<span class="normal-price">PKR ${fp.toLocaleString()}</span>`}</div></div></div>`; }).join(''); }
function selectVariant(pid,idx){ selectedVariants[pid]=idx; renderProducts(); }
function filterCat(cat,el){ activeCat=cat; document.querySelectorAll('.cat-tab').forEach(t=>t.classList.remove('active')); if(el) el.classList.add('active'); renderProducts(); closeSlideMenu(); }
function filterGender(gender,el){ activeGender=gender; document.querySelectorAll('.gender-tab').forEach(t=>t.classList.remove('active')); if(el) el.classList.add('active'); renderProducts(); closeSlideMenu(); }

function viewProduct(id){ const p=products.find(p=>p.id===id); if(!p) return; currentProduct=p; currentVariant=Object.values(p.variants)[0]; selectedSize=currentVariant.sizes?.[0]||'M'; currentQty=1; renderProductDetail(); showPage('product'); }
function renderProductDetail(){ const hs=currentVariant.sale>0; const sp=hs?Math.round(currentProduct.originalPrice-(currentProduct.originalPrice*currentVariant.sale/100)):currentProduct.originalPrice; const vars=Object.values(currentProduct.variants); const related=products.filter(p=>p.id!==currentProduct.id && p.cat===currentProduct.cat).slice(0,4); document.getElementById('productDetailContainer').innerHTML=`<div class="product-detail"><div class="product-detail-img"><img id="detailMainImg" src="${currentVariant.image}" onerror="this.src='https://placehold.co/600x600/1a1a1a/b0b0b0?text=${currentProduct.name}'"></div><div><h1 class="product-detail-title">${currentProduct.name}</h1><div class="product-detail-price">${hs?`<s>PKR ${currentProduct.originalPrice.toLocaleString()}</s> PKR ${sp.toLocaleString()}`:`PKR ${currentProduct.originalPrice.toLocaleString()}`}</div><div class="product-detail-desc">${currentProduct.description}</div><div class="detail-section-title">SIZE</div><div class="detail-size-options" id="detailSizeOptions"></div><div class="detail-section-title">COLOR</div><div class="detail-color-options" id="detailColorOptions"></div><div class="detail-section-title">QUANTITY</div><div class="detail-qty-selector"><button class="detail-qty-btn" onclick="changeDetailQty(-1)">-</button><input type="text" id="detailQty" value="1" class="detail-qty-input" readonly><button class="detail-qty-btn" onclick="changeDetailQty(1)">+</button></div><div class="detail-stock-info"><i class="fas fa-check-circle" style="color:var(--logo-silver)"></i> In Stock — Order aaj hi karein!</div><div class="detail-action-buttons"><button class="detail-btn-add-cart" onclick="addToCartFromDetail()"><i class="fas fa-shopping-bag"></i> ADD TO CART</button><button class="detail-btn-buy-now" onclick="buyNowFromDetail()"><i class="fab fa-whatsapp"></i> BUY NOW</button><button class="sizechart-btn" onclick="openSizeChart()"><i class="fas fa-chart-simple"></i> Size Chart</button></div></div></div><div class="related-products"><h3 style="text-align:center;margin-bottom:20px">YOU MAY ALSO LIKE</h3><div class="related-grid" id="detailRelatedGrid"></div></div>`; const colorContainer=document.getElementById('detailColorOptions'); if(colorContainer) colorContainer.innerHTML=vars.map((v,i)=>`<div class="detail-color-option ${i===0?'active':''}" style="background:${v.colorCode};" onclick="selectDetailColor(${i})" title="${v.color}"></div>`).join(''); const sizeContainer=document.getElementById('detailSizeOptions'); if(sizeContainer) sizeContainer.innerHTML=(currentVariant.sizes||['S','M','L','XL','XXL']).map(s=>`<div class="detail-size-btn ${s===selectedSize?'active':''}" onclick="selectDetailSize(this,'${s}')">${s}</div>`).join(''); const relatedGrid=document.getElementById('detailRelatedGrid'); if(relatedGrid) relatedGrid.innerHTML=related.map(p=>{ const fv=Object.values(p.variants)[0]; const price=fv.sale>0?Math.round(p.originalPrice-(p.originalPrice*fv.sale/100)):p.originalPrice; return `<div class="related-card" onclick="viewProduct(${p.id})"><img src="${fv.image}"><h4>${p.name}</h4><p>PKR ${price.toLocaleString()}</p></div>`; }).join(''); }
function selectDetailColor(i){ document.querySelectorAll('.detail-color-option').forEach((btn,idx)=>btn.classList.toggle('active',idx===i)); currentVariant=Object.values(currentProduct.variants)[i]; selectedSize=currentVariant.sizes?.[0]||'M'; const hs=currentVariant.sale>0; const sp=hs?Math.round(currentProduct.originalPrice-(currentProduct.originalPrice*currentVariant.sale/100)):currentProduct.originalPrice; document.getElementById('detailMainImg').src=currentVariant.image; const priceDiv=document.querySelector('.product-detail-price'); if(priceDiv) priceDiv.innerHTML=hs?`<s>PKR ${currentProduct.originalPrice.toLocaleString()}</s> PKR ${sp.toLocaleString()}`:`PKR ${currentProduct.originalPrice.toLocaleString()}`; const sizeContainer=document.getElementById('detailSizeOptions'); if(sizeContainer) sizeContainer.innerHTML=(currentVariant.sizes||['S','M','L','XL','XXL']).map(s=>`<div class="detail-size-btn ${s===selectedSize?'active':''}" onclick="selectDetailSize(this,'${s}')">${s}</div>`).join(''); }
function selectDetailSize(el,s){ document.querySelectorAll('.detail-size-btn').forEach(btn=>btn.classList.remove('active')); el.classList.add('active'); selectedSize=s; }
function changeDetailQty(d){ let n=currentQty+d; if(n>=1 && n<=10){ currentQty=n; document.getElementById('detailQty').value=currentQty; } }
function addToCartFromDetail(){ const sp=currentVariant.sale>0?Math.round(currentProduct.originalPrice-(currentProduct.originalPrice*currentVariant.sale/100)):currentProduct.originalPrice; const idx=cart.findIndex(i=>i.id===currentProduct.id && i.color===currentVariant.color && i.size===selectedSize); if(idx>-1) cart[idx].quantity+=currentQty; else cart.push({id:currentProduct.id,name:currentProduct.name,color:currentVariant.color,size:selectedSize,quantity:currentQty,image:currentVariant.image,price:currentProduct.originalPrice,salePrice:sp}); localStorage.setItem('ws_cart',JSON.stringify(cart)); updateCartCount(); showToast('✅ Added to cart!'); }
function buyNowFromDetail(){ addToCartFromDetail(); showPage('cart'); renderCartPage(); }
function renderCartPage(){ if(cart.length===0){ document.getElementById('cartContainer').innerHTML=`<div style="text-align:center;padding:60px"><i class="fas fa-shopping-bag" style="font-size:60px;color:#ddd"></i><p>Cart empty</p><button class="btn-primary" onclick="showPage('home')">Shop Now</button></div>`; return; } let sub=0; cart.forEach(i=>{ const p=i.salePrice||i.price; sub+=p*i.quantity; }); const ship=sub>=5000?0:299; const total=sub+ship; document.getElementById('cartContainer').innerHTML=`<div class="cart-grid"><div class="cart-items"><div class="cart-header"><div>PRODUCT</div><div>PRICE</div><div>QTY</div><div>TOTAL</div></div>${cart.map((i,idx)=>{ const p=i.salePrice||i.price; const tp=p*i.quantity; return `<div class="cart-item"><div class="cart-item-info"><img src="${i.image}"><div><h4>${i.name}</h4><p>${i.color} / ${i.size}</p></div></div><div>PKR ${p.toLocaleString()}</div><div><button class="cart-qty-btn" onclick="updateCartQty(${idx},-1)">-</button><span>${i.quantity}</span><button class="cart-qty-btn" onclick="updateCartQty(${idx},1)">+</button></div><div>PKR ${tp.toLocaleString()}</div><div class="cart-remove" onclick="removeCartItem(${idx})"><i class="fas fa-trash"></i></div></div>`; }).join('')}</div><div class="cart-summary"><h3>Order Summary</h3><div class="summary-row"><span>Subtotal</span><span>PKR ${sub.toLocaleString()}</span></div><div class="summary-row"><span>Shipping</span><span>${ship===0?'FREE 🎉':'PKR '+ship.toLocaleString()}</span></div><div class="summary-row summary-total"><span>Total</span><span>PKR ${total.toLocaleString()}</span></div><button class="btn-primary" style="width:100%" onclick="showPage('checkout');renderCheckoutPage()">Checkout</button><p style="font-size:12px;margin-top:15px;color:var(--text-light)">🎉 PKR 5000 se upar free shipping!</p></div></div>`; updateCartCount(); }
function updateCartQty(idx,d){ let n=cart[idx].quantity+d; if(n>=1 && n<=10){ cart[idx].quantity=n; localStorage.setItem('ws_cart',JSON.stringify(cart)); renderCartPage(); } else if(n<1) removeCartItem(idx); }
function removeCartItem(idx){ cart.splice(idx,1); localStorage.setItem('ws_cart',JSON.stringify(cart)); renderCartPage(); updateCartCount(); }
function renderCheckoutPage(){ if(cart.length===0){ showPage('cart'); return; } let sub=0; cart.forEach(i=>{ const p=i.salePrice||i.price; sub+=p*i.quantity; }); const ship=sub>=5000?0:299; const total=sub+ship; document.getElementById('checkoutContainer').innerHTML=`<div class="checkout-grid"><div class="checkout-form"><h2 class="form-title">Shipping Info</h2><div class="form-row"><div class="form-group"><label>First Name</label><input id="chFName"></div><div class="form-group"><label>Last Name</label><input id="chLName"></div></div><div class="form-group"><label>Email</label><input id="chEmail"></div><div class="form-group"><label>Phone</label><input id="chPhone"></div><div class="form-group"><label>Address</label><input id="chAddress"></div><div class="form-row"><div class="form-group"><label>City</label><input id="chCity" value="Faisalabad"></div><div class="form-group"><label>Postal Code</label><input id="chPostal"></div></div><div class="jazzcash-box"><i class="fab fa-whatsapp"></i><h3>0320 9606000</h3><p>Send payment to JazzCash</p><p class="small">After payment, send screenshot on WhatsApp</p></div><div class="form-group"><label><input type="checkbox" id="chSaveInfo"> Save info</label></div></div><div class="order-summary"><h2>Order Summary</h2>${cart.map(i=>{ const p=i.salePrice||i.price; return `<div class="cart-item"><img class="cart-item-img" src="${i.image}"><div><h4>${i.name}</h4><p>${i.color} / ${i.size} / Qty: ${i.quantity}</p><div>PKR ${(p*i.quantity).toLocaleString()}</div></div></div>`; }).join('')}<div class="summary-row"><span>Subtotal</span><span>PKR ${sub.toLocaleString()}</span></div><div class="summary-row"><span>Shipping</span><span>${ship===0?'FREE':'PKR '+ship.toLocaleString()}</span></div><div class="summary-row summary-total"><span>Total</span><span>PKR ${total.toLocaleString()}</span></div><button class="btn-primary" style="width:100%" onclick="placeOrder()">Confirm Order via WhatsApp</button><a href="#" class="back-link" onclick="showPage('cart');return false">← Back</a></div></div>`; loadSavedCheckoutInfo(); }
function placeOrder(){ if(cart.length===0){ alert('Cart empty'); return; } const fn=document.getElementById('chFName').value, ln=document.getElementById('chLName').value, em=document.getElementById('chEmail').value, ph=document.getElementById('chPhone').value, ad=document.getElementById('chAddress').value, ct=document.getElementById('chCity').value; if(!fn||!ln||!em||!ph||!ad||!ct){ alert('Fill all details'); return; } let sub=0; cart.forEach(i=>{ const p=i.salePrice||i.price; sub+=p*i.quantity; }); const ship=sub>=5000?0:299; const total=sub+ship; let msg=`🏆 *WORLD STITCHING ORDER* 🏆%0A%0A*Customer*%0A${fn} ${ln}%0A${em}%0A${ph}%0A${ad}, ${ct}%0A%0A*Items*%0A`; cart.forEach(i=>{ const p=i.salePrice||i.price; msg+=`📦 ${i.name} (${i.color}/${i.size}) x${i.quantity} = PKR ${(p*i.quantity).toLocaleString()}%0A`; }); msg+=`%0A*Total*: PKR ${total.toLocaleString()}%0A%0A*Payment*: JazzCash 0320 9606000%0A📍 Faisalabad, Pakistan%0A🙏 Thank you!`; window.open(`https://wa.me/923256054759?text=${encodeURIComponent(msg)}`,'_blank'); if(document.getElementById('chSaveInfo').checked){ const info={firstName:fn,lastName:ln,email:em,phone:ph,address:ad,city:ct}; localStorage.setItem('ws_shipping',JSON.stringify(info)); } cart=[]; localStorage.setItem('ws_cart',JSON.stringify(cart)); updateCartCount(); showToast('Order placed!'); showPage('home'); }
function loadSavedCheckoutInfo(){ const saved=localStorage.getItem('ws_shipping'); if(saved){ const i=JSON.parse(saved); document.getElementById('chFName').value=i.firstName||''; document.getElementById('chLName').value=i.lastName||''; document.getElementById('chEmail').value=i.email||''; document.getElementById('chPhone').value=i.phone||''; document.getElementById('chAddress').value=i.address||''; document.getElementById('chCity').value=i.city||'Faisalabad'; } }
function loadCart(){ const saved=localStorage.getItem('ws_cart'); cart=saved?JSON.parse(saved):[]; updateCartCount(); }
loadCart(); loadProductsFromFirebase();
</script>
</body>
</html>
