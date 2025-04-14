<script lang="ts">
  // Empty script block - this component is just for styles
</script>

<div class="hidden">
  <!-- This is a dummy container to hold styles -->
</div>

<style>
  /* Animations */
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
  
  :global(.animate-blob) {
    animation: blob 10s infinite alternate;
  }
  
  :global(.animation-delay-2000) {
    animation-delay: 2s;
  }
  
  /* Backgrounds */
  :global(.bg-gradient-primary) {
    background: linear-gradient(to bottom, #0f172a, #1e293b, #0f172a);
  }
  
  :global(.bg-card) {
    background-color: rgba(51, 65, 85, 0.5);
    backdrop-filter: blur(8px);
    border: 1px solid rgba(71, 85, 105, 1);
  }
  
  :global(.bg-card-hover) {
    transition: all 0.3s ease;
  }
  :global(.bg-card-hover:hover) {
    border-color: rgba(99, 102, 241, 1);
    box-shadow: 0 10px 15px -3px rgba(99, 102, 241, 0.2);
  }
  
  /* Text Gradients */
  :global(.text-gradient-primary) {
    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;
    background-image: linear-gradient(to right, rgba(99, 102, 241, 1), rgba(168, 85, 247, 1), rgba(236, 72, 153, 1));
  }
  
  :global(.text-gradient-secondary) {
    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;
    background-image: linear-gradient(to right, rgba(99, 102, 241, 1), rgba(34, 211, 238, 1));
  }
  
  /* Buttons */
  :global(.btn) {
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.75rem 1.5rem;
    border-radius: 0.5rem;
    font-weight: 500;
    transition: background-color 0.3s ease;
  }
  
  :global(.btn-primary) {
    background-color: rgba(99, 102, 241, 1);
    color: white;
  }
  :global(.btn-primary:hover) {
    background-color: rgba(79, 70, 229, 1);
  }
  
  :global(.btn-secondary) {
    background-color: rgba(51, 65, 85, 1);
    color: white;
  }
  :global(.btn-secondary:hover) {
    background-color: rgba(71, 85, 105, 1);
  }
</style> 