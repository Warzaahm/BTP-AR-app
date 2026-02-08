<script>
    import Icon from "@iconify/svelte";
    const burgerName = [
        { name: 'Mes chantiers', link: '/' },
        { name: 'Tableau de bord', link: '/dashboard' },
        { name: 'Aide', link: '/contact-us' },
        { name: 'Paramètres', link: '/settings' },
        { name: 'Déconnexion', link: '/logout' }
      ];
    
    let stepsList = $state([
        { id: 1, label: 'Préparation du chantier', description: 'Installation du chantier, sécurité, etc.', statut: 'terminé' },
        { id: 2, label: 'Fondations', description: 'Construction des fondations du bâtiment', statut: 'en cours' },
        { id: 3, label: 'Élévation des murs', description: 'Construction des murs extérieurs', statut: 'à faire' },
        { id: 4, label: 'Toiture', description: 'Installation de la toiture', statut: 'à faire' },
        { id: 5, label: 'Finitions', description: 'Travaux de finition intérieure et extérieure', statut: 'à faire' }
    ]);

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
    {#each  as }
    <button></button>  
    {/each}
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
    main {
        padding: 2rem 1rem;
        background-color: #F5F5F5;
    }
</style>