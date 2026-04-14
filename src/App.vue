<script setup lang="ts">
import { ref, onMounted } from 'vue';

const currentTab = ref('HOME');
const isDarkMode = ref(true);

const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value;
  if (isDarkMode.value) {
    document.documentElement.classList.add('dark');
  } else {
    document.documentElement.classList.remove('dark');
  }
};

const tabs = ['HOME', 'LIVE', 'SOCIALS', 'PICKS'];

const scrollToSection = (tab: string) => {
  currentTab.value = tab;
  const element = document.getElementById(tab.toLowerCase());
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' });
  }
};

onMounted(() => {
  if (isDarkMode.value) {
    document.documentElement.classList.add('dark');
  }

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        currentTab.value = entry.target.id.toUpperCase();
      }
    });
  }, { threshold: 0.5 });

  tabs.forEach(tab => {
    const el = document.getElementById(tab.toLowerCase());
    if (el) observer.observe(el);
  });
});

const socials = [
  { name: 'Discord',  desc: 'Join our VIP community for daily picks and exclusive chat', icon: 'M20.317 4.3698a19.7913 19.7913 0 00-4.8851-1.5152.0741.0741 0 00-.0785.0371c-.211.3753-.4447.8648-.6083 1.2495-1.8447-.2762-3.68-.2762-5.4868 0-.1636-.3933-.4058-.8742-.6177-1.2495a.077.077 0 00-.0785-.037 19.7363 19.7363 0 00-4.8852 1.515.0699.0699 0 00-.0321.0277C.5334 9.0458-.319 13.5799.0992 18.0578a.0824.0824 0 00.0312.0561c2.0528 1.5076 4.0413 2.4228 5.9929 3.0294a.0777.0777 0 00.0842-.0276c.4616-.6304.8731-1.2952 1.226-1.9942a.076.076 0 00-.0416-.1057c-.6528-.2476-1.2743-.5495-1.8722-.8923a.077.077 0 01-.0076-.1277c.1258-.0943.2517-.1923.3718-.2914a.0743.0743 0 01.0776-.0105c3.9278 1.7933 8.18 1.7933 12.0614 0a.0739.0739 0 01.0785.0095c.1202.099.246.1981.3728.2924a.077.077 0 01-.0066.1276 12.2986 12.2986 0 01-1.873.8914.0766.0766 0 00-.0407.1067c.3604.698.7719 1.3628 1.225 1.9932a.076.076 0 00.0842.0286c1.961-.6067 3.9495-1.5219 6.0023-3.0294a.077.077 0 00.0313-.0552c.5004-5.177-.8382-9.6739-3.5485-13.6604a.061.061 0 00-.0312-.0286zM8.02 15.3312c-1.1825 0-2.1569-1.0857-2.1569-2.419 0-1.3332.9555-2.4189 2.157-2.4189 1.2108 0 2.1757 1.0952 2.1568 2.419 0 1.3333-.9555 2.4189-2.1569 2.4189zm7.9748 0c-1.1825 0-2.1569-1.0857-2.1569-2.419 0-1.3332.9554-2.4189 2.1569-2.4189 1.2108 0 2.1757 1.0952 2.1568 2.419 0 1.3333-.946 2.4189-2.1568 2.4189Z', color: 'text-indigo-500' },
  { name: 'X', desc: 'Real-time updates and live picks', icon: 'M23 3a10.9 10.9 0 01-3.14 1.53 4.48 4.48 0 00-7.86 3v1A10.66 10.66 0 013 4s-4 9 5 13a11.64 11.64 0 01-7 2c9 5 20 0 20-11.5a4.5 4.5 0 00-.08-.83A7.72 7.72 0 0023 3z', color: 'text-blue-400' },
  { name: 'Instagram', desc: 'Behind the scenes and highlights', icon: 'M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z', color: 'text-pink-500' },
];

