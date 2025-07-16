<script lang="ts">
    import Button from "./Button.svelte";
    import { ArrowUpRight } from "@lucide/svelte";
</script>

<nav>
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
        display: flex;
        justify-content: space-between;
        align-items: center;
        
        .logo {
            width: 2rem;
            height: 2rem;
            background: var(--accent-color);
            border-radius: 50%;
        }

        ul {
            display: flex;
            list-style: none;
            gap: 1rem;

            a {
                text-decoration: none;
                color: var(--text-color);
                font-weight: 500;
            }
        }
    }
</style>