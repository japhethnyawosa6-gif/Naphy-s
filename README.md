<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LUXE & CO | Personalized Gifts & Accessories</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;500;600;700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #1a1a1a;
            --accent: #d4af37;
            --accent-hover: #b8960c;
            --soft-bg: #faf9f6;
        }
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--soft-bg);
        }
        
        h1, h2, h3, h4, .serif {
            font-family: 'Playfair Display', serif;
        }
        
        /* Smooth scrolling */
        html {
            scroll-behavior: smooth;
        }
        
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        ::-webkit-scrollbar-thumb {
            background: var(--accent);
            border-radius: 4px;
        }
        
        /* Animations */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }
        
        @keyframes shimmer {
            0% { background-position: -1000px 0; }
            100% { background-position: 1000px 0; }
        }
        
        .animate-fade-in-up {
            animation: fadeInUp 0.8s ease-out forwards;
        }
        
        .animate-float {
            animation: float 3s ease-in-out infinite;
        }
        
        /* Glass morphism */
        .glass {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.3);
        }
        
        .glass-dark {
            background: rgba(26, 26, 26, 0.9);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
        }
        
        /* Hover effects */
        .hover-lift {
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .hover-lift:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
        }
        
        /* Image hover zoom */
        .img-zoom {
            overflow: hidden;
        }
        .img-zoom img {
            transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .img-zoom:hover img {
            transform: scale(1.08);
        }
        
        /* Customization panel */
        .customization-panel {
            transition: all 0.3s ease;
        }
        
        /* Cart sidebar */
        .cart-sidebar {
            transform: translateX(100%);
            transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .cart-sidebar.open {
            transform: translateX(0);
        }
        
        /* Loading shimmer */
        .shimmer {
            background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
            background-size: 1000px 100%;
            animation: shimmer 2s infinite linear;
        }
        
        /* Text gradient */
        .text-gradient {
            background: linear-gradient(135deg, #d4af37 0%, #f4d03f 50%, #d4af37 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        /* Custom radio buttons for customization */
        .custom-radio:checked + div {
            border-color: var(--accent);
            background-color: rgba(212, 175, 55, 0.1);
        }
        
        /* Parallax effect */
        .parallax {
            background-attachment: fixed;
            background-position: center;
            background-repeat: no-repeat;
            background-size: cover;
        }
        
        /* Mobile menu */
        .mobile-menu {
            transform: translateX(-100%);
            transition: transform 0.3s ease;
        }
        .mobile-menu.open {
            transform: translateX(0);
        }
        
        /* Notification toast */
        .toast {
            transform: translateY(100px);
            opacity: 0;
            transition: all 0.4s ease;
        }
        .toast.show {
            transform: translateY(0);
            opacity: 1;
        }
    </style>
</head>
<body class="antialiased text-gray-800">

    <!-- Navigation -->
    <nav id="navbar" class="fixed w-full z-50 transition-all duration-300 bg-transparent">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center h-20">
                <!-- Logo -->
                <div class="flex-shrink-0 flex items-center cursor-pointer" onclick="window.scrollTo(0,0)">
                    <span class="serif text-2xl font-bold tracking-wider text-white" id="nav-logo">LUXE & CO</span>
                </div>
                
                <!-- Desktop Menu -->
                <div class="hidden md:flex items-center space-x-8">
                    <a href="#bags" class="text-white hover:text-yellow-400 transition-colors text-sm tracking-wide uppercase">Bags</a>
                    <a href="#bottles" class="text-white hover:text-yellow-400 transition-colors text-sm tracking-wide uppercase">Bottles & Hats</a>
                    <a href="#baskets" class="text-white hover:text-yellow-400 transition-colors text-sm tracking-wide uppercase">Gift Baskets</a>
                    <a href="#bracelets" class="text-white hover:text-yellow-400 transition-colors text-sm tracking-wide uppercase">Bracelets</a>
                </div>
                
                <!-- Icons -->
                <div class="flex items-center space-x-6">
                    <button class="text-white hover:text-yellow-400 transition-colors">
                        <i class="fas fa-search text-lg"></i>
                    </button>
                    <button class="text-white hover:text-yellow-400 transition-colors relative" onclick="toggleCart()">
                        <i class="fas fa-shopping-bag text-lg"></i>
                        <span id="cart-count" class="absolute -top-2 -right-2 bg-yellow-500 text-white text-xs rounded-full h-5 w-5 flex items-center justify-center font-semibold">0</span>
                    </button>
                    <button class="md:hidden text-white" onclick="toggleMobileMenu()">
                        <i class="fas fa-bars text-xl"></i>
                    </button>
                </div>
            </div>
        </div>
    </nav>

    <!-- Mobile Menu -->
    <div id="mobile-menu" class="mobile-menu fixed inset-0 z-50 bg-black bg-opacity-95 md:hidden">
        <div class="p-8">
            <button onclick="toggleMobileMenu()" class="text-white float-right">
                <i class="fas fa-times text-2xl"></i>
            </button>
            <div class="mt-12 space-y-6">
                <a href="#bags" onclick="toggleMobileMenu()" class="block text-white text-2xl serif">Bags</a>
                <a href="#bottles" onclick="toggleMobileMenu()" class="block text-white text-2xl serif">Bottles & Hats</a>
                <a href="#baskets" onclick="toggleMobileMenu()" class="block text-white text-2xl serif">Gift Baskets</a>
                <a href="#bracelets" onclick="toggleMobileMenu()" class="block text-white text-2xl serif">Bracelets</a>
            </div>
        </div>
    </div>

    <!-- Hero Section -->
    <section class="relative h-screen flex items-center justify-center overflow-hidden">
        <div class="absolute inset-0 z-0">
            <img src="https://images.unsplash.com/photo-1441986300917-64674bd600d8?w=1920&q=80" alt="Luxury gifts" class="w-full h-full object-cover">
            <div class="absolute inset-0 bg-gradient-to-b from-black/60 via-black/40 to-black/60"></div>
        </div>
        
        <div class="relative z-10 text-center px-4 max-w-5xl mx-auto">
            <p class="text-yellow-400 text-sm tracking-[0.3em] uppercase mb-4 animate-fade-in-up" style="animation-delay: 0.1s">Est. 2024</p>
            <h1 class="serif text-5xl md:text-7xl lg:text-8xl text-white font-medium mb-6 leading-tight animate-fade-in-up" style="animation-delay: 0.2s">
                Gifts That Tell<br><span class="text-gradient italic">Your Story</span>
            </h1>
            <p class="text-gray-200 text-lg md:text-xl max-w-2xl mx-auto mb-10 font-light animate-fade-in-up" style="animation-delay: 0.3s">
                Exquisite personalized bags, engraved bracelets, custom bottles with matching hats, and curated gift baskets for every occasion.
            </p>
            <div class="flex flex-col sm:flex-row gap-4 justify-center animate-fade-in-up" style="animation-delay: 0.4s">
                <a href="#collections" class="px-8 py-4 bg-yellow-500 text-black font-semibold rounded-full hover:bg-yellow-400 transition-all transform hover:scale-105">
                    Explore Collections
                </a>
                <a href="#customize" class="px-8 py-4 border-2 border-white text-white font-semibold rounded-full hover:bg-white hover:text-black transition-all">
                    Customize Now
                </a>
            </div>
        </div>
        
        <div class="absolute bottom-10 left-1/2 transform -translate-x-1/2 animate-float">
            <i class="fas fa-chevron-down text-white text-2xl opacity-70"></i>
        </div>
    </section>

    <!-- Features Bar -->
    <section class="bg-white py-12 border-b border-gray-100">
        <div class="max-w-7xl mx-auto px-4 grid grid-cols-2 md:grid-cols-4 gap-8 text-center">
            <div class="hover-lift p-4">
                <i class="fas fa-shipping-fast text-3xl text-yellow-500 mb-3"></i>
                <h3 class="font-semibold text-sm uppercase tracking-wide">Free Shipping</h3>
                <p class="text-gray-500 text-xs mt-1">On orders over $75</p>
            </div>
            <div class="hover-lift p-4">
                <i class="fas fa-gem text-3xl text-yellow-500 mb-3"></i>
                <h3 class="font-semibold text-sm uppercase tracking-wide">Premium Quality</h3>
                <p class="text-gray-500 text-xs mt-1">Handcrafted with care</p>
            </div>
            <div class="hover-lift p-4">
                <i class="fas fa-pen-fancy text-3xl text-yellow-500 mb-3"></i>
                <h3 class="font-semibold text-sm uppercase tracking-wide">Free Personalization</h3>
                <p class="text-gray-500 text-xs mt-1">Names & messages</p>
            </div>
            <div class="hover-lift p-4">
                <i class="fas fa-undo text-3xl text-yellow-500 mb-3"></i>
                <h3 class="font-semibold text-sm uppercase tracking-wide">Easy Returns</h3>
                <p class="text-gray-500 text-xs mt-1">30-day guarantee</p>
            </div>
        </div>
    </section>

    <!-- Collections Section -->
    <section id="collections" class="py-20 bg-white">
        <div class="max-w-7xl mx-auto px-4">
            <div class="text-center mb-16">
                <p class="text-yellow-600 text-sm tracking-[0.2em] uppercase mb-2">Curated Selection</p>
                <h2 class="serif text-4xl md:text-5xl text-gray-900 mb-4">Our Collections</h2>
                <div class="w-24 h-1 bg-yellow-400 mx-auto"></div>
            </div>

            <!-- Category Tabs -->
            <div class="flex flex-wrap justify-center gap-4 mb-12">
                <button onclick="filterProducts('all')" class="category-btn active px-6 py-2 rounded-full border-2 border-gray-900 bg-gray-900 text-white text-sm font-medium transition-all" data-category="all">All</button>
                <button onclick="filterProducts('bags')" class="category-btn px-6 py-2 rounded-full border-2 border-gray-300 text-gray-700 hover:border-gray-900 hover:text-gray-900 text-sm font-medium transition-all" data-category="bags">Bags</button>
                <button onclick="filterProducts('bottles')" class="category-btn px-6 py-2 rounded-full border-2 border-gray-300 text-gray-700 hover:border-gray-900 hover:text-gray-900 text-sm font-medium transition-all" data-category="bottles">Bottles & Hats</button>
                <button onclick="filterProducts('baskets')" class="category-btn px-6 py-2 rounded-full border-2 border-gray-300 text-gray-700 hover:border-gray-900 hover:text-gray-900 text-sm font-medium transition-all" data-category="baskets">Gift Baskets</button>
                <button onclick="filterProducts('bracelets')" class="category-btn px-6 py-2 rounded-full border-2 border-gray-300 text-gray-700 hover:border-gray-900 hover:text-gray-900 text-sm font-medium transition-all" data-category="bracelets">Bracelets</button>
            </div>

            <!-- Products Grid -->
            <div id="products-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8">
                <!-- Products will be injected here by JavaScript -->
            </div>
        </div>
    </section>

    <!-- Customization Showcase -->
    <section id="customize" class="py-20 bg-gray-50">
        <div class="max-w-7xl mx-auto px-4">
            <div class="grid md:grid-cols-2 gap-12 items-center">
                <div class="relative">
                    <div class="absolute -top-4 -left-4 w-24 h-24 bg-yellow-400 rounded-full opacity-20"></div>
                    <div class="absolute -bottom-4 -right-4 w-32 h-32 bg-gray-900 rounded-full opacity-10"></div>
                    <img src="https://images.unsplash.com/photo-1611591437281-460bfbe1220a?w=800&q=80" alt="Personalization" class="relative rounded-2xl shadow-2xl w-full object-cover h-[500px]">
                    <div class="absolute bottom-8 left-8 bg-white p-6 rounded-lg shadow-xl max-w-xs">
                        <i class="fas fa-magic text-yellow-500 text-2xl mb-2"></i>
                        <p class="serif text-lg font-medium">"Every gift tells a story. What's yours?"</p>
                    </div>
                </div>
                <div>
                    <p class="text-yellow-600 text-sm tracking-[0.2em] uppercase mb-2">Make It Yours</p>
                    <h2 class="serif text-4xl md:text-5xl text-gray-900 mb-6">Personalization<br>Perfection</h2>
                    <p class="text-gray-600 mb-8 leading-relaxed">
                        Transform ordinary gifts into extraordinary memories. Add names, initials, special dates, or meaningful messages to create truly unique pieces that will be treasured forever.
                    </p>
                    
                    <div class="space-y-4 mb-8">
                        <div class="flex items-start gap-4">
                            <div class="w-12 h-12 bg-yellow-100 rounded-full flex items-center justify-center flex-shrink-0">
                                <i class="fas fa-font text-yellow-600"></i>
                            </div>
                            <div>
                                <h4 class="font-semibold text-gray-900">Custom Engraving</h4>
                                <p class="text-gray-600 text-sm">Precision laser engraving on bracelets, bottles, and accessories</p>
                            </div>
                        </div>
                        <div class="flex items-start gap-4">
                            <div class="w-12 h-12 bg-yellow-100 rounded-full flex items-center justify-center flex-shrink-0">
                                <i class="fas fa-palette text-yellow-600"></i>
                            </div>
                            <div>
                                <h4 class="font-semibold text-gray-900">Color Selection</h4>
                                <p class="text-gray-600 text-sm">Choose from 20+ colors for bottles, hats, and bag accessories</p>
                            </div>
                        </div>
                        <div class="flex items-start gap-4">
                            <div class="w-12 h-12 bg-yellow-100 rounded-full flex items-center justify-center flex-shrink-0">
                                <i class="fas fa-gift text-yellow-600"></i>
                            </div>
                            <div>
                                <h4 class="font-semibold text-gray-900">Gift Packaging</h4>
                                <p class="text-gray-600 text-sm">Premium gift boxes with handwritten message cards</p>
                            </div>
                        </div>
                    </div>
                    
                    <button onclick="scrollToSection('collections')" class="px-8 py-4 bg-gray-900 text-white font-semibold rounded-full hover:bg-gray-800 transition-all transform hover:scale-105 inline-flex items-center gap-2">
                        Start Customizing <i class="fas fa-arrow-right"></i>
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- Gift Baskets Highlight -->
    <section id="baskets" class="py-20 bg-gray-900 text-white relative overflow-hidden">
        <div class="absolute inset-0 opacity-20">
            <img src="https://images.unsplash.com/photo-1549465220-1a8b9238cd48?w=1920&q=80" alt="Gift baskets" class="w-full h-full object-cover">
        </div>
        <div class="max-w-7xl mx-auto px-4 relative z-10">
            <div class="text-center mb-12">
                <p class="text-yellow-400 text-sm tracking-[0.2em] uppercase mb-2">Curated With Love</p>
                <h2 class="serif text-4xl md:text-5xl mb-4">Luxury Gift Baskets</h2>
                <p class="text-gray-400 max-w-2xl mx-auto">Thoughtfully curated collections for every occasion. From spa retreats to gourmet delights, each basket is a journey of discovery.</p>
            </div>
            
            <div class="grid md:grid-cols-3 gap-8">
                <div class="glass-dark p-8 rounded-2xl hover-lift border border-gray-700">
                    <div class="w-16 h-16 bg-yellow-500/20 rounded-full flex items-center justify-center mb-6">
                        <i class="fas fa-spa text-yellow-400 text-2xl"></i>
                    </div>
                    <h3 class="serif text-2xl mb-3">Spa & Relaxation</h3>
                    <p class="text-gray-400 mb-6">Artisanal soaps, bath bombs, candles, and plush towels for the ultimate relaxation experience.</p>
                    <p class="text-yellow-400 font-semibold text-xl mb-4">From $89</p>
                    <button onclick="addToCart({id: 'basket1', name: 'Spa & Relaxation Basket', price: 89, image: 'https://images.unsplash.com/photo-1540555700478-4be289fbecef?w=400&q=80'})" class="w-full py-3 border border-yellow-400 text-yellow-400 rounded-full hover:bg-yellow-400 hover:text-gray-900 transition-all">
                        Add to Cart
                    </button>
                </div>
                
                <div class="glass-dark p-8 rounded-2xl hover-lift border border-gray-700 transform md:-translate-y-4">
                    <div class="absolute -top-4 left-1/2 transform -translate-x-1/2 bg-yellow-500 text-gray-900 text-xs font-bold px-4 py-1 rounded-full">BESTSELLER</div>
                    <div class="w-16 h-16 bg-yellow-500/20 rounded-full flex items-center justify-center mb-6">
                        <i class="fas fa-wine-glass-alt text-yellow-400 text-2xl"></i>
                    </div>
                    <h3 class="serif text-2xl mb-3">Gourmet Delight</h3>
                    <p class="text-gray-400 mb-6">Fine wines, artisanal cheeses, luxury chocolates, and gourmet snacks for the connoisseur.</p>
                    <p class="text-yellow-400 font-semibold text-xl mb-4">From $149</p>
                    <button onclick="addToCart({id: 'basket2', name: 'Gourmet Delight Basket', price: 149, image: 'https://images.unsplash.com/photo-1549465220-1a8b9238cd48?w=400&q=80'})" class="w-full py-3 bg-yellow-500 text-gray-900 rounded-full hover:bg-yellow-400 transition-all font-semibold">
                        Add to Cart
                    </button>
                </div>
                
                <div class="glass-dark p-8 rounded-2xl hover-lift border border-gray-700">
                    <div class="w-16 h-16 bg-yellow-500/20 rounded-full flex items-center justify-center mb-6">
                        <i class="fas fa-heart text-yellow-400 text-2xl"></i>
                    </div>
                    <h3 class="serif text-2xl mb-3">Romance & Love</h3>
                    <p class="text-gray-400 mb-6">Roses, champagne, personalized jewelry, and intimate gifts for that special someone.</p>
                    <p class="text-yellow-400 font-semibold text-xl mb-4">From $199</p>
                    <button onclick="addToCart({id: 'basket3', name: 'Romance & Love Basket', price: 199, image: 'https://images.unsplash.com/photo-1513201099705-a9746e1e201f?w=400&q=80'})" class="w-full py-3 border border-yellow-400 text-yellow-400 rounded-full hover:bg-yellow-400 hover:text-gray-900 transition-all">
                        Add to Cart
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- Product Detail Modal -->
    <div id="product-modal" class="fixed inset-0 z-50 hidden">
        <div class="absolute inset-0 bg-black/70 backdrop-blur-sm" onclick="closeModal()"></div>
        <div class="absolute inset-0 flex items-center justify-center p-4">
            <div class="bg-white rounded-2xl max-w-4xl w-full max-h-[90vh] overflow-y-auto shadow-2xl transform scale-95 opacity-0 transition-all duration-300" id="modal-content">
                <button onclick="closeModal()" class="absolute top-4 right-4 w-10 h-10 bg-gray-100 rounded-full flex items-center justify-center hover:bg-gray-200 transition-colors z-10">
                    <i class="fas fa-times text-gray-600"></i>
                </button>
                <div id="modal-body" class="grid md:grid-cols-2 gap-8 p-8">
                    <!-- Content injected by JS -->
                </div>
            </div>
        </div>
    </div>

    <!-- Cart Sidebar -->
    <div id="cart-overlay" class="fixed inset-0 bg-black/50 z-50 hidden" onclick="toggleCart()"></div>
    <div id="cart-sidebar" class="cart-sidebar fixed top-0 right-0 h-full w-full md:w-[450px] bg-white z-50 shadow-2xl flex flex-col">
        <div class="p-6 border-b border-gray-100 flex justify-between items-center">
            <h2 class="serif text-2xl">Your Cart</h2>
            <button onclick="toggleCart()" class="w-10 h-10 rounded-full hover:bg-gray-100 flex items-center justify-center transition-colors">
                <i class="fas fa-times text-gray-600"></i>
            </button>
        </div>
        <div id="cart-items" class="flex-1 overflow-y-auto p-6 space-y-4">
            <!-- Cart items injected here -->
        </div>
        <div class="border-t border-gray-100 p-6 bg-gray-50">
            <div class="flex justify-between mb-4 text-lg font-semibold">
                <span>Total</span>
                <span id="cart-total">$0.00</span>
            </div>
            <button class="w-full py-4 bg-gray-900 text-white rounded-full font-semibold hover:bg-gray-800 transition-all mb-3">
                Checkout
            </button>
            <button onclick="toggleCart()" class="w-full py-3 border border-gray-300 text-gray-700 rounded-full font-medium hover:bg-gray-100 transition-all">
                Continue Shopping
            </button>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="toast fixed bottom-8 left-1/2 transform -translate-x-1/2 bg-gray-900 text-white px-6 py-4 rounded-full shadow-2xl z-50 flex items-center gap-3">
        <i class="fas fa-check-circle text-green-400"></i>
        <span id="toast-message">Item added to cart!</span>
    </div>

    <!-- Footer -->
    <footer class="bg-gray-900 text-white pt-20 pb-10">
        <div class="max-w-7xl mx-auto px-4">
            <div class="grid md:grid-cols-4 gap-12 mb-16">
                <div>
                    <span class="serif text-2xl font-bold tracking-wider block mb-6">LUXE & CO</span>
                    <p class="text-gray-400 text-sm leading-relaxed mb-6">Crafting personalized luxury gifts that create lasting memories. Every piece tells a unique story.</p>
                    <div class="flex space-x-4">
                        <a href="#" class="w-10 h-10 bg-gray-800 rounded-full flex items-center justify-center hover:bg-yellow-500 hover:text-gray-900 transition-all">
                            <i class="fab fa-instagram"></i>
                        </a>
                        <a href="#" class="w-10 h-10 bg-gray-800 rounded-full flex items-center justify-center hover:bg-yellow-500 hover:text-gray-900 transition-all">
                            <i class="fab fa-facebook-f"></i>
                        </a>
                        <a href="#" class="w-10 h-10 bg-gray-800 rounded-full flex items-center justify-center hover:bg-yellow-500 hover:text-gray-900 transition-all">
                            <i class="fab fa-pinterest-p"></i>
                        </a>
                    </div>
                </div>
                <div>
                    <h4 class="font-semibold uppercase tracking-wider mb-6">Shop</h4>
                    <ul class="space-y-3 text-gray-400 text-sm">
                        <li><a href="#bags" class="hover:text-yellow-400 transition-colors">All Bags</a></li>
                        <li><a href="#bottles" class="hover:text-yellow-400 transition-colors">Water Bottles</a></li>
                        <li><a href="#bracelets" class="hover:text-yellow-400 transition-colors">Bracelets</a></li>
                        <li><a href="#baskets" class="hover:text-yellow-400 transition-colors">Gift Baskets</a></li>
                        <li><a href="#" class="hover:text-yellow-400 transition-colors">New Arrivals</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="font-semibold uppercase tracking-wider mb-6">Customer Care</h4>
                    <ul class="space-y-3 text-gray-400 text-sm">
                        <li><a href="#" class="hover:text-yellow-400 transition-colors">Contact Us</a></li>
                        <li><a href="#" class="hover:text-yellow-400 transition-colors">Shipping Info</a></li>
                        <li><a href="#" class="hover:text-yellow-400 transition-colors">Returns & Exchanges</a></li>
                        <li><a href="#" class="hover:text-yellow-400 transition-colors">FAQ</a></li>
                        <li><a href="#" class="hover:text-yellow-400 transition-colors">Track Order</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="font-semibold uppercase tracking-wider mb-6">Newsletter</h4>
                    <p class="text-gray-400 text-sm mb-4">Subscribe for exclusive offers and personalized gift ideas.</p>
                    <form class="flex gap-2" onsubmit="event.preventDefault(); showToast('Thank you for subscribing!');">
                        <input type="email" placeholder="Your email" class="flex-1 px-4 py-3 bg-gray-800 border border-gray-700 rounded-full text-white placeholder-gray-500 focus:outline-none focus:border-yellow-500 text-sm">
                        <button type="submit" class="px-6 py-3 bg-yellow-500 text-gray-900 rounded-full font-semibold hover:bg-yellow-400 transition-all">
                            <i class="fas fa-arrow-right"></i>
                        </button>
                    </form>
                </div>
            </div>
            <div class="border-t border-gray-800 pt-8 flex flex-col md:flex-row justify-between items-center gap-4">
                <p class="text-gray-500 text-sm">&copy; 2024 Luxe & Co. All rights reserved.</p>
                <div class="flex gap-6 text-sm text-gray-500">
                    <a href="#" class="hover:text-white transition-colors">Privacy Policy</a>
                    <a href="#" class="hover:text-white transition-colors">Terms of Service</a>
                </div>
            </div>
        </div>
    </footer>

    <script>
        // Product Data
        const products = [
            // Bags
            {
                id: 'bag1',
                name: 'The Executive Tote',
                category: 'bags',
                price: 189,
                image: 'https://images.unsplash.com/photo-1548036328-c9fa89d128fa?w=600&q=80',
                description: 'Handcrafted leather tote with gold hardware. Perfect for the modern professional.',
                customization: ['Initials (up to 3 letters)', 'Name (up to 12 characters)', 'No personalization'],
                colors: ['Black', 'Tan', 'Navy', 'Burgundy']
            },
            {
                id: 'bag2',
                name: 'Weekender Duffle',
                category: 'bags',
                price: 249,
                image: 'https://images.unsplash.com/photo-1553062407-98eeb64c6a62?w=600&q=80',
                description: 'Spacious canvas and leather duffle bag for weekend getaways.',
                customization: ['Name engraving on tag', 'Custom patch', 'No personalization'],
                colors: ['Olive', 'Charcoal', 'Camel']
            },
            {
                id: 'bag3',
                name: 'Mini Crossbody',
                category: 'bags',
                price: 129,
                image: 'https://images.unsplash.com/photo-1584917865442-de89df76afd3?w=600&q=80',
                description: 'Compact and stylish crossbody bag for everyday essentials.',
                customization: ['Monogram (2-3 letters)', 'Name on strap', 'No personalization'],
                colors: ['Blush', 'Black', 'Sage', 'Cream']
            },
            
            // Bottles & Hats
            {
                id: 'bottle1',
                name: 'Hydration Pro Set',
                category: 'bottles',
                price: 79,
                image: 'https://images.unsplash.com/photo-1602143407151-7111542de6e8?w=600&q=80',
                description: 'Insulated stainless steel bottle with matching snapback hat.',
                customization: ['Name on bottle', 'Initials on hat', 'Both personalized', 'No personalization'],
                colors: ['Matte Black', 'Rose Gold', 'Navy', 'Forest Green']
            },
            {
                id: 'bottle2',
                name: 'Active Lifestyle Bundle',
                category: 'bottles',
                price: 99,
                image: 'https://images.unsplash.com/photo-1523362628745-0c100150b504?w=600&q=80',
                description: 'Sports bottle with performance cap and breathable trucker hat.',
                customization: ['Name on bottle', 'Team name on hat', 'Both personalized'],
                colors: ['Electric Blue', 'Neon Pink', 'White', 'Black']
            },
            {
                id: 'bottle3',
                name: 'Corporate Gift Set',
                category: 'bottles',
                price: 119,
                image: 'https://images.unsplash.com/photo-1610824352934-c10d87b700cc?w=600&q=80',
                description: 'Premium bottle with executive cap and structured cap.',
                customization: ['Company logo', 'Employee name', 'Both'],
                colors: ['Midnight Black', 'Silver', 'Navy Blue']
            },
            
            // Gift Baskets (Additional to featured ones)
            {
                id: 'basket4',
                name: 'New Parent Care Package',
                category: 'baskets',
                price: 169,
                image: 'https://images.unsplash.com/photo-1515488042361-ee00e0ddd4e4?w=600&q=80',
                description: 'Thoughtful essentials for new parents including baby items and self-care products.',
                customization: ['Personalized card', 'Custom ribbon message', 'Both'],
                colors: ['Neutral', 'Pink Theme', 'Blue Theme']
            },
            {
                id: 'basket5',
                name: 'Corporate Wellness Kit',
                category: 'baskets',
                price: 129,
                image: 'https://images.unsplash.com/photo-1513201099705-a9746e1e201f?w=600&q=80',
                description: 'Desk essentials, healthy snacks, and relaxation items for the office.',
                customization: ['Company branding', 'Employee name', 'No personalization'],
                colors: ['Standard']
            },
            
            // Bracelets
            {
                id: 'bracelet1',
                name: 'Classic ID Bracelet - Men',
                category: 'bracelets',
                price: 89,
                image: 'https://images.unsplash.com/photo-1611591437281-460bfbe1220a?w=600&q=80',
                description: 'Stainless steel ID bracelet with custom engraving. Bold and masculine.',
                customization: ['Name engraving', 'Coordinates', 'Special date', 'Custom message'],
                colors: ['Silver', 'Gunmetal', 'Gold', 'Black']
            },
            {
                id: 'bracelet2',
                name: 'Delicate Chain Bracelet - Women',
                category: 'bracelets',
                price: 69,
                image: 'https://images.unsplash.com/photo-1573408301185-9146fe634ad0?w=600&q=80',
                description: 'Elegant chain bracelet with personalized nameplate.',
                customization: ['Name (up to 8 letters)', 'Initial', 'Short phrase', 'No engraving'],
                colors: ['Rose Gold', 'Silver', 'Gold']
            },
            {
                id: 'bracelet3',
                name: 'Leather Cuff - Unisex',
                category: 'bracelets',
                price: 59,
                image: 'https://images.unsplash.com/photo-1611652022419-a9419f74343d?w=600&q=80',
                description: 'Genuine leather cuff with metal plate for engraving.',
                customization: ['Name', 'Coordinates', 'Date', 'Short quote'],
                colors: ['Brown', 'Black', 'Tan', 'Navy']
            },
            {
                id: 'bracelet4',
                name: 'Beaded Gemstone Bracelet',
                category: 'bracelets',
                price: 79,
                image: 'https://images.unsplash.com/photo-1599643478518-17488fbbcd75?w=600&q=80',
                description: 'Natural gemstone beads with custom engraved charm.',
                customization: ['Initial charm', 'Name charm', 'Symbol charm'],
                colors: ['Onyx Black', 'Lapis Blue', 'Rose Quartz', 'Tiger Eye']
            }
        ];

        // Cart State
        let cart = [];

        // Initialize
        document.addEventListener('DOMContentLoaded', () => {
            renderProducts('all');
            updateNavbar();
        });

        // Navbar scroll effect
        window.addEventListener('scroll', updateNavbar);

        function updateNavbar() {
            const navbar = document.getElementById('navbar');
            const logo = document.getElementById('nav-logo');
            const links = navbar.querySelectorAll('a:not(.mobile-menu a)');
            const icons = navbar.querySelectorAll('button:not(.md\\:hidden) i');
            
            if (window.scrollY > 50) {
                navbar.classList.add('glass', 'shadow-sm');
                navbar.classList.remove('bg-transparent');
                logo.classList.remove('text-white');
                logo.classList.add('text-gray-900');
                links.forEach(link => {
                    link.classList.remove('text-white');
                    link.classList.add('text-gray-800');
                });
                icons.forEach(icon => {
                    icon.classList.remove('text-white');
                    icon.classList.add('text-gray-800');
                });
            } else {
                navbar.classList.remove('glass', 'shadow-sm');
                navbar.classList.add('bg-transparent');
                logo.classList.add('text-white');
                logo.classList.remove('text-gray-900');
                links.forEach(link => {
                    link.classList.add('text-white');
                    link.classList.remove('text-gray-800');
                });
                icons.forEach(icon => {
                    icon.classList.add('text-white');
                    icon.classList.remove('text-gray-800');
                });
            }
        }

        // Mobile Menu Toggle
        function toggleMobileMenu() {
            const menu = document.getElementById('mobile-menu');
            menu.classList.toggle('open');
        }

        // Filter Products
        function filterProducts(category) {
            // Update buttons
            document.querySelectorAll('.category-btn').forEach(btn => {
                if (btn.dataset.category === category) {
                    btn.classList.add('bg-gray-900', 'text-white', 'border-gray-900');
                    btn.classList.remove('border-gray-300', 'text-gray-700');
                } else {
                    btn.classList.remove('bg-gray-900', 'text-white', 'border-gray-900');
                    btn.classList.add('border-gray-300', 'text-gray-700');
                }
            });
            
            renderProducts(category);
        }

        // Render Products
        function renderProducts(category) {
            const grid = document.getElementById('products-grid');
            const filtered = category === 'all' ? products : products.filter(p => p.category === category);
            
            grid.innerHTML = filtered.map(product => `
                <div class="group bg-white rounded-2xl overflow-hidden hover-lift shadow-sm border border-gray-100">
                    <div class="img-zoom relative aspect-[4/5] overflow-hidden bg-gray-100">
                        <img src="${product.image}" alt="${product.name}" class="w-full h-full object-cover">
                        <div class="absolute inset-0 bg-black/0 group-hover:bg-black/20 transition-all duration-300"></div>
                        <button onclick="openProductModal('${product.id}')" class="absolute bottom-4 left-4 right-4 py-3 bg-white text-gray-900 rounded-full font-medium opacity-0 group-hover:opacity-100 transform translate-y-4 group-hover:translate-y-0 transition-all duration-300 shadow-lg hover:bg-gray-50">
                            Customize & Add
                        </button>
                        ${product.category === 'bracelets' ? '<span class="absolute top-4 left-4 bg-yellow-400 text-gray-900 text-xs font-bold px-3 py-1 rounded-full">PERSONALIZED</span>' : ''}
                    </div>
                    <div class="p-6">
                        <div class="flex justify-between items-start mb-2">
                            <h3 class="serif text-lg font-medium text-gray-900">${product.name}</h3>
                            <span class="font-semibold text-gray-900">$${product.price}</span>
                        </div>
                        <p class="text-gray-500 text-sm mb-4 line-clamp-2">${product.description}</p>
                        <div class="flex items-center justify-between">
                            <div class="flex gap-1">
                                ${product.colors.slice(0, 4).map(color => `
                                    <div class="w-4 h-4 rounded-full border border-gray-200" style="background-color: ${getColorCode(color)}" title="${color}"></div>
                                `).join('')}
                                ${product.colors.length > 4 ? `<span class="text-xs text-gray-400 ml-1">+${product.colors.length - 4}</span>` : ''}
                            </div>
                            <button onclick="quickAdd('${product.id}')" class="text-yellow-600 hover:text-yellow-700 font-medium text-sm flex items-center gap-1">
                                Quick Add <i class="fas fa-plus text-xs"></i>
                            </button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        // Get color code helper
        function getColorCode(colorName) {
            const colors = {
                'Black': '#000000', 'Tan': '#D2B48C', 'Navy': '#000080', 'Burgundy': '#800020',
                'Olive': '#808000', 'Charcoal': '#36454F', 'Camel': '#C19A6B',
                'Blush': '#DE5D83', 'Sage': '#9DC183', 'Cream': '#FFFDD0',
                'Matte Black': '#1a1a1a', 'Rose Gold': '#B76E79', 'Forest Green': '#228B22',
                'Electric Blue': '#7DF9FF', 'Neon Pink': '#FF6EC7', 'White': '#FFFFFF',
                'Silver': '#C0C0C0', 'Gunmetal': '#2A3439', 'Gold': '#FFD700',
                'Brown': '#8B4513', 'Navy Blue': '#000080', 'Onyx Black': '#353839',
                'Lapis Blue': '#26619C', 'Rose Quartz': '#AA98A9', 'Tiger Eye': '#B56917'
            };
            return colors[colorName] || '#cccccc';
        }

        // Product Modal
        function openProductModal(productId) {
            const product = products.find(p => p.id === productId);
            if (!product) return;
            
            const modal = document.getElementById('product-modal');
            const content = document.getElementById('modal-content');
            const body = document.getElementById('modal-body');
            
            body.innerHTML = `
                <div class="img-zoom rounded-xl overflow-hidden">
                    <img src="${product.image}" alt="${product.name}" class="w-full h-full object-cover min-h-[300px]">
                </div>
                <div class="flex flex-col">
                    <span class="text-yellow-600 text-sm tracking-wider uppercase mb-2">${product.category}</span>
                    <h2 class="serif text-3xl text-gray-900 mb-4">${product.name}</h2>
                    <p class="text-2xl font-semibold text-gray-900 mb-6">$${product.price}</p>
                    <p class="text-gray-600 mb-8">${product.description}</p>
                    
                    <div class="space-y-6 mb-8">
                        <div>
                            <label class="block text-sm font-semibold text-gray-900 mb-3">Personalization Option</label>
                            <div class="space-y-2">
                                ${product.customization.map((opt, idx) => `
                                    <label class="flex items-center gap-3 cursor-pointer p-3 rounded-lg border border-gray-200 hover:border-yellow-400 transition-all">
                                        <input type="radio" name="customization" value="${opt}" class="custom-radio w-4 h-4 text-yellow-500 focus:ring-yellow-500" ${idx === 0 ? 'checked' : ''}>
                                        <span class="text-sm text-gray-700">${opt}</span>
                                    </label>
                                `).join('')}
                            </div>
                        </div>
                        
                        <div>
                            <label class="block text-sm font-semibold text-gray-900 mb-3">Select Color</label>
                            <div class="flex flex-wrap gap-3">
                                ${product.colors.map((color, idx) => `
                                    <button onclick="selectColor(this, '${color}')" class="color-btn w-10 h-10 rounded-full border-2 ${idx === 0 ? 'border-yellow-500 ring-2 ring-yellow-200' : 'border-gray-200'} transition-all hover:scale-110" style="background-color: ${getColorCode(color)}" title="${color}"></button>
                                `).join('')}
                            </div>
                            <p id="selected-color" class="text-sm text-gray-600 mt-2">Selected: ${product.colors[0]}</p>
                        </div>
                        
                        <div id="engraving-field" class="${product.customization[0].includes('No') ? 'hidden' : ''}">
                            <label class="block text-sm font-semibold text-gray-900 mb-2">Engraving Text</label>
                            <input type="text" id="engraving-text" placeholder="Enter name or message..." 
                                class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:border-yellow-500 focus:ring-2 focus:ring-yellow-200 transition-all"
                                maxlength="20">
                            <p class="text-xs text-gray-500 mt-1">Max 20 characters</p>
                        </div>
                    </div>
                    
                    <button onclick="addToCartFromModal('${product.id}')" class="mt-auto w-full py-4 bg-gray-900 text-white rounded-full font-semibold hover:bg-gray-800 transition-all transform hover:scale-[1.02] flex items-center justify-center gap-2">
                        <i class="fas fa-shopping-bag"></i> Add to Cart - $${product.price}
                    </button>
                </div>
            `;
            
            modal.classList.remove('hidden');
            setTimeout(() => {
                content.classList.remove('scale-95', 'opacity-0');
                content.classList.add('scale-100', 'opacity-100');
            }, 10);
        }

        function closeModal() {
            const modal = document.getElementById('product-modal');
            const content = document.getElementById('modal-content');
            
            content.classList.remove('scale-100', 'opacity-100');
            content.classList.add('scale-95', 'opacity-0');
            
            setTimeout(() => {
                modal.classList.add('hidden');
            }, 300);
        }

        function selectColor(btn, color) {
            document.querySelectorAll('.color-btn').forEach(b => {
                b.classList.remove('border-yellow-500', 'ring-2', 'ring-yellow-200');
                b.classList.add('border-gray-200');
            });
            btn.classList.remove('border-gray-200');
            btn.classList.add('border-yellow-500', 'ring-2', 'ring-yellow-200');
            document.getElementById('selected-color').textContent = `Selected: ${color}`;
        }

        // Cart Functions
        function addToCart(product) {
            const existing = cart.find(item => item.id === product.id);
            if (existing) {
                existing.quantity++;
            } else {
                cart.push({...product, quantity: 1});
            }
            updateCartUI();
            showToast(`${product.name} added to cart!`);
        }

        function addToCartFromModal(productId) {
            const product = products.find(p => p.id === productId);
            const engraving = document.getElementById('engraving-text')?.value || '';
            const color = document.getElementById('selected-color')?.textContent.replace('Selected: ', '') || product.colors[0];
            const customization = document.querySelector('input[name="customization"]:checked')?.value || product.customization[0];
            
            const cartItem = {
                ...product,
                quantity: 1,
                engraving,
                color,
                customization
            };
            
            cart.push(cartItem);
            updateCartUI();
            closeModal();
            showToast(`${product.name} customized and added!`);
        }

        function quickAdd(productId) {
            const product = products.find(p => p.id === productId);
            addToCart(product);
        }

        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCartUI();
        }

        function updateQuantity(index, change) {
            cart[index].quantity += change;
            if (cart[index].quantity <= 0) {
                cart.splice(index, 1);
            }
            updateCartUI();
        }

        function updateCartUI() {
            const count = document.getElementById('cart-count');
            const items = document.getElementById('cart-items');
            const total = document.getElementById('cart-total');
            
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            const totalPrice = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            
            count.textContent = totalItems;
            total.textContent = `$${totalPrice.toFixed(2)}`;
            
            if (cart.length === 0) {
                items.innerHTML = `
                    <div class="text-center py-12">
                        <i class="fas fa-shopping-bag text-4xl text-gray-300 mb-4"></i>
                        <p class="text-gray-500">Your cart is empty</p>
                        <button onclick="toggleCart()" class="mt-4 text-yellow-600 hover:text-yellow-700 font-medium">Continue Shopping</button>
                    </div>
                `;
            } else {
                items.innerHTML = cart.map((item, index) => `
                    <div class="flex gap-4 bg-gray-50 p-4 rounded-xl">
                        <img src="${item.image}" alt="${item.name}" class="w-20 h-20 object-cover rounded-lg">
                        <div class="flex-1">
                            <h4 class="font-semibold text-gray-900 text-sm">${item.name}</h4>
                            ${item.engraving ? `<p class="text-xs text-gray-500 mt-1">"${item.engraving}"</p>` : ''}
                            ${item.color ? `<p class="text-xs text-gray-500">Color: ${item.color}</p>` : ''}
                            <div class="flex items-center justify-between mt-3">
                                <div class="flex items-center gap-3 bg-white rounded-full px-3 py-1 border border-gray-200">
                                    <button onclick="updateQuantity(${index}, -1)" class="text-gray-500 hover:text-gray-700 w-6 h-6 flex items-center justify-center">-</button>
                                    <span class="text-sm font-medium w-4 text-center">${item.quantity}</span>
                                    <button onclick="updateQuantity(${index}, 1)" class="text-gray-500 hover:text-gray-700 w-6 h-6 flex items-center justify-center">+</button>
                                </div>
                                <span class="font-semibold text-gray-900">$${(item.price * item.quantity).toFixed(2)}</span>
                            </div>
                        </div>
                        <button onclick="removeFromCart(${index})" class="text-gray-400 hover:text-red-500 transition-colors h-fit">
                            <i class="fas fa-trash-alt"></i>
                        </button>
                    </div>
                `).join('');
            }
        }

        function toggleCart() {
            const sidebar = document.getElementById('cart-sidebar');
            const overlay = document.getElementById('cart-overlay');
            
            if (sidebar.classList.contains('open')) {
                sidebar.classList.remove('open');
                overlay.classList.add('hidden');
                document.body.style.overflow = '';
            } else {
                sidebar.classList.add('open');
                overlay.classList.remove('hidden');
                document.body.style.overflow = 'hidden';
            }
        }

        // Toast Notification
        function showToast(message) {
            const toast = document.getElementById('toast');
            const msg = document.getElementById('toast-message');
            msg.textContent = message;
            toast.classList.add('show');
            
            setTimeout(() => {
                toast.classList.remove('show');
            }, 3000);
        }

        // Smooth scroll helper
        function scrollToSection(id) {
            document.getElementById(id).scrollIntoView({ behavior: 'smooth' });
        }

        // Close modal on escape key
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape') {
                closeModal();
                const sidebar = document.getElementById('cart-sidebar');
                if (sidebar.classList.contains('open')) toggleCart();
            }
        });
    </script>
</body>
</html>
