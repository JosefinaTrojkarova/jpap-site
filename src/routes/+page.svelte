<script>
    import '../reset.css'
    import '../app.css';
    import { Nav, Button, Hero, DotMatrix } from '$lib';
    import { Mail, Download, ArrowRight } from '@lucide/svelte';
</script>


<main>
    <Nav />
    <Hero />
    <DotMatrix />
    
    <div class="button-examples">
        <!-- Button without icon -->
        <Button>Simple Button</Button>
        
        <!-- Buttons with different icons -->
        <Button icon={Mail}>Contact Us</Button>
        <Button icon={Download}>Download</Button>
        <Button icon={ArrowRight}>Get Started</Button>
        
        <!-- Button with additional props -->
        <Button icon={Mail} disabled>Disabled Button</Button>
    </div>
</main>

<style>
    main {
        display: flex;
        flex-direction: column;
        padding: 0 2rem;
        max-width: 1440px;
        margin: 0 auto;
        gap: 4rem;
    }
    
    .button-examples {
        display: flex;
        flex-wrap: wrap;
        gap: 1rem;
        justify-content: center;
        margin-bottom: 0rem;
    }
</style>