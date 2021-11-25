<script></script>

<nav class="navbar">
    <a class="navbar__logo" href="/">
        first-svelte-app
    </a>
    <a href="https://github.com/slaylocal/first-svelte-app" rel="noopener noreffer" target="_blank">
        Github
    </a>
</nav>

<style>
    .navbar {
        color: #fff;
        height: 60px;
        background-color: #222222;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 0 40px;
    }

    .navbar__logo {
        text-decoration: none;
        color: #fff;
        font-size: 20px;
        font-weight: bold;
        transition: color .2s ease-in-out;
    }

    .navbar__logo:hover {
        color: #ccc;
    }
</style>