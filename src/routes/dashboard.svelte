<script>
    import Icon  from "@iconify/svelte";
    const burgerName = [
        { name: 'Mes chantiers', link: '/' },
        { name: 'Tableau de bord', link: '/dashboard' },
        { name: 'Aide', link: '/contact-us' },
        { name: 'Paramètres', link: '/settings' },
        { name: 'Déconnexion', link: '/logout' }
      ];
    let stats = $state([
    { count: 12, label: 'Terminés', icon: '✅' },
    { count: 8, label: 'En cours', icon: '🔄' },
    { count: 5, label: 'À faire', icon: '📋' }
  ]);

  let progress = $state(65);  

  let menuOpen = $state(false);

  const showResponsiveMenu = () => {
    menuOpen = !menuOpen;
  };

</script>

<header>
    
    <button class="dashboard_burger--icon" on:click|preventDefault={showResponsiveMenu}>
      <span><Icon icon="charm:menu-hamburger" width="16" height="16"  style="color: #fff" /></span>
    </button>
    {#if menuOpen}
    <nav class="dashboard_burger--list">
        <ul>
            {#each burgerName as item}
        <li><a href={item.link}>{item.name}</a></li>
        {/each}
      </ul>
    </nav>

    {:else}
    <h1 class="dashboard_title">Construction immeuble A</h1>
    <h2 class="dashboard_subtitle">Jean Dupont</h2>
    {/if}
</header>
{#if !menuOpen}
<main>
    <div>
        <label for="progress-bar">Progression du chantier:</label>
        <progress id="progress-bar" value={progress} max="100">{progress} %</progress>
    </div>
    <div class="dashboard_stats--grid">
        {#each stats as stat}
        <div class="dashboard_stats--element">
            <span class="dashboard_stats--icon">{stat.icon}</span>
            <span class="dashboard_stats--count">{stat.count}</span>
            <span class="dashboard_stats--label">{stat.label}</span>
        </div>
        {/each}
    </div>

    <button class="dashboard_scan">SCANNER UN ELEMENT</button>
</main>
{/if}

<style>
    /* Header */
    header {
        background-color: #FF6B00;
        padding: 1rem;
        color: white;
        position: relative;
    }

    .dashboard_burger--icon {
        background: none;
        border: none;
        cursor: pointer;
        padding: 0.5rem;
    }

    .dashboard_title {
        font-size: 1.5rem;
        font-weight: bold;
        margin: 0.5rem 0 0.25rem 0;
    }

    .dashboard_subtitle {
        font-size: 1rem;
        font-weight: normal;
        opacity: 0.9;
    }

    /* Menu burger */
    .dashboard_burger--list {
        position: fixed;
        top: 0;
        left: 0;
        width: 80%;
        max-width: 300px;
        height: 100vh;
        background-color: white;
        box-shadow: 2px 0 8px rgba(0,0,0,0.2);
        z-index: 1000;
        padding: 2rem 0;
    }

    .dashboard_burger--list li {
        border-bottom: 1px solid #eee;
    }

    .dashboard_burger--list a {
        display: block;
        padding: 1rem 1.5rem;
        color: #212121;
        text-decoration: none;
    }

    .dashboard_burger--list a:hover {
        background-color: #f5f5f5;
        color: #FF6B00;
    }

    /* Main */
    main {
        padding: 2rem 1rem;
        background-color: #F5F5F5;
    }

    /* Barre de progression */
    label {
        display: block;
        font-weight: bold;
        margin-bottom: 0.5rem;
        color: #212121;
    }

    progress {
        width: 100%;
        height: 30px;
        margin-bottom: 2rem;
    }

    /* Stats - Grid 3 colonnes */
    .dashboard_stats--grid {
         display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 1rem;
        margin-bottom: 2rem;
    }

    .dashboard_stats--element {
        background: white;
        padding: 1.5rem;
        border-radius: 12px;
        box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
    }

    .dashboard_stats--icon {
        font-size: 2rem;
        margin-bottom: 0.5rem;
    }

    .dashboard_stats--count {
        font-size: 2rem;
        font-weight: bold;
        color: #212121;
        margin-bottom: 0.25rem;
    }

    .dashboard_stats--label {
        font-size: 0.9rem;
        color: #666;
    }

    /* Bouton Scanner */
    .dashboard_scan {
        width: 100%;
        max-width: 400px;
        min-height: 80px;
        background-color: #FF6B00;
        color: white;
        font-size: 1.3rem;
        font-weight: bold;
        border: none;
        border-radius: 12px;
        cursor: pointer;
        margin: 0 auto;
        display: block;
        box-shadow: 0 4px 12px rgba(255, 107, 0, 0.3);
    }

    .dashboard_scan:hover {
        background-color: #e66000;
        transform: translateY(-2px);
        box-shadow: 0 6px 16px rgba(255, 107, 0, 0.4);
    }

    .dashboard_scan:active {
        transform: translateY(0);
    }

    /* Responsive pour mobile */
    @media (max-width: 768px) {
        .dashboard_stats--grid {
        grid-template-columns: 1fr;
    }
        .dashboard_stats--element {
            padding: 1rem;
        }
    }

</style>