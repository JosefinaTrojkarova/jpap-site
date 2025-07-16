<script lang="ts">
    import Button from "./Button.svelte";
    import { ArrowRight } from "@lucide/svelte";
</script>

<section class="hero">
    <p class="callout">
        <span class="circle"></span>
        <span class="text">Přijímáme nové klienty</span>
    </p>
    <h1>Tvoříme weby, které řeší problémy a přináší výsledky</h1>

    <p class="description">
        Čeští podnikatelé mají weby jen na okrasu (často ani to ne). My měníme hru. Proměníme Váš web, vyfintíme branding a zařídíme reklamy.
    </p>
    <form method="POST" class="audit">
        <input type="url" name="url" id="url" placeholder="Odkaz na Váš web" required>
        <Button type="submit" icon={ArrowRight}>Získat audit zdarma</Button>
    </form>
    <img src="/full-logo.svg" alt="Logo jpap" class="logo">
</section>

<style>
    .hero {
        position: relative;
        box-sizing: border-box;
        display: flex;
        flex-direction: column;
        padding-top: 8rem;
        padding-bottom: 2rem;
        gap: 1rem;
        height: 100vh;

        .callout {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            color: var(--text-color);

            .circle {
                width: 1rem;
                height: 1rem;
                background-color: greenyellow;
                box-shadow: 0 0 10px 5px rgba(172, 255, 47, 0.3);
                border-radius: 50%;
            }
        }

        h1 {
            font-family: 'Clash Display', sans-serif;
            font-size: 5rem;
        }

        .description {
            margin-top: auto;
            width: 450px;
        }

        form {
            display: flex;
            align-items: center;
            padding: .5rem;
            background: white;
            border-radius: 1rem;
            width: 100%;
            max-width: 600px;

            input {
                flex-grow: 1;
                padding: 0.75rem 1rem;
                border: 1px solid var(--border-color);
                border-radius: 0.5rem;
                font-size: 1rem;
                font-family: inherit;

                &:focus {
                    outline: none;
                }
            }

            &:has(input:focus) {
                outline: auto 2px var(--accent-color);
            }
        }

        .logo {
            position: absolute;
            width: 30rem;
            right: 0;
            bottom: 2rem;
        }
    }
</style>