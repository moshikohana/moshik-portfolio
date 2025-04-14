<script lang="ts">
  import { writable } from 'svelte/store';
  import MoshikPortfolioEnglish from './MoshikPortfolio.svelte';
  import { Globe, Github, Linkedin, Mail, Phone, Code, Terminal, Braces, Hash, FileCode, Database, Star, Cloud, Cpu, Coffee, Laptop, Layers, ServerCrash } from 'lucide-svelte';
  import UIStyles from './templates/UIStyles.svelte';
  import { onMount } from 'svelte';
  
  // Language store
  const language = writable('english'); // english or hebrew
  
  // Toggle language function
  function toggleLanguage() {
    language.update(lang => lang === 'english' ? 'hebrew' : 'english');
  }

  // Animation variables
  interface Icon {
    component: any;
    color: string;
    x: number;
    y: number;
    size: number;
    speedX: number;
    speedY: number;
    rotation: number;
    rotationSpeed: number;
    opacity: number;
    scale: number;
  }
  
  let icons: Icon[] = [];
  let particlesVisible = false;
  
  onMount(() => {
    const iconComponents = [
      Code, Terminal, Braces, Hash, Github, 
      Linkedin, FileCode, Database, Star, Cloud, 
      Cpu, Coffee, Laptop, Layers, ServerCrash
    ];
    const colors = [
      '#4E85C3', '#4AA6B5', '#7FBFCF', '#C0E5F7', 
      '#D0D0D0', '#E5E5E5', '#6A82FB', '#FC5C7D',
      '#8E54E9', '#4776E6', '#8A5CF5'
    ];
    
    // Set particles visible after a small delay for initial animation
    setTimeout(() => {
      particlesVisible = true;
    }, 500);
    
    for (let i = 0; i < 25; i++) {
      const randomComponent = iconComponents[Math.floor(Math.random() * iconComponents.length)];
      const randomColor = colors[Math.floor(Math.random() * colors.length)];
      
      icons.push({
        component: randomComponent,
        color: randomColor,
        x: Math.random() * 100,
        y: Math.random() * 100,
        size: Math.random() * 30 + 15,
        speedX: (Math.random() - 0.5) * 0.2,
        speedY: (Math.random() - 0.5) * 0.2,
        rotation: Math.random() * 360,
        rotationSpeed: (Math.random() - 0.5) * 0.5,
        opacity: Math.random() * 0.2 + 0.05,
        scale: Math.random() * 0.3 + 0.9
      });
    }
    
    // Animation loop
    function animate() {
      icons = icons.map(icon => {
        // Update position
        icon.x += icon.speedX;
        icon.y += icon.speedY;
        icon.rotation += icon.rotationSpeed;
        
        // Bounce off edges
        if (icon.x < 0 || icon.x > 100) icon.speedX *= -1;
        if (icon.y < 0 || icon.y > 100) icon.speedY *= -1;
        
        return icon;
      });
      
      // Continue animation
      requestAnimationFrame(animate);
    }
    
    // Start animation
    animate();
  });
</script>

<!-- Language selector with enhanced styling -->
<div class="fixed top-4 right-4 z-50">
  <button 
    on:click={toggleLanguage}
    class="flex items-center gap-2 bg-slate-800/80 backdrop-blur-sm text-white px-3 py-2 rounded-lg border border-slate-600 hover:bg-slate-700 transition-all duration-300 hover:scale-105 hover:shadow-glow"
  >
    <Globe size={16} class="animate-spin-slow" />
    <span>{$language === 'english' ? 'עברית' : 'English'}</span>
  </button>
</div>

