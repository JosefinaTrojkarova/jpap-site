<script lang="ts">
    import Button from "./Button.svelte";
    import { ArrowUpRight } from "@lucide/svelte";

    let scrollY = $state(0);
    let isScrolled = $derived(scrollY > 50);
</script>

<svelte:window bind:scrollY />

<nav class:scrolled={isScrolled}>
    <a href="/" class="logo" aria-label="Domů"></a>
    <ul>
        <li><a href="/about">O nás</a></li>
        <li><a href="/services">Služby</a></li>
        <li><a href="/contact">Ceník</a></li>
    </ul>
    <Button icon={ArrowUpRight} type="button" aria-label="Kontaktujte nás">
        Kontaktujte nás
    </Button>
</nav>

<style>
    nav {
        z-index: 1000;
        box-sizing: border-box;
        top: 0;
        left: 50%;
        transform: translateX(-50%);
        position: fixed;
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: min(calc(100vw), calc(1440px + 2rem));
        padding: 2rem;
        transition: padding .4s cubic-bezier(.625,.05,0,1);
        
        &.scrolled {
            padding: 1rem;
        }

        .logo {
            width: 2rem;
            height: 2rem;
            background: var(--accent-color);
            border-radius: 50%;
        }

        ul {
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            list-style: none;

            a {
                padding: 0.5rem 1rem;
                text-decoration: none;
                color: var(--text-color);
                font-weight: 500;
            }
        }
    }
</style>