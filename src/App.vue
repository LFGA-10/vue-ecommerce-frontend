<script setup lang="ts">
import { ref } from 'vue';
import { 
  ShoppingBag, 
  Search, 
  User, 
  Menu, 
  Star, 
  ArrowRight,
  Heart,
  Filter
} from 'lucide-vue-next';

const categories = ['All', 'Electronics', 'Apparel', 'Home', 'Accessories'];
const activeCategory = ref('All');

const products = [
  { id: 1, name: "Premium Wireless Headphones", price: 299, rating: 4.8, image: "https://images.unsplash.com/photo-1505740420928-5e560c06d30e?auto=format&fit=crop&q=80&w=400", category: "Electronics" },
  { id: 2, name: "Minimalist Watch", price: 150, rating: 4.9, image: "https://images.unsplash.com/photo-1523275335684-37898b6baf30?auto=format&fit=crop&q=80&w=400", category: "Accessories" },
  { id: 3, name: "Smart Speaker", price: 120, rating: 4.7, image: "https://images.unsplash.com/photo-1589492477829-5e65395b66cc?auto=format&fit=crop&q=80&w=400", category: "Electronics" },
  { id: 4, name: "Leather Backpack", price: 180, rating: 4.6, image: "https://images.unsplash.com/photo-1548036627-19f2b16bc014?auto=format&fit=crop&q=80&w=400", category: "Accessories" },
];

const cartCount = ref(2);
</script>

<template>
  <div class="min-h-screen bg-white text-gray-900 font-['Inter'] selection:bg-indigo-100">
    <!-- Navbar -->
    <nav class="sticky top-0 z-50 bg-white/80 backdrop-blur-xl border-b border-gray-100">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between items-center h-20">
          <div class="flex items-center gap-10">
            <h1 class="text-2xl font-bold tracking-tighter text-indigo-600">LUMINA.</h1>
            <div class="hidden md:flex items-center gap-8 text-sm font-medium text-gray-500">
              <a href="#" class="hover:text-indigo-600 transition-colors">Shop</a>
              <a href="#" class="hover:text-indigo-600 transition-colors">Collections</a>
              <a href="#" class="hover:text-indigo-600 transition-colors">About</a>
            </div>
          </div>
          <div class="flex items-center gap-6">
            <button class="p-2 hover:bg-gray-50 rounded-full transition-colors"><Search size={20} /></button>
            <button class="p-2 hover:bg-gray-50 rounded-full transition-colors"><User size={20} /></button>
            <button class="relative p-2 hover:bg-gray-50 rounded-full transition-colors">
              <ShoppingBag size={20} />
              <span class="absolute top-0 right-0 bg-indigo-600 text-white text-[10px] font-bold w-5 h-5 rounded-full flex items-center justify-center">
                {{ cartCount }}
              </span>
            </button>
          </div>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section class="relative h-[80vh] flex items-center overflow-hidden bg-gray-50">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid md:grid-cols-2 items-center gap-12 relative z-10">
        <div class="space-y-8">
          <span class="inline-block px-4 py-2 bg-indigo-50 text-indigo-600 rounded-full text-xs font-bold uppercase tracking-widest">
            New Collection 2026
          </span>
          <h2 class="text-6xl md:text-8xl font-bold tracking-tighter leading-[0.9]">
            The Art of <br/> <span class="text-indigo-600">Simplicity.</span>
          </h2>
          <p class="text-xl text-gray-500 max-w-md leading-relaxed">
            Elevate your everyday with our curated selection of minimalist essentials, designed for performance and style.
          </p>
          <div class="flex items-center gap-6">
            <button class="px-8 py-4 bg-gray-900 text-white rounded-2xl font-bold hover:bg-gray-800 transition-all flex items-center gap-2 group">
              Shop Collection
              <ArrowRight class="group-hover:translate-x-1 transition-transform" size={20} />
            </button>
            <button class="text-sm font-bold border-b-2 border-gray-900 pb-1">View Lookbook</button>
          </div>
        </div>
        <div class="hidden md:block relative">
          <div class="absolute -top-20 -right-20 w-96 h-96 bg-indigo-200/50 blur-[100px] rounded-full" />
          <img src="https://images.unsplash.com/photo-1505740420928-5e560c06d30e?auto=format&fit=crop&q=80&w=1200" alt="Hero" class="relative z-10 rounded-[40px] shadow-2xl" />
        </div>
      </div>
    </section>

    <!-- Products Section -->
    <section class="py-24 max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex flex-col md:flex-row justify-between items-end mb-12 gap-8">
        <div>
          <h3 class="text-4xl font-bold tracking-tight mb-4">Featured Products</h3>
          <div class="flex flex-wrap gap-4">
            <button 
              v-for="cat in categories" 
              :key="cat"
              @click="activeCategory = cat"
              :class="activeCategory === cat ? 'bg-indigo-600 text-white' : 'bg-gray-50 text-gray-500 hover:bg-gray-100'"
              class="px-6 py-2 rounded-full text-sm font-medium transition-all"
            >
              {{ cat }}
            </button>
          </div>
        </div>
        <button class="flex items-center gap-2 text-sm font-bold border border-gray-200 px-6 py-3 rounded-2xl hover:bg-gray-50 transition-all">
          <Filter size={16} />
          Filters
        </button>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
        <div v-for="product in products" :key="product.id" class="group cursor-pointer">
          <div class="relative aspect-square overflow-hidden bg-gray-100 rounded-[32px] mb-6">
            <img :src="product.image" :alt="product.name" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" />
            <button class="absolute top-4 right-4 p-3 bg-white rounded-2xl shadow-lg opacity-0 group-hover:opacity-100 transition-all hover:text-red-500">
              <Heart size={20} />
            </button>
            <button class="absolute bottom-4 left-4 right-4 bg-white py-3 rounded-2xl font-bold shadow-lg translate-y-4 opacity-0 group-hover:translate-y-0 group-hover:opacity-100 transition-all">
              Add to Cart
            </button>
          </div>
          <div class="flex justify-between items-start mb-2">
            <h4 class="font-bold text-lg leading-tight">{{ product.name }}</h4>
            <div class="flex items-center gap-1 text-sm font-bold">
              <Star size={14} class="fill-yellow-400 text-yellow-400" />
              {{ product.rating }}
            </div>
          </div>
          <p class="text-indigo-600 font-bold">${{ product.price }}</p>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-900 text-white py-20">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid md:grid-cols-4 gap-12">
        <div class="col-span-2 space-y-6">
          <h1 class="text-3xl font-bold tracking-tighter">LUMINA.</h1>
          <p class="text-gray-400 max-w-sm leading-relaxed">
            The next generation of e-commerce experience. Built for speed, style, and simplicity.
          </p>
        </div>
        <div class="space-y-4">
          <h5 class="font-bold">Links</h5>
          <ul class="text-gray-400 space-y-2 text-sm">
            <li><a href="#" class="hover:text-white transition-colors">Shop All</a></li>
            <li><a href="#" class="hover:text-white transition-colors">Shipping</a></li>
            <li><a href="#" class="hover:text-white transition-colors">Returns</a></li>
          </ul>
        </div>
        <div class="space-y-4">
          <h5 class="font-bold">Contact</h5>
          <p class="text-gray-400 text-sm">hello@lumina.com</p>
          <div class="flex gap-4">
            <!-- Social icons here -->
          </div>
        </div>
      </div>
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 mt-20 pt-8 border-t border-white/5 text-center text-gray-500 text-sm">
        © 2026 Lumina E-commerce. Designed by Antigravity.
      </div>
    </footer>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
</style>
