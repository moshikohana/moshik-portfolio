<script lang="ts">
  import Hero from './templates/Hero.svelte';
  import FeatureCards from './templates/FeatureCards.svelte';
  import UIStyles from './templates/UIStyles.svelte';
  import { Code, Briefcase, GraduationCap, Star, Award, Mail, Phone, Github, Linkedin, Terminal, Database, Rocket } from 'lucide-svelte';
  import type { Feature } from './templates/FeatureCards.svelte';
  
  // Skills section
  const skills: Feature[] = [
    {
      icon: Code,
      iconColor: 'text-indigo-400',
      iconBgColor: 'bg-indigo-500/20',
      title: 'Programming Languages',
      description: 'Java, Python, C, C#, JavaScript, TypeScript, SQL, HTML, PHP'
    },
    {
      icon: Briefcase,
      iconColor: 'text-purple-400',
      iconBgColor: 'bg-purple-500/20',
      title: 'Frameworks & Libraries',
      description: 'Node.js, Angular, Next.js, React'
    },
    {
      icon: GraduationCap,
      iconColor: 'text-pink-400',
      iconBgColor: 'bg-pink-500/20',
      title: 'Databases',
      description: 'SQL Server, MongoDB'
    }
  ];

  // Experience timeline data
  const experiences = [
    {
      title: "Student Intern",
      company: "Prime Minister's Office",
      department: "Department of Interior, Planning, and Development",
      period: "2023 - Present",
      responsibilities: [
        "Conduct policy research and background work for government resolutions",
        "Build relationships with government ministries and local authorities",
        "Support planning and development programs",
        "Assist in managing projects, including data collection and analysis",
        "Create daily reports on department collaboration",
        "Oversee the 'Horror Archive' and distribute materials to stakeholders",
        "Formulate public diplomacy tasks"
      ]
    },
    {
      title: "Intern",
      company: "Ministry of National Infrastructure, Geological Survey of Israel",
      period: "2019-2021",
      responsibilities: [
        "Drafted ISO-compliant procedures for computer hardware onboarding",
        "Coordinated inventory management with Government ICT Department",
        "Assisted in transitioning legacy website to government domain",
        "Organized content and maintained the new website before and after launch"
      ]
    }
  ];

  // Education background
  const education = [
    {
      degree: "Bachelor's Degree in Computer Science",
      institution: "The Open University of Israel",
      period: "2022 - Present"
    },
    {
      degree: "Full Stack Web Developer course",
      institution: "John Bryce College",
      period: "2017 - 2018"
    }
  ];
</script>

<!-- Include global styles -->
<UIStyles />