<!-- Particles background (appears in both language versions) -->
{#if particlesVisible}
  <div class="fixed inset-0 -z-10 particles-bg"></div>
{/if}

<!-- English Version -->
{#if $language === 'english'}
  <MoshikPortfolioEnglish />
{:else}
  <!-- Hebrew Version -->
  <div class="bg-gradient-primary text-white min-h-screen rtl">
    <!-- Hero Section with Hebrew text -->
    <section class="relative overflow-hidden py-24 px-4 sm:px-6 lg:px-8">
      <!-- Matrix-style code rain background -->
      <div class="absolute inset-0 opacity-5" style="background-image: url('data:image/svg+xml,%3csvg xmlns=\'http://www.w3.org/2000/svg\' viewBox=\'0 0 32 32\' width=\'32\' height=\'32\' fill=\'none\' stroke=\'rgb(255 255 255 / 0.05)\'%3e%3cpath d=\'M0 .5H31.5V32\'/%3e%3c/svg%3e'); background-size: 40px 40px;"></div>
      
      <!-- Animated background gradient -->
      <div class="absolute inset-0 bg-gradient-to-br from-indigo-900/20 via-purple-900/20 to-pink-900/20 animate-gradient-slow"></div>
      
      <!-- Enhanced grid lines with subtle animation -->
      <div class="absolute inset-0 grid-lines"></div>
      
      <!-- Floating tech icons with enhanced animations -->
      <div class="absolute inset-0 overflow-hidden pointer-events-none">
        {#each icons as icon}
          <div 
            class="absolute transform transition-all duration-[5000ms] ease-in-out animate-float"
            style="left: {icon.x}%; top: {icon.y}%; opacity: {icon.opacity}; transform: rotate({icon.rotation}deg) scale({icon.scale});"
          >
            <svelte:component this={icon.component} size={icon.size} style="color: {icon.color}" />
          </div>
        {/each}
      </div>
      
      <div class="relative max-w-5xl mx-auto text-center">
        <div class="mb-8 inline-flex items-center justify-center rounded-full bg-indigo-500/10 px-3 py-1 text-sm font-medium text-indigo-400 ring-1 ring-inset ring-indigo-500/20 animate-pulse-subtle hover:scale-105 transition-transform duration-300">
          <Star size={16} class="ml-1 animate-sparkle" />
          <span>זמין להזדמנויות חדשות</span>
        </div>
        
        <h1 class="text-4xl sm:text-6xl font-bold mb-6 bg-clip-text text-transparent bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 animate-title-gradient">
          מושיק אוחנה
        </h1>
        
        <p class="max-w-2xl mx-auto text-lg text-slate-300 mb-10 animate-fade-up">
          מפתח Full Stack ותלמיד מדעי המחשב
        </p>
        
        <div class="flex flex-wrap justify-center gap-4">
          <a href="#contact" class="inline-flex items-center gap-2 px-6 py-3 rounded-lg bg-indigo-600 hover:bg-indigo-700 text-white font-medium transition-colors relative overflow-hidden group">
            <span class="relative z-10">צור קשר</span>
            <span class="absolute inset-0 bg-gradient-to-r from-purple-600 to-indigo-600 opacity-0 group-hover:opacity-100 transition-opacity"></span>
          </a>
          
          <a href="/Moshik_Ohana_Resume.pdf" class="inline-flex items-center gap-2 px-6 py-3 rounded-lg bg-slate-700 hover:bg-slate-600 text-white font-medium transition-colors relative overflow-hidden group" download>
            <span class="relative z-10">צפה בקורות חיים</span>
            <span class="absolute inset-0 bg-gradient-to-r from-slate-600 to-slate-500 opacity-0 group-hover:opacity-100 transition-opacity"></span>
          </a>
        </div>
      </div>
      
      <!-- Enhanced animated background gradients -->
      <div class="absolute -top-40 -right-40 w-80 h-80 bg-indigo-600 rounded-full opacity-30 blur-3xl animate-blob animation-infinite glow"></div>
      <div class="absolute -bottom-40 -left-40 w-80 h-80 bg-purple-600 rounded-full opacity-30 blur-3xl animate-blob animation-delay-2000 animation-infinite glow"></div>
      <div class="absolute top-1/2 left-1/4 w-64 h-64 bg-blue-600 rounded-full opacity-20 blur-3xl animate-blob animation-delay-4000 animation-infinite glow"></div>
    </section>
    
    <!-- About Me Section in Hebrew -->
    <section class="py-16 px-4 sm:px-6 lg:px-8">
      <div class="max-w-3xl mx-auto">
        <h2 class="text-2xl font-bold mb-6 bg-clip-text text-transparent bg-gradient-to-r from-indigo-400 to-cyan-400 text-center animate-title-gradient">אודותיי</h2>
        <div class="bg-slate-700/50 p-6 rounded-xl border border-slate-600 backdrop-blur-sm hover:shadow-glow transition-all duration-300 card-hover">
          <p class="text-slate-300 mb-4">
            סטודנט בשנה השנייה למדעי המחשב באוניברסיטה הפתוחה עם הוכחת יכולת בלמידה מהירה, כישורי אנוש מצוינים, ויכולת לנהל משימות מרובות ביעילות.
          </p>
          <p class="text-slate-300">
            בעל יכולת הסתגלות חזקה לסביבות חדשות ומדגים יכולות למידה עצמית. סיים תכנית פיתוח Full Stack במכללת ג'ון ברייס.
            בעל ניסיון בדיפלומטיה ציבורית, ניהול אבטחה, ניהול אתרים ויצירת תוכן.
          </p>
        </div>
      </div>
    </section>
    
    <!-- Hebrew Skills Section -->
    <section class="py-16 px-4 sm:px-6 lg:px-8 bg-slate-800/50">
      <div class="max-w-7xl mx-auto">
        <h2 class="text-2xl font-bold text-center mb-12">
          <span class="bg-clip-text text-transparent bg-gradient-to-r from-indigo-400 to-cyan-400 animate-title-gradient">
            כישורים ומומחיות
          </span>
        </h2>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <!-- Programming Languages -->
          <div class="bg-slate-700/50 p-6 rounded-xl border border-slate-600 backdrop-blur-sm hover:shadow-glow transition-all duration-300 card-hover">
            <div class="w-12 h-12 rounded-lg bg-indigo-500/20 flex items-center justify-center mb-4 animate-float animation-delay-random">
              <Code class="text-indigo-400" size={24} />
            </div>
            <h3 class="text-xl font-semibold mb-2">שפות תכנות</h3>
            <p class="text-slate-300">Java, Python, C, C#, JavaScript, TypeScript, SQL, HTML, PHP</p>
          </div>
          
          <!-- Frameworks -->
          <div class="bg-slate-700/50 p-6 rounded-xl border border-slate-600 backdrop-blur-sm hover:shadow-glow transition-all duration-300 card-hover">
            <div class="w-12 h-12 rounded-lg bg-purple-500/20 flex items-center justify-center mb-4 animate-float animation-delay-random">
              <Layers class="text-purple-400" size={24} />
            </div>
            <h3 class="text-xl font-semibold mb-2">ספריות ופריימוורקים</h3>
            <p class="text-slate-300">Node.js, Angular, Next.js, React</p>
          </div>
          
          <!-- Databases -->
          <div class="bg-slate-700/50 p-6 rounded-xl border border-slate-600 backdrop-blur-sm hover:shadow-glow transition-all duration-300 card-hover">
            <div class="w-12 h-12 rounded-lg bg-pink-500/20 flex items-center justify-center mb-4 animate-float animation-delay-random">
              <Database class="text-pink-400" size={24} />
            </div>
            <h3 class="text-xl font-semibold mb-2">מסדי נתונים</h3>
            <p class="text-slate-300">SQL Server, MongoDB</p>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Contact Section in Hebrew -->
    <section id="contact" class="py-16 px-4 sm:px-6 lg:px-8 bg-gradient-to-r from-indigo-900/50 to-purple-900/50">
      <div class="max-w-3xl mx-auto text-center">
        <h2 class="text-3xl font-bold mb-8 bg-clip-text text-transparent bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 animate-title-gradient">צור קשר</h2>
        
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 max-w-xl mx-auto mb-8">
          <a href="mailto:moshikoohana@gmail.com" class="bg-slate-700/50 p-4 rounded-xl flex items-center hover:border-indigo-500 transition-all duration-300 border border-slate-600 backdrop-blur-sm hover:shadow-glow">
            <Mail class="text-indigo-400 ml-3 animate-float" size={20} />
            <span>moshikoohana@gmail.com</span>
          </a>
          
          <a href="tel:+972524243250" class="bg-slate-700/50 p-4 rounded-xl flex items-center hover:border-indigo-500 transition-all duration-300 border border-slate-600 backdrop-blur-sm hover:shadow-glow">
            <Phone class="text-purple-400 ml-3 animate-float" size={20} />
            <span>+972 52 424 3250</span>
          </a>
        </div>
        
        <a href="/Moshik_Ohana_Resume.pdf" class="inline-flex items-center gap-2 px-6 py-3 rounded-lg bg-indigo-600 hover:bg-indigo-700 text-white font-medium transition-all duration-300 hover:scale-105 hover:shadow-glow" download>
          <span>הורד קורות חיים</span>
        </a>
      </div>
    </section>
    
    <!-- Footer -->
    <footer class="py-6 px-4 sm:px-6 lg:px-8 bg-slate-900 border-t border-slate-800">
      <div class="max-w-7xl mx-auto text-center text-slate-400 text-sm">
        <p>© {new Date().getFullYear()} מושיק אוחנה. כל הזכויות שמורות.</p>
      </div>
    </footer>
  </div>
{/if}

<style>
  :global(.rtl) {
    direction: rtl;
    text-align: right;
  }
  
  @keyframes gradient-shift {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  
  .animate-gradient-slow {
    animation: gradient-shift 15s ease infinite;
    background-size: 400% 400%;
  }
  
  /* Enhanced animations */
  @keyframes float {
    0% { transform: translateY(0) translateX(0) rotate(0) scale(1); }
    25% { transform: translateY(-10px) translateX(5px) rotate(5deg) scale(1.05); }
    50% { transform: translateY(0) translateX(10px) rotate(10deg) scale(1); }
    75% { transform: translateY(10px) translateX(5px) rotate(5deg) scale(0.95); }
    100% { transform: translateY(0) translateX(0) rotate(0) scale(1); }
  }
  
  .animate-float {
    animation: float 15s ease-in-out infinite;
  }
  
  .animation-delay-random {
    animation-delay: calc(var(--random, 0) * 5s);
  }
  
  @keyframes spin-slow {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }
  
  .animate-spin-slow {
    animation: spin-slow 8s linear infinite;
  }
  
  /* Grid lines animation */
  .grid-lines {
    background-size: 50px 50px;
    background-image:
      linear-gradient(to right, rgba(255, 255, 255, 0.02) 1px, transparent 1px),
      linear-gradient(to bottom, rgba(255, 255, 255, 0.02) 1px, transparent 1px);
    animation: grid-pulse 8s infinite alternate;
  }
  
  @keyframes grid-pulse {
    0% {
      opacity: 0.3;
      background-size: 50px 50px;
    }
    100% {
      opacity: 0.1;
      background-size: 55px 55px;
    }
  }
  
  /* Particles background */
  .particles-bg {
    background-image: 
      radial-gradient(circle, rgba(99, 102, 241, 0.05) 1px, transparent 1px),
      radial-gradient(circle, rgba(168, 85, 247, 0.05) 1px, transparent 1px);
    background-size: 50px 50px, 30px 30px;
    background-position: 0 0, 25px 25px;
    animation: particles-float 20s linear infinite;
    opacity: 0; 
    transition: opacity 1s ease-in-out;
    animation: fade-in 1s forwards;
  }
  
  @keyframes particles-float {
    0% { background-position: 0 0, 25px 25px; }
    100% { background-position: 50px 50px, 75px 75px; }
  }
  
  @keyframes fade-in {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  
  /* Title gradient animation */
  @keyframes title-gradient {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
  }
  
  .animate-title-gradient {
    background-size: 200% auto;
    animation: title-gradient 5s ease infinite;
  }
  
  /* Hover effects */
  .hover\:shadow-glow:hover {
    box-shadow: 0 0 15px rgba(99, 102, 241, 0.4);
  }
  
  .card-hover {
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  
  .card-hover:hover {
    transform: translateY(-5px);
  }
  
  /* Sparkle animation */
  @keyframes sparkle {
    0%, 100% {
      transform: scale(1);
      opacity: 1;
    }
    50% {
      transform: scale(1.2);
      opacity: 0.7;
    }
  }
  
  .animate-sparkle {
    animation: sparkle 2s ease-in-out infinite;
  }
  
  /* Pulse subtle animation */
  @keyframes pulse-subtle {
    0%, 100% {
      opacity: 1;
    }
    50% {
      opacity: 0.7;
    }
  }
  
  .animate-pulse-subtle {
    animation: pulse-subtle 3s infinite;
  }
  
  /* Glow effect */
  .glow {
    box-shadow: 0 0 60px 30px rgba(99, 102, 241, 0.2);
    animation: glow-pulse 4s ease-in-out infinite alternate;
  }
  
  @keyframes glow-pulse {
    0% {
      box-shadow: 0 0 60px 30px rgba(99, 102, 241, 0.1);
    }
    100% {
      box-shadow: 0 0 80px 40px rgba(99, 102, 241, 0.2);
    }
  }
</style> 