<script>
    import '../reset.css'
    import '../app.css';
    import Nav from "$lib/components/Nav.svelte";
    import Button from "$lib/components/Button.svelte";
    import { Mail, Download, ArrowRight } from '@lucide/svelte';
</script>

<Nav />

<main>
    <h1>Button Component Demo</h1>
    
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
        padding: 2rem;
        max-width: 1200px;
        margin: 0 auto;
    }
    
    h1 {
        font-family: 'Clash Display', sans-serif;
        font-size: 2.5rem;
        margin-bottom: 2rem;
        text-align: center;
    }
    
    .button-examples {
        display: flex;
        flex-wrap: wrap;
        gap: 1rem;
        justify-content: center;
    }
</style>