const picks = [
  { id: 1, date: '02/14/2026', title: 'Cilic ML + Cerundolo ML + Aliassime ML + Fritz ML', odds: 2.5, wager: 250.00, units: 1, uPayout: 2.5, payout: 625.00, result: 'Win', profit: 375.00, unitsEarned: 1.5 },
  { id: 2, date: '02/14/2026', title: 'Humbert -3.5', odds: 1.6, wager: 250.00, units: 2.5, uPayout: 4.0, payout: 400.00, result: 'Win', profit: 150.00, unitsEarned: 1.5 },
  { id: 3, date: '02/14/2026', title: 'Munar (+1.5 sets) + Darderi ML', odds: 1.84, wager: 150.00, units: 1.5, uPayout: 2.8, payout: 276.00, result: 'Win', profit: 126.00, unitsEarned: 1.3 },
  { id: 4, date: '02/14/2026', title: 'Aliassime ML', odds: 1.45, wager: 300.00, units: 3, uPayout: 4.4, payout: 435.00, result: 'Win', profit: 135.00, unitsEarned: 1.4 },
  { id: 5, date: '02/14/2026', title: 'Halys ML + Vukic ML', odds: 1.69, wager: 150.00, units: 1.5, uPayout: 0.0, payout: 0.00, result: 'Loss', profit: -150.00, unitsEarned: -1.5 },
  { id: 6, date: '02/14/2026', title: 'Mboko (+1.5 sets) + De Minaur ML', odds: 1.78, wager: 150.00, units: 1.5, uPayout: 0.0, payout: 0.00, result: 'Loss', profit: -150.00, unitsEarned: -1.5 },
  { id: 7, date: '02/14/2026', title: 'Iowa State -4.5', odds: 1.53, wager: 300.00, units: 3, uPayout: 4.6, payout: 459.00, result: 'Win', profit: 159.00, unitsEarned: 1.6 },
  { id: 8, date: '02/14/2026', title: 'Shelton ML', odds: 1.49, wager: 250.00, units: 2.5, uPayout: 3.7, payout: 372.50, result: 'Win', profit: 122.50, unitsEarned: 1.2 },
  { id: 9, date: '02/14/2026', title: 'Granollers/ Zeballos ML + Aliassime ML + Passaro ML', odds: 2.82, wager: 200.00, units: 2, uPayout: 5.6, payout: 564.00, result: 'Win', profit: 364.00, unitsEarned: 3.6 },
];

const livePicks = [
  { id: 1, sport: 'Tennis', match: 'Alcaraz vs Sinner', time: 'Live - Set 2', title: 'Alcaraz Next Break', odds: '+150', confidence: 'High', color: 'border-blue-500' },
  { id: 2, sport: 'Basketball', match: 'Lakers vs Celtics', time: 'Q3 - 5:40', title: 'Over 220.5 Total Points', odds: '-110', confidence: 'Medium', color: 'border-orange-500' },
  { id: 3, sport: 'Soccer', match: 'Real Madrid vs Barcelona', time: 'HT - 0:0', title: 'Next Goal: Real Madrid', odds: '+120', confidence: 'High', color: 'border-emerald-500' },
];

const formatCurrency = (value: number) => {
  return new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD' }).format(value);
};
</script>

