<script lang="ts">
	import type { Component, Snippet } from 'svelte';

	interface Props {
		icon?: Component;
		children?: Snippet;
		[key: string]: any;
	}

	let { icon, children, ...rest }: Props = $props();
</script>

<button {...rest}>
    {@render children?.()}
	{#if icon}
		{@const IconComponent = icon}
		<IconComponent style="width: 1.5rem; height: 1.5rem;" />
	{/if}
</button>

<style>
    button {
        display: inline-flex;
        align-items: center;
        gap: 0.5rem;
        padding: .75rem 1.5rem;
        background: var(--accent-color);
        color: white;
        border: none;
        border-radius: 0.5rem;
        font-weight: 500;
        font-family: inherit;
        font-size: 1rem;
        cursor: pointer;
        transition: all 0.2s ease;

        &:hover {
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        }

        &:active {
            transform: translateY(0);
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
        }

        &:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        &:disabled:hover {
            transform: none;
            box-shadow: none;
        }

        &:disabled:active {
            transform: none;
            box-shadow: none;
        }
    }
</style>
