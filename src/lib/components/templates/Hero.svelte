<script lang="ts">
  import { onMount, onDestroy } from 'svelte';
  import { Sparkles, Code, Terminal, Braces, Hash, Github, Linkedin, FileCode, Database, Globe, Server, Cloud, Cpu, Coffee, Laptop } from 'lucide-svelte';
  
  // Props for customization
  export let title = "Your Name";
  export let subtitle = "Your Title or Tagline";
  export let badgeText = "Available for Hire";
  export let primaryButtonText = "Contact Me";
  export let primaryButtonLink = "#contact";
  export let secondaryButtonText = "View Resume";
  export let secondaryButtonLink = "#experience";
  
  // Element references
  let heroElement: HTMLElement;
  let codeContainerRef: HTMLElement;
  
  // Code elements for background
  const codeSnippets = [
    { id: 1, text: "function optimizePortfolio() {", delay: 0, color: "text-blue-400" },
    { id: 2, text: "  const skills = ['JavaScript', 'React', 'Svelte'];", delay: 200, color: "text-indigo-400" },
    { id: 3, text: "  return experience.map(job => ({", delay: 400, color: "text-purple-400" },
    { id: 4, text: "    ...job,", delay: 600, color: "text-pink-400" },
    { id: 5, text: "    highlight: job.skills.filter(s => skills.includes(s))", delay: 800, color: "text-rose-400" },
    { id: 6, text: "  }));", delay: 1000, color: "text-purple-400" },
    { id: 7, text: "}", delay: 1200, color: "text-blue-400" },
    { id: 8, text: "", delay: 1400, color: "text-white" },
    { id: 9, text: "const Portfolio = () => {", delay: 1600, color: "text-blue-400" },
    { id: 10, text: "  useEffect(() => {", delay: 1800, color: "text-indigo-400" },
    { id: 11, text: "    optimizePortfolio();", delay: 2000, color: "text-purple-400" },
    { id: 12, text: "  }, []);", delay: 2200, color: "text-indigo-400" },
    { id: 13, text: "  return <Layout>", delay: 2400, color: "text-pink-400" },
    { id: 14, text: "    <Hero />", delay: 2600, color: "text-rose-400" },
    { id: 15, text: "    <About />", delay: 2800, color: "text-rose-400" },
    { id: 16, text: "    <Experience />", delay: 3000, color: "text-rose-400" },
    { id: 17, text: "    <Contact />", delay: 3200, color: "text-rose-400" },
    { id: 18, text: "  </Layout>;", delay: 3400, color: "text-pink-400" },
    { id: 19, text: "};", delay: 3600, color: "text-blue-400" },
  ];
  
  // Text typing animation
  let typingLineIndex = 0;
  let charIndex = 0;
  let typingInterval: number;
  let typewriterText = '';
  let currentLine: string = '';
  let isTyping = false;
  
  // SVG Tech Icons (in addition to Lucide icons)
  const svelteLogo = `<svg viewBox="0 0 98.1 118" xmlns="http://www.w3.org/2000/svg"><path d="m91.8 15.6c-10.9-15.7-32.6-20.3-48.2-10.4l-27.5 17.6c-7.5 4.7-12.7 12.4-14.2 21.1-1.3 7.3-.2 14.8 3.3 21.3-2.4 3.6-4 7.6-4.7 11.8-1.6 8.9.5 18.1 5.7 25.4 11 15.7 32.6 20.3 48.2 10.4l27.5-17.5c7.5-4.7 12.7-12.4 14.2-21.1 1.3-7.3.2-14.8-3.3-21.3 2.4-3.6 4-7.6 4.7-11.8 1.7-9-.4-18.2-5.7-25.5" fill="#ff3e00"/><path d="m40.9 103.9c-8.9 2.3-18.2-1.2-23.4-8.7-3.2-4.4-4.4-9.9-3.5-15.3.2-.9.4-1.7.6-2.6l.5-1.6 1.4 1c3.3 2.4 6.9 4.2 10.8 5.4l1 .3-.1 1c-.1 1.4.3 2.9 1.1 4.1 1.6 2.3 4.4 3.4 7.1 2.7.6-.2 1.2-.4 1.7-.7l27.4-17.5c1.4-.9 2.3-2.2 2.6-3.8s-.1-3.3-1-4.6c-1.6-2.3-4.4-3.3-7.1-2.6-.6.2-1.2.4-1.7.7l-10.5 6.7c-1.7 1.1-3.6 1.9-5.6 2.4-8.9 2.3-18.2-1.2-23.4-8.7-3.1-4.4-4.4-9.9-3.4-15.3.9-5.2 4.1-9.9 8.6-12.7l27.5-17.5c1.7-1.1 3.6-1.9 5.6-2.5 8.9-2.3 18.2 1.2 23.4 8.7 3.2 4.4 4.4 9.9 3.5 15.3-.9 5.2-4.1 9.9-8.6 12.7l-27.5 17.5c-1.7 1.1-3.6 1.9-5.6 2.5" fill="#fff"/></svg>`;
  const nextLogo = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 180 180"><mask height="180" id="mask0" width="180" x="0" y="0" maskUnits="userSpaceOnUse"><circle cx="90" cy="90" fill="#fff" r="90" /></mask><g mask="url(#mask0)"><circle cx="90" cy="90" fill="#000" r="90" /><path d="M149.508 157.52L69.142 54H54v71.97h12.114V69.384l73.885 95.461a90.304 90.304 0 009.509-7.325z" fill="url(#paint0_linear)" /><path fill="#fff" d="M115 54H127V126H115z" /></g><defs><linearGradient gradientUnits="userSpaceOnUse" id="paint0_linear" x1="109" x2="144.5" y1="116.5" y2="160.5"><stop stop-color="#fff" /><stop offset="1" stop-color="#fff" stop-opacity="0" /></linearGradient></defs></svg>`;
  const reactLogo = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="-11.5 -10.23174 23 20.46348"><circle cx="0" cy="0" r="2.05" fill="#61dafb"/><g stroke="#61dafb" stroke-width="1" fill="none"><ellipse rx="11" ry="4.2"/><ellipse rx="11" ry="4.2" transform="rotate(60)"/><ellipse rx="11" ry="4.2" transform="rotate(120)"/></g></svg>`;
  const vscodeIcon = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><path fill="#007acc" d="M2.3 41.3 12 36.1V64L2.3 58.7V41.3zM75.4 39 60.5 58.7 45.6 39H75.4z"/><path fill="#007acc" d="M75.4 61 45.6 61 60.5 41.3 75.4 61z"/><path fill="#007acc" d="M24.1 46.7 32.7 41.3 41.3 46.7 32.7 52 24.1 46.7z"/><path fill="#007acc" d="M75.7 36.1V64L86.2 58.7V41.3L75.7 36.1zM62.9 9.4 48.1 36H34.1L18.2 9.4 35.4 4.6 49.1 21.4 62.9 4.6 80 9.4 62.9 9.4zM43.3 90.6 21.4 78.6 4.6 95.4 27.4 86.4 43.3 69.7V90.6zM56.7 90.6V69.7L72.6 86.4 95.4 95.4 78.6 78.6 56.7 90.6z"/></svg>`;
  const nodejsIcon = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path fill="#539e43" d="M224 508c-6.7 0-13.5-1.8-19.4-5.2l-61.7-36.5c-9.2-5.2-4.7-7-1.7-8 12.3-4.3 14.8-5.2 27.9-12.7 1.4-.8 3.2-.5 4.6.4l47.4 28.1c1.7 1 4.1 1 5.7 0l184.7-106.6c1.7-1 2.8-3 2.8-5V149.3c0-2.1-1.1-4-2.9-5.1L226.8 37.7c-1.7-1-4-1-5.7 0L36.6 144.3c-1.8 1-2.9 3-2.9 5.1v213.1c0 2 1.1 4 2.9 4.9l50.6 29.2c27.5 13.7 44.3-2.4 44.3-18.7V167.5c0-3 2.4-5.3 5.4-5.3h23.4c2.9 0 5.4 2.3 5.4 5.3V378c0 36.6-20 57.6-54.7 57.6-10.7 0-19.1 0-42.5-11.6l-48.4-27.9C8.1 389.2.7 376.3.7 362.4V149.3c0-13.8 7.4-26.8 19.4-33.7L204.6 9c11.7-6.6 27.2-6.6 38.8 0l184.7 106.7c12 6.9 19.4 19.8 19.4 33.7v213.1c0 13.8-7.4 26.7-19.4 33.7L243.4 502.8c-5.9 3.4-12.6 5.2-19.4 5.2zm149.1-210.1c0-39.9-27-50.5-83.7-58-57.4-7.6-63.2-11.5-63.2-24.9 0-11.1 4.9-25.9 47.4-25.9 37.9 0 51.9 8.2 57.7 33.8.5 2.4 2.7 4.2 5.2 4.2h24c1.5 0 2.9-.6 3.9-1.7s1.5-2.6 1.4-4.1c-3.7-44.1-33-64.6-92.2-64.6-52.7 0-84.1 22.2-84.1 59.5 0 40.4 31.3 51.6 81.8 56.6 60.5 5.9 65.2 14.8 65.2 26.7 0 20.6-16.6 29.4-55.5 29.4-48.9 0-59.6-12.3-63.2-36.6-.4-2.6-2.6-4.5-5.3-4.5h-23.9c-3 0-5.3 2.4-5.3 5.3 0 31.1 16.9 68.2 97.8 68.2 58.4-.1 92-23.2 92-63.4z"/></svg>`;
  const typescriptLogo = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 400 400"><path fill="#007acc" d="M0 200V0h400v400H0"/><path fill="#fff" d="M87.7 200.7V217h52v148h36.9V217h52v-16c0-9 0-16.3-.4-16.5 0-.3-31.7-.4-70.2-.4l-70 .3v16.4l-.3-.1zM321.4 184c10.2 2.4 18 7 25 14.3 3.7 4 9.2 11 9.6 12.8 0 .6-17.3 12.3-27.8 18.8-.4.3-2-1.4-3.6-4-5.2-7.4-10.5-10.6-18.8-11.2-12-.8-20 5.5-20 16 0 3.2.6 5 1.8 7.6 2.7 5.5 7.7 8.8 23.2 15.6 28.6 12.3 41 20.4 48.5 32 8.5 13 10.4 33.4 4.7 48.7-6.4 16.7-22 28-44.3 31.7-7 1.2-23 1-30.5-.3-16-3-31.3-11-40.7-21.3-3.7-4-10.8-14.7-10.4-15.4l3.8-2.4 15-8.7 11.3-6.6 2.6 3.5c3.3 5.2 10.7 12.2 15 14.6 13 6.7 30.4 5.8 39-2 3.7-3.4 5.3-7 5.3-12 0-4.6-.7-6.7-3-10.2-3.2-4.4-9.6-8-27.6-16-20.7-8.8-29.5-14.4-37.7-23-4.7-5.2-9-13.3-11-20-1.5-5.8-2-20-.6-25.7 4.3-20 19.4-34 41-38 7-1.4 23.5-.8 30.4 1l-.2.2z"/></svg>`;
  const vueIcon = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 256 221"><path fill="#41B883" d="M204.8 0H256L128 220.8 0 0h97.92L128 51.2 157.44 0h47.36Z"/><path fill="#41B883" d="m0 0 128 220.8L256 0h-51.2L128 132.48 50.56 0H0Z"/><path fill="#35495E" d="M50.56 0 128 133.12 204.8 0h-47.36L128 51.2 97.92 0H50.56Z"/></svg>`;
  const angularIcon = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 186.2 200"><path fill="#DD0031" d="M93.1 0 0 33.2l14.2 123.1L93.1 200l79-43.7 14.1-123.1L93.1 0z"/><path fill="#C3002F" d="M93.1 0v22.2-.1V200l79-43.7 14.1-123.1L93.1 0z"/><path fill="#FFFFFF" d="M93.1 22.1 34.9 152.6h21.7l11.7-29.2h49.4l11.7 29.2h21.7L93.1 22.1zm17 83.3h-34l17-40.9 17 40.9z"/></svg>`;
  
  // Animation elements
  let animationInterval: number;
  let matrixRainInterval: number;
  const icons = [Code, Terminal, Braces, Hash, Github, Linkedin, FileCode, Database, Globe, Server, Cloud, Cpu, Coffee, Laptop];
  let floatingElements = Array(35).fill(0).map((_, i) => ({
    id: i,
    x: Math.random() * 100,
    y: Math.random() * 100,
    size: Math.random() * 20 + 10,
    speed: Math.random() * 0.5 + 0.2,
    direction: Math.random() > 0.5 ? 1 : -1,
    horizontalSpeed: Math.random() * 0.3 + 0.1,
    horizontalDirection: Math.random() > 0.5 ? 1 : -1,
    rotationSpeed: Math.random() * 0.5 + 0.1,
    rotation: Math.random() * 360,
    icon: i % icons.length < icons.length ? icons[i % icons.length] : null,
    svgIcon: i % 14 === 0 ? svelteLogo : 
             i % 14 === 1 ? nextLogo : 
             i % 14 === 2 ? reactLogo :
             i % 14 === 3 ? vscodeIcon :
             i % 14 === 4 ? nodejsIcon :
             i % 14 === 5 ? typescriptLogo :
             i % 14 === 6 ? vueIcon :
             i % 14 === 7 ? angularIcon : null,
    opacity: Math.random() * 0.3 + 0.1,
    color: `rgba(${Math.floor(Math.random() * 100 + 100)}, ${Math.floor(Math.random() * 100 + 100)}, 255, 0.2)`,
    scale: Math.random() * 0.5 + 0.8,
    animationDelay: Math.random() * 5 + 's'
  }));
  
  function typeNextCharacter() {
    if (typingLineIndex >= codeSnippets.length) {
      // Reset to start typing again for continuous effect
      typingLineIndex = 0;
      charIndex = 0;
      typewriterText = '';
      return;
    }
    
    currentLine = codeSnippets[typingLineIndex].text;
    
    if (charIndex < currentLine.length) {
      typewriterText = currentLine.substring(0, charIndex + 1);
      charIndex++;
    } else {
      // Line complete, move to next line
      charIndex = 0;
      typingLineIndex++;
      // Add a new line if not at the end
      if (typingLineIndex < codeSnippets.length) {
        typewriterText = '';
      }
    }
  }
  
  onMount(() => {
    // Start typewriter effect
    isTyping = true;
    typingInterval = setInterval(typeNextCharacter, 50);
    
    // Animate the floating code icons continuously
    animationInterval = setInterval(() => {
      floatingElements = floatingElements.map(element => {
        // Move element vertically
        let newY = element.y + element.speed * element.direction;
        
        // Move element horizontally
        let newX = element.x + element.horizontalSpeed * element.horizontalDirection;
        
        // Rotate element
        let newRotation = (element.rotation + element.rotationSpeed) % 360;
        
        // Bounce if reaching edges (vertical)
        if (newY <= 0 || newY >= 100) {
          element.direction *= -1;
          newY = element.y + element.speed * element.direction;
        }
        
        // Bounce if reaching edges (horizontal)
        if (newX <= 0 || newX >= 100) {
          element.horizontalDirection *= -1;
          newX = element.x + element.horizontalSpeed * element.horizontalDirection;
        }
        
        return {
          ...element,
          y: newY,
          x: newX,
          rotation: newRotation
        };
      });
    }, 50);
    
    // Add typing animation for code elements
    const codeElements = codeContainerRef?.querySelectorAll('.code-line') || [];
    codeElements.forEach((element) => {
      setTimeout(() => {
        element.classList.add('active');
      }, parseInt(element.getAttribute('data-delay') || '0'));
    });
    
    // Reset code animation periodically for continuous effect
    setInterval(() => {
      codeElements.forEach((element, index) => {
        element.classList.remove('active');
        setTimeout(() => {
          element.classList.add('active');
        }, parseInt(element.getAttribute('data-delay') || '0'));
      });
    }, 15000); // Reset every 15 seconds
    
    // Make the matrix rain effect continuous
    matrixRainInterval = setInterval(() => {
      const matrixBg = document.querySelector('.code-matrix-background');
      if (matrixBg) {
        matrixBg.classList.remove('matrix-reanimation');
        void (matrixBg as HTMLElement).offsetWidth; // Trigger reflow with proper type casting
        matrixBg.classList.add('matrix-reanimation');
      }
    }, 30000); // Reset matrix rain animation every 30 seconds
  });
  
  onDestroy(() => {
    if (animationInterval) clearInterval(animationInterval);
    if (typingInterval) clearInterval(typingInterval);
    if (matrixRainInterval) clearInterval(matrixRainInterval);
  });