<template>
  <div class="min-h-screen bg-white dark:bg-[#09090b] text-gray-900 dark:text-gray-100 font-sans relative overflow-x-hidden transition-colors duration-500">

    <!-- Navbar -->
    <nav class="fixed top-0 left-0 right-0 z-50 flex items-center justify-between px-6 md:px-8 py-4 border-b border-gray-200 dark:border-white/5 bg-white/80 dark:bg-[#09090b]/80 backdrop-blur-xl transition-colors duration-500">
      <div class="flex items-center gap-3 cursor-pointer" @click="scrollToSection('HOME')">
        <span class="text-2xl font-black italic text-gray-900 dark:text-white tracking-tighter hidden sm:block">Marko Picks</span>
      </div>

      <div class="hidden md:flex items-center gap-8 bg-gray-100/50 dark:bg-white/5 px-2 py-1.5 rounded-xl border border-gray-200 dark:border-white/5">
        <button 
          v-for="tab in tabs" 
          :key="tab"
          @click="scrollToSection(tab)"
          class="font-medium tracking-wide transition-all duration-300 text-xs px-4 py-2 rounded-lg"
          :class="currentTab === tab ? 'text-gray-900 dark:text-white bg-white dark:bg-white/10 shadow-sm' : 'text-gray-500 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white'"
        >
          {{ tab }}
        </button>
      </div>

      <div class="flex items-center gap-4 md:gap-6">
        <!-- Dark Mode Toggle Switch -->
        <div @click="toggleDarkMode" class="w-12 h-6 rounded-full flex items-center px-1 cursor-pointer transition-colors duration-300 border" :class="isDarkMode ? 'bg-[#18181b] border-white/10' : 'bg-gray-200 border-gray-300'">
          <div class="w-4 h-4 rounded-full bg-white shadow-sm transform transition-transform duration-300 flex items-center justify-center" :class="isDarkMode ? 'translate-x-6' : 'translate-x-0'">
            <svg v-if="!isDarkMode" class="w-3 h-3 text-yellow-500" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z" clip-rule="evenodd"></path></svg>
            <svg v-else class="w-3 h-3 text-gray-800" fill="currentColor" viewBox="0 0 20 20"><path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z"></path></svg>
          </div>
        </div>
      </div>
    </nav>

    <!-- Main Content -->
    <main class="relative z-10 flex flex-col w-full">
      
      <!-- HOME SECTION -->
      <section id="home" class="min-h-screen flex items-center justify-center pt-24 pb-16 px-6">
        <!-- Ambient light effect -->
        <div v-if="isDarkMode" class="absolute top-1/3 left-1/4 w-[500px] h-[500px] bg-blue-600/10 rounded-full blur-[100px] pointer-events-none -z-10"></div>
        <div v-if="!isDarkMode" class="absolute top-1/3 left-1/4 w-[500px] h-[500px] bg-blue-600/5 rounded-full blur-[100px] pointer-events-none -z-10"></div>

        <div class="max-w-6xl w-full flex flex-col lg:flex-row items-center justify-between gap-16">
          <div class="flex-1 space-y-6 text-center lg:text-left relative z-10">
            <div class="inline-flex items-center gap-2 bg-blue-50 dark:bg-blue-500/10 text-blue-600 dark:text-blue-400 px-4 py-1.5 rounded-full font-semibold text-xs tracking-widest uppercase border border-blue-200 dark:border-blue-500/20">
              <div class="w-1.5 h-1.5 rounded-full bg-blue-600"></div>
              Expert Analysis
            </div>
            
            <h1 class="text-6xl md:text-8xl font-extrabold text-gray-900 dark:text-white tracking-tighter transition-colors duration-500">
              MARKO <br/><span class="text-blue-600 dark:text-blue-500">PICKS</span>
            </h1>
            <h2 class="text-lg md:text-xl font-medium text-gray-500 dark:text-gray-400 transition-colors duration-500 max-w-lg mx-auto lg:mx-0 leading-relaxed">
              Elevate your betting game with data-driven insights, daily premium picks, and an exclusive community.
            </h2>
            
            <div class="flex flex-col sm:flex-row items-center justify-center lg:justify-start gap-4 pt-6">
              <button class="w-full sm:w-auto bg-gray-900 dark:bg-white hover:bg-gray-800 dark:hover:bg-gray-100 text-white dark:text-gray-900 font-semibold py-3.5 px-8 rounded-xl transition-all shadow-lg flex items-center justify-center gap-2">
                Get VIP Access
              </button>
              <button @click="scrollToSection('PICKS')" class="w-full sm:w-auto bg-white dark:bg-[#18181b] border border-gray-200 dark:border-white/10 text-gray-700 dark:text-gray-300 hover:bg-gray-50 dark:hover:bg-[#27272a] font-semibold py-3.5 px-8 rounded-xl transition-all shadow-sm flex items-center justify-center gap-2">
                View Latest Picks
              </button>
            </div>
          </div>
          
          <!-- Official Partner Card -->
          <div class="flex-1 w-full max-w-md bg-white dark:bg-[#18181b] rounded-3xl p-8 border border-gray-200 dark:border-white/5 relative shadow-2xl dark:shadow-2xl dark:shadow-black transition-colors duration-500 z-10">
            <div class="flex justify-center mb-8 relative">
              <div class="text-6xl font-black italic tracking-tighter text-gray-900 dark:text-white transition-colors duration-500">
                Stake
              </div>
            </div>
            
            <h3 class="text-center text-xs text-gray-400 dark:text-gray-500 font-bold tracking-[0.2em] mb-6 uppercase transition-colors duration-500">Official Partner</h3>
            
            <div class="bg-gray-50 dark:bg-[#0f0f11] rounded-2xl p-6 border border-gray-100 dark:border-white/5 transition-colors duration-500">
              <h4 class="text-center font-bold text-gray-900 dark:text-white mb-2 transition-colors duration-500">READY TO PLAY?</h4>
              <p class="text-center text-sm text-gray-500 dark:text-gray-400 mb-6 transition-colors duration-500">Join the ultimate sports betting experience</p>
              
              <button class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-4 px-5 rounded-xl flex items-center justify-between shadow-lg shadow-blue-600/20 transition-all mb-6">
                <div class="flex items-center gap-3">
                  <div class="w-8 h-8 rounded-full bg-white/20 flex items-center justify-center">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                  </div>
                  <div class="text-left">
                    <div class="text-sm">Join Stake Now</div>
                    <div class="text-[10px] font-normal opacity-90">Get Exclusive Bonuses</div>
                  </div>
                </div>
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"></path></svg>
              </button>
              
              <div class="text-center">
                <div class="text-[10px] text-gray-400 dark:text-gray-500 mb-3 font-semibold uppercase tracking-widest transition-colors duration-500">Quick Access</div>
                <div class="flex justify-center gap-2">
                  <button class="bg-white dark:bg-[#18181b] text-xs px-4 py-2 rounded-lg text-gray-600 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white border border-gray-200 dark:border-white/5 transition-colors duration-500 shadow-sm font-medium">Stake.games</button>
                  <button class="bg-white dark:bg-[#18181b] text-xs px-4 py-2 rounded-lg text-gray-600 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white border border-gray-200 dark:border-white/5 transition-colors duration-500 shadow-sm font-medium">Stake.com</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- LIVE PICKS SECTION -->
      <section id="live" class="min-h-screen flex items-center justify-center py-20 px-6 border-t border-gray-200 dark:border-white/5 bg-gray-50/50 dark:bg-black/20">
        <div class="max-w-6xl w-full flex flex-col items-center">
          <div class="inline-flex items-center gap-2 bg-red-50 dark:bg-red-500/10 text-red-600 dark:text-red-500 px-4 py-1.5 rounded-full font-semibold text-xs tracking-widest uppercase mb-6 border border-red-200 dark:border-red-500/20">
            <div class="w-2 h-2 rounded-full bg-red-500 animate-pulse"></div>
            Live Action
          </div>
          <h2 class="text-4xl md:text-5xl font-bold mb-4 text-gray-900 dark:text-white tracking-tight transition-colors duration-500 text-center">
            In-Play Picks
          </h2>
          <p class="text-gray-500 dark:text-gray-400 mb-16 transition-colors duration-500 text-center text-lg max-w-xl">
            Real-time value. Jump on these live betting opportunities before the odds shift.
          </p>
          
          <div class="grid grid-cols-1 md:grid-cols-3 gap-6 w-full">
            <div v-for="pick in livePicks" :key="pick.id" 
                 class="bg-white dark:bg-[#18181b] rounded-3xl p-6 border-t-4 border-l border-r border-b border-gray-200 dark:border-white/5 flex flex-col transition-all duration-300 shadow-sm hover:shadow-xl hover:-translate-y-1 relative overflow-hidden"
                 :class="pick.color">
              
              <!-- Live Indicator Background Glow -->
              <div class="absolute -top-10 -right-10 w-32 h-32 bg-red-500/5 dark:bg-red-500/10 rounded-full blur-2xl pointer-events-none"></div>

              <div class="flex justify-between items-start mb-6">
                <div>
                  <span class="text-xs font-bold text-gray-400 dark:text-gray-500 uppercase tracking-widest">{{ pick.sport }}</span>
                  <div class="text-sm font-semibold text-gray-900 dark:text-white mt-1">{{ pick.match }}</div>
                </div>
                <span class="px-3 py-1 rounded-full text-[10px] font-bold uppercase tracking-wider bg-red-50 dark:bg-red-500/10 text-red-600 dark:text-red-400 border border-red-200/50 dark:border-red-500/20 flex items-center gap-1.5">
                  <div class="w-1.5 h-1.5 rounded-full bg-red-500 animate-pulse"></div>
                  {{ pick.time }}
                </span>
              </div>

              <h3 class="text-xl font-bold text-gray-900 dark:text-white mb-6 leading-snug flex-1">{{ pick.title }}</h3>

              <div class="bg-gray-50 dark:bg-[#0f0f11] rounded-2xl p-4 border border-gray-100 dark:border-white/5 mb-6">
                <div class="flex justify-between items-center">
                  <span class="text-xs font-semibold text-gray-500 uppercase">Current Odds</span>
                  <span class="text-xl font-black text-gray-900 dark:text-white">{{ pick.odds }}</span>
                </div>
              </div>

              <div class="flex items-center justify-between mt-auto pt-4 border-t border-gray-100 dark:border-white/5">
                <div class="flex items-center gap-2">
                  <span class="text-xs text-gray-500 font-medium uppercase tracking-wider">Confidence:</span>
                  <span class="text-xs font-bold px-2 py-1 rounded bg-blue-50 dark:bg-blue-500/10 text-blue-600 dark:text-blue-400">{{ pick.confidence }}</span>
                </div>
                <button class="bg-gray-900 dark:bg-white text-white dark:text-gray-900 hover:bg-gray-800 dark:hover:bg-gray-200 text-xs font-bold py-2 px-4 rounded-lg transition-colors">
                  Tail Pick
                </button>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- SOCIALS SECTION -->
      <section id="socials" class="min-h-screen flex items-center justify-center py-20 px-6 border-t border-gray-200 dark:border-white/5">
        <div class="max-w-5xl w-full flex flex-col items-center">
          <div class="inline-flex items-center gap-2 bg-gray-100 dark:bg-white/5 text-gray-600 dark:text-gray-300 px-4 py-1.5 rounded-full font-semibold text-xs tracking-widest uppercase mb-6">
            Community
          </div>
          <h2 class="text-4xl md:text-5xl font-bold mb-4 text-gray-900 dark:text-white tracking-tight transition-colors duration-500 text-center">Connect With Us</h2>
          <p class="text-gray-500 dark:text-gray-400 text-center max-w-xl mb-16 transition-colors duration-500 text-lg">
            Join thousands of others in our community. Get real-time updates, daily breakdowns, and exclusive behind-the-scenes content.
          </p>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6 w-full">
            <div v-for="social in socials" :key="social.name" class="group bg-white dark:bg-[#18181b] border border-gray-200 dark:border-white/5 rounded-3xl p-8 flex flex-col hover:border-blue-600/30 dark:hover:border-blue-600/30 transition-all duration-300 shadow-sm hover:shadow-xl hover:shadow-blue-600/5">
              <div class="flex items-center gap-5 mb-4">
                <div class="w-14 h-14 rounded-2xl bg-gray-50 dark:bg-white/5 flex items-center justify-center border border-gray-100 dark:border-white/5 group-hover:scale-110 transition-transform duration-300">
                  <svg class="w-7 h-7 transition-colors duration-500" :class="social.color" fill="currentColor" viewBox="0 0 24 24">
                    <path :d="social.icon"></path>
                  </svg>
                </div>
                <div>
                  <h3 class="text-xl font-bold text-gray-900 dark:text-white transition-colors duration-500">{{ social.name }}</h3>
                  <p class="text-blue-600 dark:text-blue-500 text-sm font-medium transition-colors duration-500">{{ social.followers }}</p>
                </div>
              </div>
              <p class="text-gray-500 dark:text-gray-400 text-sm mt-2 mb-8 flex-1 leading-relaxed transition-colors duration-500">{{ social.desc }}</p>
              <button class="w-full bg-gray-50 dark:bg-white/5 hover:bg-blue-600 dark:hover:bg-blue-600 text-gray-700 dark:text-gray-300 hover:text-white dark:hover:text-white font-semibold py-3.5 rounded-xl transition-all duration-300 border border-gray-200 dark:border-transparent">
                Follow {{ social.name }}
              </button>
            </div>
          </div>
        </div>
      </section>

      <!-- PICKS SECTION -->
      <section id="picks" class="min-h-screen flex items-center justify-center py-20 px-6 border-t border-gray-200 dark:border-white/5">
        <div class="max-w-6xl w-full flex flex-col items-center">
          <div class="inline-flex items-center gap-2 bg-blue-50 dark:bg-blue-500/10 text-blue-600 dark:text-blue-400 px-4 py-1.5 rounded-full font-semibold text-xs tracking-widest uppercase mb-6 border border-blue-200 dark:border-blue-500/20">
            Performance
          </div>
          <h2 class="text-4xl md:text-5xl font-bold mb-4 text-gray-900 dark:text-white tracking-tight transition-colors duration-500 text-center">
            Recent Picks
          </h2>
          <p class="text-gray-500 dark:text-gray-400 mb-16 transition-colors duration-500 text-center text-lg max-w-xl">
            Complete transparency on our recent plays. Track our odds, wagers, and overall profit.
          </p>
          
          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 w-full">
            <div v-for="pick in picks" :key="pick.id" 
                 class="bg-white dark:bg-[#18181b] rounded-3xl p-6 border border-gray-200 dark:border-white/5 flex flex-col transition-all duration-300 shadow-sm hover:shadow-xl hover:-translate-y-1"
                 :class="pick.result === 'Win' ? 'hover:shadow-emerald-500/10' : 'hover:shadow-red-500/10'">
              
              <div class="flex justify-between items-start mb-4">
                <span class="text-xs font-semibold text-gray-500 dark:text-gray-400">{{ pick.date }}</span>
                <span class="px-3 py-1 rounded-full text-xs font-bold uppercase tracking-wider"
                      :class="pick.result === 'Win' ? 'bg-emerald-100 text-emerald-700 dark:bg-emerald-500/10 dark:text-emerald-400' : 'bg-red-100 text-red-700 dark:bg-red-500/10 dark:text-red-400'">
                  {{ pick.result }}
                </span>
              </div>

              <h3 class="text-lg font-bold text-gray-900 dark:text-white mb-6 leading-snug flex-1">{{ pick.title }}</h3>

              <div class="grid grid-cols-2 gap-4 mb-6">
                <div class="bg-gray-50 dark:bg-[#0f0f11] p-3 rounded-xl border border-gray-100 dark:border-white/5">
                  <div class="text-[10px] text-gray-500 uppercase font-semibold mb-1">Odds</div>
                  <div class="font-bold text-gray-900 dark:text-white">{{ pick.odds }}</div>
                </div>
                <div class="bg-gray-50 dark:bg-[#0f0f11] p-3 rounded-xl border border-gray-100 dark:border-white/5">
                  <div class="text-[10px] text-gray-500 uppercase font-semibold mb-1">Units</div>
                  <div class="font-bold text-gray-900 dark:text-white">{{ pick.units }}</div>
                </div>
                <div class="bg-gray-50 dark:bg-[#0f0f11] p-3 rounded-xl border border-gray-100 dark:border-white/5">
                  <div class="text-[10px] text-gray-500 uppercase font-semibold mb-1">Wager</div>
                  <div class="font-bold text-gray-900 dark:text-white">{{ formatCurrency(pick.wager) }}</div>
                </div>
                <div class="bg-gray-50 dark:bg-[#0f0f11] p-3 rounded-xl border border-gray-100 dark:border-white/5">
                  <div class="text-[10px] text-gray-500 uppercase font-semibold mb-1">Payout</div>
                  <div class="font-bold text-gray-900 dark:text-white">{{ formatCurrency(pick.payout) }}</div>
                </div>
              </div>

              <div class="pt-4 border-t border-gray-100 dark:border-white/5 flex justify-between items-center">
                <div class="text-sm font-semibold text-gray-500 dark:text-gray-400">Total Profit</div>
                <div class="text-lg font-black" :class="pick.profit > 0 ? 'text-emerald-600 dark:text-emerald-500' : 'text-red-600 dark:text-red-500'">
                  {{ pick.profit > 0 ? '+' : '' }}{{ formatCurrency(pick.profit) }}
                </div>
              </div>
            </div>
          </div>

        </div>
      </section>

    </main>

    <!-- Footer -->
    <footer class="relative z-10 border-t border-gray-200 dark:border-white/5 bg-white dark:bg-[#09090b] py-12 px-6 transition-colors duration-500">
      <div class="max-w-6xl mx-auto flex flex-col md:flex-row items-center justify-between gap-6">
        <div class="flex items-center gap-3">
          <span class="font-bold text-gray-900 dark:text-white transition-colors duration-500 tracking-tight">MARKO PICKS</span>
        </div>
        <p class="text-sm text-gray-500 dark:text-gray-400 transition-colors duration-500 font-medium">
          &copy; {{ new Date().getFullYear() }} Marko Picks. All rights reserved.
        </p>
        <div class="flex gap-6">
          <a href="#" class="text-sm font-medium text-gray-500 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white transition-colors">Terms</a>
          <a href="#" class="text-sm font-medium text-gray-500 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white transition-colors">Privacy</a>
        </div>
      </div>
    </footer>

  </div>
</template>
