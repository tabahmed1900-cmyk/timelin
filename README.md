<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Time Line Store - متجر الساعات الفاخرة</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        gold: { DEFAULT: '#d4af37', light: '#f3e5ab', dark: '#aa8c2c' },
                        darkBg: '#0a0a0a',
                        cardBg: '#141414',
                        borderCol: '#262626'
                    },
                    fontFamily: { cairo: ['Cairo', 'sans-serif'] }
                }
            }
        }
    </script>
    <style>
        body { font-family: 'Cairo', sans-serif; background-color: #0a0a0a; color: #f5f5f5; }
        .gold-gradient-text {
            background: linear-gradient(135deg, #f3e5ab 0%, #d4af37 50%, #aa8c2c 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .gold-gradient-bg { background: linear-gradient(135deg, #d4af37 0%, #aa8c2c 100%); }
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #0a0a0a; }
        ::-webkit-scrollbar-thumb { background: #262626; border-radius: 4px; }
    </style>
</head>
<body class="bg-darkBg min-h-screen flex flex-col selection:bg-gold selection:text-black">

    <header class="sticky top-0 z-50 bg-darkBg/90 backdrop-blur-md border-b border-borderCol">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <div class="flex items-center space-x-3 space-x-reverse">
                <div class="w-10 h-10 rounded-full gold-gradient-bg flex items-center justify-center shadow-lg shadow-gold/20">
                    <i class="fa-solid fa-clock text-black text-lg"></i>
                </div>
                <div>
                    <span class="text-xl font-black tracking-wider gold-gradient-text">TIME LINE</span>
                    <span class="block text-[10px] tracking-widest text-neutral-400">LUXURY WATCHES</span>
                </div>
            </div>
            <button onclick="toggleCart()" class="relative p-3 rounded-xl bg-cardBg border border-borderCol hover:border-gold/50 transition-all text-gold flex items-center gap-2">
                <i class="fa-solid fa-bag-shopping text-xl"></i>
                <span class="hidden sm:inline text-sm font-semibold">السلة</span>
                <span id="cart-badge" class="absolute -top-2 -right-2 bg-gold text-black font-bold text-xs w-5 h-5 rounded-full flex items-center justify-center shadow-md">0</span>
            </button>
        </div>
    </header>

    <section class="relative py-16 sm:py-24 overflow-hidden border-b border-borderCol bg-gradient-to-b from-cardBg to-darkBg">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10 text-center">
            <span class="inline-block py-1 px-4 rounded-full bg-gold/10 border border-gold/30 text-gold text-xs sm:text-sm font-semibold tracking-wider mb-6">
                ✨ تشكيلة فاخرة لعام 2026
            </span>
            <h1 class="text-3xl sm:text-5xl lg:text-6xl font-black tracking-tight mb-6">
                أرقى الساعات التي تعكس <span class="gold-gradient-text">فخامة حضورك</span>
            </h1>
            <p class="max-w-2xl mx-auto text-neutral-400 text-sm sm:text-base mb-8">
                اكتشف تشكيلة حصرية من الساعات الكلاسيكية والرياضية والذكية المصممة خصيصاً لأصحاب الذوق الرفيع في مصر.
            </p>
            <a href="#shop" class="inline-block px-8 py-3.5 rounded-xl gold-gradient-bg text-black font-bold hover:opacity-95 transition-all shadow-lg shadow-gold/20">
                تصفح الساعات الآن
            </a>
        </div>
    </section>

    <main id="shop" class="flex-grow max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12 w-full">
        <div class="flex flex-wrap items-center justify-center gap-3 mb-12">
            <button onclick="filterProducts('all')" class="filter-btn px-6 py-2.5 rounded-xl text-sm font-bold bg-gold text-black transition-all shadow-md">الكل</button>
            <button onclick="filterProducts('classic')" class="filter-btn px-6 py-2.5 rounded-xl text-sm font-bold bg-cardBg text-neutral-300 border border-borderCol hover:border-gold/50 transition-all">كلاسيك فاخر</button>
            <button onclick="filterProducts('sport')" class="filter-btn px-6 py-2.5 rounded-xl text-sm font-bold bg-cardBg text-neutral-300 border border-borderCol hover:border-gold/50 transition-all">رياضية</button>
            <button onclick="filterProducts('smart')" class="filter-btn px-6 py-2.5 rounded-xl text-sm font-bold bg-cardBg text-neutral-300 border border-borderCol hover:border-gold/50 transition-all">ساعات ذكية</button>
        </div>
        <div id="products-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8"></div>
    </main>

    <div id="cart-drawer" class="fixed inset-y-0 left-0 w-full sm:w-96 bg-cardBg border-r border-borderCol z-50 transform -translate-x-full transition-transform duration-300 flex flex-col shadow-2xl">
        <div class="p-6 border-b border-borderCol flex items-center justify-between">
            <div class="flex items-center gap-3"><i class="fa-solid fa-bag-shopping text-gold text-xl"></i><h2 class="text-lg font-bold">سلة المشتريات</h2></div>
            <button onclick="toggleCart()" class="p-2 text-neutral-400 hover:text-white"><i class="fa-solid fa-xmark text-xl"></i></button>
        </div>
        <div id="cart-items" class="flex-grow overflow-y-auto p-6 space-y-4 divide-y divide-borderCol/50">
            <div class="text-center py-12 text-neutral-500"><i class="fa-solid fa-cart-shopping text-4xl mb-3 opacity-40"></i><p>سلة المشتريات فارغة حالياً</p></div>
        </div>
        <div class="p-6 border-t border-borderCol bg-darkBg">
            <div class="flex justify-between items-center mb-4"><span class="text-neutral-400">الإجمالي:</span><span id="cart-total" class="text-xl font-black text-gold">0 ج.م</span></div>
            <button onclick="openCheckoutModal()" id="checkout-btn" disabled class="w-full py-3.5 rounded-xl gold-gradient-bg text-black font-bold disabled:opacity-55 shadow-lg">إتمام الطلب عبر واتساب</button>
        </div>
    </div>

    <div id="checkout-modal" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-sm hidden items-center justify-center p-4">
        <div class="bg-cardBg border border-borderCol rounded-2xl w-full max-w-md p-6 relative shadow-2xl">
            <button onclick="closeCheckoutModal()" class="absolute top-4 left-4 text-neutral-400 hover:text-white"><i class="fa-solid fa-xmark text-xl"></i></button>
            <h3 class="text-xl font-bold mb-4 gold-gradient-text">إتمام بيانات الطلب</h3>
            <form id="order-form" onsubmit="submitOrder(event)" class="space-y-4">
                <div><label class="block text-sm text-neutral-400 mb-1">الاسم بالكامل</label><input type="text" id="customer-name" required class="w-full bg-darkBg border border-borderCol rounded-xl px-4 py-3 text-white focus:border-gold focus:outline-none" placeholder="ادخل اسمك"></div>
                <div><label class="block text-sm text-neutral-400 mb-1">رقم الهاتف (مصر)</label><input type="tel" id="customer-phone" required class="w-full bg-darkBg border border-borderCol rounded-xl px-4 py-3 text-white focus:border-gold focus:outline-none" placeholder="01xxxxxxxxx"></div>
                <div><label class="block text-sm text-neutral-400 mb-1">العنوان بالتفصيل</label><textarea id="customer-address" required rows="2" class="w-full bg-darkBg border border-borderCol rounded-xl px-4 py-3 text-white focus:border-gold focus:outline-none resize-none" placeholder="المدينة، الشارع..."></textarea></div>
                <button type="submit" class="w-full py-3.5 rounded-xl gold-gradient-bg text-black font-bold shadow-lg">إرسال الطلب عبر واتساب 🚀</button>
            </form>
        </div>
    </div>

    <footer class="border-t border-borderCol py-8 bg-cardBg/50 text-center text-sm text-neutral-500">
        <p>© 2026 Time Line Store. جميع الحقوق محفوظة.</p>
    </footer>

    <script>
        const WHATSAPP_NUMBER = "201000000000";
        const products = [
            { id: 1, name: "ساعة رويال كلاسيك الفاخرة", category: "classic", price: 1850, image: "https://images.unsplash.com/photo-1522335789203-aabd1fc54bc9?auto=format&fit=crop&w=600&q=80", desc: "تصميم أنيق من الستانلس ستيل المقاوم للصدأ." },
            { id: 2, name: "ساعة كرونوغراف الرياضية", category: "sport", price: 2300, image: "https://images.unsplash.com/photo-1524805444758-089113d48a6d?auto=format&fit=crop&w=600&q=80", desc: "مصممة خصيصاً لعشاق الحركة والسرعة." },
            { id: 3, name: "ساعة التيتانيوم الذكية برو", category: "smart", price: 3100, image: "https://images.unsplash.com/photo-1508685096489-7aacd43bd3b1?auto=format&fit=crop&w=600&q=80", desc: "شاشة AMOLED عالية الدقة مع تتبع اللياقة." },
            { id: 4, name: "ساعة جولد إكس الكلاسيكية", category: "classic", price: 2100, image: "https://images.unsplash.com/photo-1533139502658-0198f920d8e8?auto=format&fit=crop&w=600&q=80", desc: "مظهر كلاسيكي فريد يعكس الفخامة." },
            { id: 5, name: "ساعة ناين تكتيكال الرياضية", category: "sport", price: 1650, image: "https://images.unsplash.com/photo-1539874754764-5a96559165b0?auto=format&fit=crop&w=600&q=80", desc: "هيكل قوي ومتين يتحمل أصعب الظروف." },
            { id: 6, name: "ساعة أورا الذكية المتطورة", category: "smart", price: 2750, image: "https://images.unsplash.com/photo-1517502884422-41eaead166d4?auto=format&fit=crop&w=600&q=80", desc: "بطارية تدوم طويلاً مع مكالمات مباشرة." }
        ];
        let cart = [];

        function renderProducts(filter = 'all') {
            const grid = document.getElementById('products-grid');
            const filtered = filter === 'all' ? products : products.filter(p => p.category === filter);
            grid.innerHTML = filtered.map(p => `
                <div class="bg-cardBg border border-borderCol rounded-2xl overflow-hidden hover:border-gold/50 transition-all duration-300 flex flex-col group shadow-xl">
                    <div class="relative h-64 overflow-hidden bg-neutral-900">
                        <img src="${p.image}" alt="${p.name}" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500">
                    </div>
                    <div class="p-6 flex flex-col flex-grow">
                        <h3 class="text-lg font-bold mb-2 group-hover:text-gold transition-colors">${p.name}</h3>
                        <p class="text-neutral-400 text-sm mb-4 flex-grow">${p.desc}</p>
                        <div class="flex items-center justify-between mt-auto pt-4 border-t border-borderCol">
                            <span class="text-xl font-black text-gold">${p.price} ج.م</span>
                            <button onclick="addToCart(${p.id})" class="px-4 py-2.5 rounded-xl bg-gold text-black font-bold text-sm hover:opacity-90 shadow-md flex items-center gap-2">
                                <i class="fa-solid fa-cart-plus"></i> إضافة للسلة
                            </button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        function filterProducts(category) {
            renderProducts(category);
        }

        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const existing = cart.find(item => item.id === productId);
            if (existing) { existing.quantity += 1; } else { cart.push({ ...product, quantity: 1 }); }
            updateCartUI();
            toggleCart(true);
        }

        function updateQuantity(productId, delta) {
            const item = cart.find(i => i.id === productId);
            if (item) {
                item.quantity += delta;
                if (item.quantity <= 0) { cart = cart.filter(i => i.id !== productId); }
            }
            updateCartUI();
        }

        function updateCartUI() {
            const badge = document.getElementById('cart-badge');
            const totalEl = document.getElementById('cart-total');
            const itemsContainer = document.getElementById('cart-items');
            const checkoutBtn = document.getElementById('checkout-btn');
            const totalCount = cart.reduce((sum, i) => sum + i.quantity, 0);
            const totalPrice = cart.reduce((sum, i) => sum + (i.price * i.quantity), 0);
            badge.textContent = totalCount;
            totalEl.textContent = `${totalPrice} ج.م`;
            if (cart.length === 0) {
                itemsContainer.innerHTML = `<div class="text-center py-12 text-neutral-500"><i class="fa-solid fa-cart-shopping text-4xl mb-3 opacity-40"></i><p>سلة المشتريات فارغة حالياً</p></div>`;
                checkoutBtn.disabled = true;
            } else {
                checkoutBtn.disabled = false;
                itemsContainer.innerHTML = cart.map(item => `
                    <div class="flex items-center justify-between py-4">
                        <div class="flex items-center gap-3">
                            <img src="${item.image}" class="w-14 h-14 object-cover rounded-xl border border-borderCol">
                            <div><h4 class="text-sm font-bold">${item.name}</h4><span class="text-xs text-gold font-semibold">${item.price} ج.م</span></div>
                        </div>
                        <div class="flex items-center gap-2 bg-darkBg border border-borderCol rounded-xl p-1">
                            <button onclick="updateQuantity(${item.id}, -1)" class="w-7 h-7 rounded-lg bg-cardBg text-white flex items-center justify-center">-</button>
                            <span class="text-sm font-bold w-6 text-center">${item.quantity}</span>
                            <button onclick="updateQuantity(${item.id}, 1)" class="w-7 h-7 rounded-lg bg-cardBg text-white flex items-center justify-center">+</button>
                        </div>
                    </div>
                `).join('');
            }
        }

        function toggleCart(forceOpen = false) {
            const drawer = document.getElementById('cart-drawer');
            if (forceOpen) { drawer.classList.remove('-translate-x-full'); } else { drawer.classList.toggle('-translate-x-full'); }
        }

        function openCheckoutModal() {
            toggleCart();
            document.getElementById('checkout-modal').classList.remove('hidden');
            document.getElementById('checkout-modal').classList.add('flex');
        }

        function closeCheckoutModal() {
            document.getElementById('checkout-modal').classList.add('hidden');
            document.getElementById('checkout-modal').classList.remove('flex');
        }

        function submitOrder(e) {
            e.preventDefault();
            const name = document.getElementById('customer-name').value;
            const phone = document.getElementById('customer-phone').value;
            const address = document.getElementById('customer-address').value;
            let message = `🛍️ *طلب جديد من متجر Time Line*%0A👤 *الاسم:* ${name}%0A📞 *الهاتف:* ${phone}%0A📍 *العنوان:* ${address}%0A%0A📦 *المنتجات:*%0A`;
            cart.forEach((item, index) => { message += `${index + 1}. ${item.name} (×${item.quantity}) - ${item.price * item.quantity} ج.م%0A`; });
            const totalPrice = cart.reduce((sum, i) => sum + (i.price * i.quantity), 0);
            message += `%0A💰 *الإجمالي:* ${totalPrice} ج.م`;
            window.open(`https://wa.me/${WHATSAPP_NUMBER}?text=${message}`, '_blank');
        }

        renderProducts();
    </script>
</body>
</html>
