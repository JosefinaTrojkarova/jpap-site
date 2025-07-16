````markdown
# GitHub Copilot – Project Guidance

## 📦 Project Setup
- This is a **Svelte 5 + pnpm** project.
- Scaffolded via:  
    ```bash
    pnpm create svelte@latest
    pnpm install
    pnpm dev
    ```
- **Use TypeScript only** for all source files.

## ⚡ Reactivity & State

* Use **runes** (`$state`, `$derived`, `$effect`) for in-component reactivity.
* Svelte runes/functions (like `$state`, `$derived`, `$effect`) **do not need to be imported**—they are available globally in Svelte files.

    ```svelte
    let count = $state(0);
    $: doubled = count * 2;
    ```
* Use `$derived` only when combining reactive values—avoid `$effect` when a derived rune suffices.

## 🗂️ Stores & Shared State

* When sharing state across components or modules, prefer Svelte’s built-in stores (`writable`, `readable`, `derived`).

    ```ts
    import { writable } from 'svelte/store';
    export const count = writable(0);
    ```
* Access stores in components using `$count`.
* For advanced shareable contexts, use `setContext`/`getContext` with stores.

## 🔄 Store Best Practices

* Keep stores **focused**—one store = one responsibility.
* Use `derived()` for computations off multiple stores.
* Clean up **manual** subscriptions when necessary.

## 🛠️ CLI & Tooling

* Use the `sv` CLI via pnpm:

    ```bash
    pnpx sv <command> # e.g., sv create, sv add, sv check, sv migrate
    ```

## 🧷 Props

* In Svelte 5, **all component inputs (props)** are declared using the `$props()` rune via destructuring.
  
    ```svelte
    <script lang="ts">
      let { answer, count = 0 }: { answer: string; count?: number } = $props();
    </script>
    ```

* **Fallback/default values** work via destructuring defaults:
  
    ```svelte
    let { size = 42 } = $props();
    ```

* **Renaming props** (e.g. reserved words like `class`):

    ```svelte
    let { class: className = '' } = $props();
    ```

  This is recommended over the old `export { x as y }` approach.

* **Rest props**: capture extra props via rest syntax:

    ```svelte
    let { foo, bar, ...rest } = $props();
    <div {...rest}>{foo} {bar}</div>
    ```

* **Reactivity of props**: incoming props stay reactive (live updates) *only* if the parent passes a `$state(...)` variable. If reactivity is needed inside, re-wrap or clone them.
````
