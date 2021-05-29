<script>
    import { onMount } from "svelte";

    let themes = [
        {"name": "💡 light", "value": "light"},
        {"name": "🌑 dark", "value": "dark"},
        {"name": "🧁 cupcake", "value": "cupcake"},
        {"name": "🐝 bumblebee", "value": "bumblebee"},
        {"name": "💎 emerald", "value": "emerald"},
        {"name": "🏚 corporate", "value": "corporate"},
        {"name": "🌊 synthwave", "value": "synthwave"},
        {"name": "📺 retro", "value": "retro"},
        {"name": "🧬 cyberpunk", "value": "cyberpunk"},
        {"name": "❤ valentine", "value": "valentine"},
        {"name": "🎃 halloween", "value": "halloween"},
        {"name": "🌷 garden", "value": "garden"},
        {"name": "🌲 forest", "value": "forest"},
        {"name": "💧 aqua", "value": "aqua"},
        {"name": "🎧 lofi", "value": "lofi"},
        {"name": "🎨 pastel", "value": "pastel"},
        {"name": "🌈 fantasy", "value": "fantasy"},
        {"name": "🔳 wireframe", "value": "wireframe"},
        {"name": "⚫ black", "value": "black"},
        {"name": "💍 luxury", "value": "luxury"},
        {"name": "🧛‍♂️ dracula", "value": "dracula"},
    ];

    onMount(() => {
        const theme = localStorage.getItem('theme');
        document.body.setAttribute("data-theme", theme);
    });
    function changeTheme(name) {
        document.body.setAttribute("data-theme", name);
        localStorage.setItem('theme', name);
    }
</script>

<div class="dropdown dropdown-end dropdown-hover">
    <div tabindex="0" class="m-1 btn">Theme</div>
    <ul class="shadow menu dropdown-content bg-gray-800 text-white rounded-box w-52 h-96">
        <li class="bg-gray-900">
            <a>↓ Scroll ↓</a>
        </li>
        {#each themes as {name,value}}
        <li on:click={() => changeTheme(value)}>
            <a>{name}</a>
        </li>
       {/each}
    </ul>
</div>

<style>
    ul{ 
        overflow-x: hidden;
        overflow-y: scroll;
    }
    ul::-webkit-scrollbar {
        display: none;
      }
</style>