</script>

<section 
  bind:this={heroElement}
  class="relative overflow-hidden py-24 px-4 sm:px-6 lg:px-8"
>
  <!-- Matrix-style code rain background -->
  <div class="absolute inset-0 code-matrix-background opacity-10 pointer-events-none matrix-reanimation"></div>

  <!-- Grid overlay -->
  <div class="absolute inset-0 opacity-5" style="background-image: url('data:image/svg+xml,%3csvg xmlns=\'http://www.w3.org/2000/svg\' viewBox=\'0 0 32 32\' width=\'32\' height=\'32\' fill=\'none\' stroke=\'rgb(255 255 255 / 0.05)\'%3e%3cpath d=\'M0 .5H31.5V32\'/%3e%3c/svg%3e'); background-size: 40px 40px;"></div>
  
  <!-- Enhanced grid lines with subtle animation -->
  <div class="absolute inset-0 grid-lines"></div>
  
  <!-- Floating code icons -->
  <div class="absolute inset-0 overflow-hidden pointer-events-none">
    {#each floatingElements as element (element.id)}
      <div 
        class="absolute transform transition-all duration-[5000ms] ease-in-out animate-float"
        style="left: {element.x}%; top: {element.y}%; opacity: {element.opacity}; transform: rotate({element.rotation}deg) scale({element.scale}); animation-delay: {element.animationDelay};"
      >
        {#if element.icon}
          <svelte:component 
            this={element.icon} 
            size={element.size} 
            class="text-tech-icon"
          />
        {:else if element.svgIcon}
          <div style="width: {element.size}px; height: {element.size}px;" class="tech-svg-icon">
            {@html element.svgIcon}
          </div>
        {/if}
      </div>
    {/each}
  </div>
  
  <!-- Particle effect background -->
  <div class="absolute inset-0 particles-container pointer-events-none"></div>
  
  <!-- Active typewriter code display -->
  <div class="absolute left-4 top-1/4 max-w-xs sm:max-w-sm md:max-w-md pointer-events-none hidden lg:block">
    <div class="typewriter">
      {#if isTyping}
        <span class={codeSnippets[typingLineIndex]?.color || 'text-blue-300'}>
          {typewriterText}<span class="typing-cursor">|</span>
        </span>
      {/if}
    </div>
  </div>
  
  <!-- Code background -->
  <div bind:this={codeContainerRef} class="absolute right-0 top-1/4 max-w-xs sm:max-w-sm md:max-w-md pointer-events-none hidden md:block opacity-10 font-mono text-xs overflow-hidden pr-4">
    {#each codeSnippets as line}
      <div class="code-line opacity-0" data-delay={line.delay}>
        <span class={line.color}>{line.text}</span>
      </div>
    {/each}
  </div>
  
  <div class="absolute top-0 left-0 right-0 h-px bg-gradient-to-r from-transparent via-indigo-500 to-transparent animate-pulse-slow"></div>
  
  <div class="relative max-w-5xl mx-auto text-center">
    <div class="mb-8 inline-flex items-center justify-center rounded-full bg-indigo-500/10 px-3 py-1 text-sm font-medium text-indigo-400 ring-1 ring-inset ring-indigo-500/20 hero-anim animate-pulse-subtle hover:scale-105 transition-transform">
      <Sparkles size={16} class="mr-1 animate-sparkle" />
      <span>{badgeText}</span>
    </div>
    
    <h1 class="hero-anim text-4xl sm:text-6xl font-bold mb-6 bg-clip-text text-transparent bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 hero-title animate-title-gradient">
      {title}
    </h1>
    
    <p class="hero-anim max-w-2xl mx-auto text-lg text-slate-300 mb-10 hero-subtitle animate-fade-up">
      {subtitle}
    </p>
    
    <div class="hero-anim flex flex-wrap justify-center gap-4">
      <a href={primaryButtonLink} class="inline-flex items-center gap-2 px-6 py-3 rounded-lg bg-indigo-600 hover:bg-indigo-700 text-white font-medium transition-colors hero-button relative overflow-hidden group shine-effect">
        <span class="relative z-10">{primaryButtonText}</span>
        <span class="absolute inset-0 bg-gradient-to-r from-purple-600 to-indigo-600 opacity-0 group-hover:opacity-100 transition-opacity"></span>
      </a>
      
      <a href={secondaryButtonLink} class="inline-flex items-center gap-2 px-6 py-3 rounded-lg bg-slate-700 hover:bg-slate-600 text-white font-medium transition-colors hero-button relative overflow-hidden group shine-effect">
        <span class="relative z-10">{secondaryButtonText}</span>
        <span class="absolute inset-0 bg-gradient-to-r from-slate-600 to-slate-500 opacity-0 group-hover:opacity-100 transition-opacity"></span>
      </a>
    </div>
  </div>
  
  <!-- Enhanced animated background gradients - made fully continuous -->
  <div class="absolute -top-40 -right-40 w-80 h-80 bg-indigo-600 rounded-full opacity-30 blur-3xl animate-blob animation-infinite glow"></div>
  <div class="absolute -bottom-40 -left-40 w-80 h-80 bg-purple-600 rounded-full opacity-30 blur-3xl animate-blob animation-delay-2000 animation-infinite glow"></div>
  <div class="absolute top-1/2 left-1/4 w-64 h-64 bg-blue-600 rounded-full opacity-20 blur-3xl animate-blob animation-delay-4000 animation-infinite glow"></div>
  <div class="absolute bottom-1/4 right-1/3 w-56 h-56 bg-pink-600 rounded-full opacity-15 blur-3xl animate-blob animation-delay-6000 animation-infinite glow"></div>
</section>

<style>
  @keyframes blob {
    0% {
      transform: translate(0, 0) scale(1);
    }
    33% {
      transform: translate(30px, -30px) scale(1.2);
    }
    66% {
      transform: translate(-20px, 20px) scale(0.8);
    }
    100% {
      transform: translate(0, 0) scale(1);
    }
  }
  
  .animate-blob {
    animation: blob 10s infinite alternate;
  }
  
  .animation-infinite {
    animation-iteration-count: infinite;
  }
  
  .animation-delay-2000 {
    animation-delay: 2s;
  }
  
  .animation-delay-4000 {
    animation-delay: 4s;
  }
  
  .animation-delay-6000 {
    animation-delay: 6s;
  }

  @keyframes float {
    0% {
      transform: translateY(0) translateX(0) rotate(0) scale(1);
    }
    25% {
      transform: translateY(-10px) translateX(5px) rotate(5deg) scale(1.05);
    }
    50% {
      transform: translateY(0) translateX(10px) rotate(10deg) scale(1);
    }
    75% {
      transform: translateY(10px) translateX(5px) rotate(5deg) scale(0.95);
    }
    100% {
      transform: translateY(0) translateX(0) rotate(0) scale(1);
    }
  }

  .animate-float {
    animation: float 15s ease-in-out infinite;
  }
  
  .tech-svg-icon {
    filter: drop-shadow(0 0 5px rgba(99, 102, 241, 0.5));
    transition: filter 0.3s ease;
  }
  
  .text-tech-icon {
    filter: drop-shadow(0 0 3px rgba(99, 102, 241, 0.5));
    color: rgba(128, 140, 255, 0.6);
    transition: all 0.3s ease;
  }
  
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
  
  @keyframes pulse-slow {
    0%, 100% {
      opacity: 0.3;
    }
    50% {
      opacity: 0.7;
    }
  }
  
  .animate-pulse-slow {
    animation: pulse-slow 4s infinite;
  }
  
  /* Matrix code rain effect */
  .code-matrix-background {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(
      45deg,
      rgba(15, 23, 42, 0.2),
      rgba(46, 16, 101, 0.2)
    );
    mask-image: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" width="400" height="400" viewBox="0 0 400 400"><text x="10" y="20" font-family="monospace" font-size="20" fill="white">01011001</text><text x="50" y="40" font-family="monospace" font-size="20" fill="white">10100101</text><text x="150" y="60" font-family="monospace" font-size="20" fill="white">01001010</text><text x="100" y="80" font-family="monospace" font-size="20" fill="white">10110010</text><text x="200" y="100" font-family="monospace" font-size="20" fill="white">01010110</text><text x="250" y="120" font-family="monospace" font-size="20" fill="white">01001100</text><text x="300" y="140" font-family="monospace" font-size="20" fill="white">10101001</text><text x="350" y="160" font-family="monospace" font-size="20" fill="white">10010110</text><text x="100" y="180" font-family="monospace" font-size="20" fill="white">01011001</text><text x="220" y="200" font-family="monospace" font-size="20" fill="white">10101001</text><text x="10" y="220" font-family="monospace" font-size="20" fill="white">01001010</text><text x="300" y="240" font-family="monospace" font-size="20" fill="white">10010110</text><text x="150" y="260" font-family="monospace" font-size="20" fill="white">01010110</text><text x="50" y="280" font-family="monospace" font-size="20" fill="white">10110010</text><text x="250" y="300" font-family="monospace" font-size="20" fill="white">10010110</text><text x="200" y="320" font-family="monospace" font-size="20" fill="white">01011001</text><text x="180" y="340" font-family="monospace" font-size="20" fill="white">10101011</text><text x="320" y="360" font-family="monospace" font-size="20" fill="white">01001010</text><text x="120" y="380" font-family="monospace" font-size="20" fill="white">10101001</text></svg>');
    mask-size: 400px 400px;
  }
  
  .matrix-reanimation {
    animation: matrix-rain 30s linear infinite;
  }
  
  @keyframes matrix-rain {
    0% {
      mask-position: 0 0;
    }
    100% {
      mask-position: 400px 400px;
    }
  }
  
  /* Typing cursor animation */
  .typewriter {
    font-family: monospace;
    font-size: 0.875rem;
    background-color: rgba(15, 23, 42, 0.6);
    padding: 1rem;
    border-radius: 0.5rem;
    width: fit-content;
    max-width: 100%;
    white-space: nowrap;
    position: relative;
    overflow: hidden;
    border-left: 3px solid rgba(99, 102, 241, 0.5);
  }
  
  .typing-cursor {
    display: inline-block;
    animation: blink 0.7s infinite;
  }
  
  @keyframes blink {
    0%, 100% {
      opacity: 1;
    }
    50% {
      opacity: 0;
    }
  }
  
  /* Code typing animation */
  .code-line {
    transition: opacity 0.5s ease, transform 0.5s ease;
    transform: translateX(20px);
  }
  
  .code-line.active {
    opacity: 1;
    transform: translateX(0);
  }
  
  /* Hero animations */
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }
  
  .hero-title {
    animation: fadeIn 0.8s ease-out forwards;
  }
  
  .hero-subtitle {
    animation: fadeIn 0.8s ease-out 0.3s forwards;
    opacity: 0;
  }
  
  .hero-button {
    position: relative;
    overflow: hidden;
  }
  
  .hero-button::after {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
    transition: 0.5s;
  }
  
  .hero-button:hover::after {
    left: 100%;
  }
  
  /* NEW ENHANCED ANIMATIONS */
  
  /* Title gradient animation */
  @keyframes title-gradient {
    0% {
      background-position: 0% 50%;
    }
    50% {
      background-position: 100% 50%;
    }
    100% {
      background-position: 0% 50%;
    }
  }
  
  .animate-title-gradient {
    background-size: 200% auto;
    animation: title-gradient 5s ease infinite;
  }
  
  /* Fade up animation */
  @keyframes fade-up {
    0% {
      opacity: 0;
      transform: translateY(20px);
    }
    100% {
      opacity: 1;
      transform: translateY(0);
    }
  }
  
  .animate-fade-up {
    animation: fade-up 1s ease-out forwards;
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
  
  /* Particles container */
  .particles-container {
    background-image: radial-gradient(circle, rgba(99, 102, 241, 0.05) 1px, transparent 1px);
    background-size: 30px 30px;
    animation: particles-float 20s linear infinite;
  }
  
  @keyframes particles-float {
    0% {
      background-position: 0 0;
    }
    100% {
      background-position: 30px 30px;
    }
  }

  /* Shine effect for buttons */
  @keyframes shine {
    0% {
      background-position: -200% center;
    }
    100% {
      background-position: 200% center;
    }
  }

  .shine-effect {
    position: relative;
    overflow: hidden;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
    background-size: 200% 100%;
    animation: shine 3s infinite linear;
  }
</style> 