<div class="bg-gradient-primary text-white min-h-screen">
  <!-- Hero Section -->
  <Hero 
    title="Moshik Ohana"
    subtitle="Full Stack Web Developer & Computer Science Student"
    badgeText="Available for New Opportunities"
    primaryButtonText="Contact Me"
    primaryButtonLink="#contact"
    secondaryButtonText="View Resume"
    secondaryButtonLink="#experience"
  />
  
  <!-- About Me Section -->
  <section class="py-16 px-4 sm:px-6 lg:px-8">
    <div class="max-w-3xl mx-auto">
      <h2 class="text-2xl font-bold mb-6 text-gradient-secondary text-center">About Me</h2>
      <div class="bg-card p-6 rounded-xl">
        <p class="text-slate-300 mb-4">
          Highly motivated second-year Computer Science student at the Open University with a proven track
          record of quick learning, excellent interpersonal skills, and the ability to manage multiple tasks
          efficiently.
        </p>
        <p class="text-slate-300">
          Possesses strong adaptability to new environments and demonstrates proactive self-learning capabilities. 
          Completed a Full Stack Web Developer program at John Bryce College.
          Experienced in public diplomacy, security management, website administration, and content creation.
        </p>
      </div>
    </div>
  </section>
  
  <!-- Skills Section -->
  <FeatureCards 
    features={skills}
    title="Skills & Expertise"
  />
  
  <!-- Experience Section -->
  <section id="experience" class="py-16 px-4 sm:px-6 lg:px-8">
    <div class="max-w-3xl mx-auto">
      <h2 class="text-2xl font-bold mb-10 text-gradient-secondary text-center">Professional Experience</h2>
      
      <div class="space-y-12">
        {#each experiences as exp, i}
          <div class="bg-card p-6 rounded-xl relative">
            <!-- Timeline elements -->
            {#if i < experiences.length - 1}
              <div class="absolute left-11 top-[5.5rem] bottom-0 w-0.5 bg-indigo-500/30"></div>
            {/if}
            <div class="absolute left-10 top-10 h-2 w-2 rounded-full bg-indigo-500"></div>
            
            <div class="ml-8">
              <h3 class="font-bold text-xl">{exp.title}</h3>
              <h4 class="text-indigo-300 mb-1">{exp.company}</h4>
              {#if exp.department}
                <p class="text-slate-400 mb-2">{exp.department}</p>
              {/if}
              <p class="text-sm text-slate-400 mb-4">{exp.period}</p>
              
              <ul class="space-y-2">
                {#each exp.responsibilities as resp}
                  <li class="flex">
                    <span class="text-indigo-400 mr-2">•</span>
                    <span class="text-slate-300">{resp}</span>
                  </li>
                {/each}
              </ul>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </section>
  
  <!-- Education Section -->
  <section class="py-16 px-4 sm:px-6 lg:px-8 bg-slate-800/50">
    <div class="max-w-3xl mx-auto">
      <h2 class="text-2xl font-bold mb-10 text-gradient-secondary text-center">Education</h2>
      
      <div class="space-y-6">
        {#each education as edu, i}
          <div class="bg-card p-6 rounded-xl">
            <h3 class="font-bold text-xl">{edu.degree}</h3>
            <h4 class="text-indigo-300 mb-1">{edu.institution}</h4>
            <p class="text-sm text-slate-400">{edu.period}</p>
          </div>
        {/each}
      </div>
    </div>
  </section>
  
  <!-- Military Service Section -->
  <section class="py-16 px-4 sm:px-6 lg:px-8">
    <div class="max-w-3xl mx-auto">
      <h2 class="text-2xl font-bold mb-6 text-gradient-secondary text-center">Military Service</h2>
      <div class="bg-card p-6 rounded-xl">
        <h3 class="font-bold text-xl">Infantry Soldier, Golani Brigade (51st Battalion)</h3>
        <h4 class="text-indigo-300 mb-1">Israel Defense Forces</h4>
        <p class="text-sm text-slate-400 mb-4">2011 – 2014</p>
      </div>
    </div>
  </section>
  
  <!-- Contact Section -->
  <section id="contact" class="py-16 px-4 sm:px-6 lg:px-8 bg-gradient-to-r from-indigo-900/50 to-purple-900/50">
    <div class="max-w-3xl mx-auto text-center">
      <h2 class="text-3xl font-bold mb-8 text-gradient-primary">Contact Me</h2>
      
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4 max-w-xl mx-auto mb-8">
        <a href="mailto:moshikoohana@gmail.com" class="bg-card p-4 rounded-xl flex items-center hover:border-indigo-500 transition-colors">
          <Mail size={24} class="text-indigo-400 mr-3" />
          <span>moshikoohana@gmail.com</span>
        </a>
        
        <a href="tel:+972524243250" class="bg-card p-4 rounded-xl flex items-center hover:border-indigo-500 transition-colors">
          <Phone size={24} class="text-purple-400 mr-3" />
          <span>+972 52 424 3250</span>
        </a>
        
        <a href="https://github.com/moshikohana" class="bg-card p-4 rounded-xl flex items-center hover:border-indigo-500 transition-colors">
          <Github size={24} class="text-pink-400 mr-3" />
          <span>GitHub</span>
        </a>
        
        <a href="https://www.linkedin.com/in/moshiko-ohana-88a6a0171/" class="bg-card p-4 rounded-xl flex items-center hover:border-indigo-500 transition-colors">
          <Linkedin size={24} class="text-cyan-400 mr-3" />
          <span>LinkedIn</span>
        </a>
      </div>
      
      <a href="#" class="btn btn-primary">
        <span>Download Resume</span>
      </a>
    </div>
  </section>
  
  <!-- Footer -->
  <footer class="py-6 px-4 sm:px-6 lg:px-8 bg-slate-900 border-t border-slate-800">
    <div class="max-w-7xl mx-auto text-center text-slate-400 text-sm">
      <p>© {new Date().getFullYear()} Moshik Ohana. All rights reserved.</p>
    </div>
  </footer>
</div> 