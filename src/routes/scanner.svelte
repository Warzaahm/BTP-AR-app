<script>
    import Icon  from "@iconify/svelte";
    const burgerName = [
        { name: 'Mes chantiers', link: '/' },
        { name: 'Tableau de bord', link: '/dashboard' },
        { name: 'Aide', link: '/contact-us' },
        { name: 'Paramètres', link: '/settings' },
        { name: 'Déconnexion', link: '/logout' }
      ];
    let scanState = $state("start");
    let hotspotData = $state([
        { id: 1, name: 'Mur porteur R+1',zone: 'Bâtiment A - Zone A', status: 'En cours', x: 25, y: 40  },
        { id: 2, name: 'Poutre IPN 200', zone: 'Bâtiment A - Plancher haut', status: 'À faire', x: 60, y: 25 },
        { id: 3, name: 'Gaine électrique', zone: 'Bâtiment A - Circulation', status: 'Terminé', x: 45, y: 70}
    ]);
    // Stocker les données du hotspot détecté pour les afficher dans l'état "completed"
    let detectedHotspot = $state(null);
    let menuOpen = $state(false);

    const showResponsiveMenu = () => {
        menuOpen = !menuOpen;
    };

    // Passer à l'état "scanning" puis "completed" après un délai simulant le scan
    const switchState = (hotspot) => {
        scanState = "scanning";
        setTimeout(() => {
            // Savoir quel hotspot a été scanné et afficher les résultats dans completed
            detectedHotspot = hotspot;
            scanState = "completed";
        }, 3000);
    };

    const handleSubmitToSteps = () => {
        //Naviguer vers le scanner
        push("/steps");
    };
    const handleSubmitToControls = () => {
        //Naviguer vers le scanner
        push("/controls");
    };
</script>

<header>
    
    <button class="dashboard_burger--icon" on:click|preventDefault={showResponsiveMenu}>
      <span><Icon icon="charm:menu-hamburger" width="16" height="16"  style="color: #fff" /></span>
    </button>
    {#if menuOpen}
    <nav class="dashboard_burger--list">
        <ul class="dashboard_burger--list-ul">
            {#each burgerName as item}
        <li class="dashboard_burger--list-li"><a href={item.link}>{item.name}</a></li>
        {/each}
      </ul>
    </nav>

    {:else}
    <h1 class="dashboard_title">Scanner un élément</h1>
    {/if}

</header>
{#if !menuOpen}
    {#if scanState === "start"}
        <main class="scanner_start--main">
            <img src="/images/chantier.jpg" alt="chantier">

            {#each hotspotData as hotspot}
            <div class="scanner_start--element" on:click={() => switchState(hotspot)} style="left: {hotspot.x}%; top: {hotspot.y}%">
                <span class="scanner_start--icon"><Icon icon="ri:map-pin-fill" width="24" height="24"  style="color: #e21e09" /></span>
                <p class="scanner_start--name">{hotspot.name}</p>
            </div>
            {/each}
        </main>

        <footer class="scanner_start--footer">
            <p class="scanner_start--footer-text">Placez votre appareil devant l'élément à scanner </p>
        </footer>

    {:else if scanState === "scanning"}
        <main class="scanner_scanning--main">
            <img src="/images/chantier.jpg" alt="chantier">

            <div class="scanner_scanning--overlay">
                <span class="scanner_scanning--charge"></span>
                <p class="scanner_scanning--text">Analyse en cours...</p>
            </div>
        </main>

    {:else if scanState === "completed"}
        <main class="scanner_completed--main">
            <img src="/images/chantier.jpg" alt="chantier" on:click={() => scanState = "start"}>

            <div class="scanner_completed--overlay">
                <div class="scanner_completed--hotspot">
                <h2 class="scanner_completed--hotspot-title">{detectedHotspot.name}</h2>
                <p>{detectedHotspot.zone}</p>
            </div>
            <div class="scanner_completed--status">
                <p class="scanner_completed--status-text">Statut: {detectedHotspot.status} </p>
            </div>
            <div class="scanner_completed--actions">
                <button class="scanner_completed--button" on:click={handleSubmitToSteps}>Voir les étapes</button>
            </div>
            <div class="scanner_completed--actions">
                <button class="scanner_completed--button" on:click={handleSubmitToControls}>Voir les contrôles</button>
            </div>
            </div>
        </main>

        <footer class="scanner_completed--footer">
            <p class="scanner_completed--footer-text">Touchez l'image pour scanner un autre élément</p>
        </footer>
    {/if}
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

    /* ETAT START */
    .scanner_start--main {
        position: relative;
        width: 100%;
        height: calc(100vh - 150px);
    }
    .scanner_start--main img {
        width: 100%;
        height: 100%;
        object-fit: contain; 
    }

    /* Hotspots cliquables */

    /* Gestion Animation */
     @keyframes pulse {
        0%, 100% { transform: scale(1); } /* Commence et termine à la taille normale */
        50% { transform: scale(1.2); } /* Agrandit à 120% au milieu de l'animation */
    }
    .scanner_start--element {
        position: absolute;
        cursor: pointer;
        display: flex;
        animation: pulse 2s infinite; /* Animation pulsante */
    }


    .scanner_start--name {
        background: rgba(255, 107, 0, 0.9);
        color: white;
        padding: 0.3rem 0.5rem;
        border-radius: 5px;
        font-size: 0.8rem;
        font-weight: bold;
        margin-top: 0.25rem;
    }

    .scanner_start--footer {
        background: #212121;
        color: white;
        text-align: center;
        padding: 1rem;
    }

    .scanner_start--footer-text {
        font-size: 0.8rem;
    }

   /* ÉTAT SCANNING */
    .scanner_scanning--main {
        position: relative;
        width: 100%;
        height: 100vh;
    }

    .scanner_scanning--main img {
        width: 100%;
        height: 100%;
        object-fit: contain;
        filter: brightness(0.5); /* Assombrit l'image */
    }
    .scanner_scanning--overlay {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.7); /* Fond noir à 70% */
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 1rem;
    }

    /* Gestion Animation */
    @keyframes charge {
        to { transform: rotate(360deg); } /* Rotation complète de 360 degrés */
    }
    
    .scanner_scanning--charge {
        width: 50px;
        height: 50px;
        border: 6px solid rgba(255, 255, 255, 0.3);
        border-top-color: #FF6B00; /* Seul le haut est orange */
        border-radius: 50%; /* Forme ronde */
        animation: charge 1s linear infinite;/* Rotation en 1 seconde, vitesse constante (linear), infini */
    }

     .scanner_scanning--text {
        color: white;
        font-weight: bold;
    }

    /* ÉTAT COMPLETED */
    .scanner_completed--main {
        position: relative;
        width: 100%;
        height: calc(100vh - 150px);
    }

    .scanner_completed--main img {
        width: 100%;
        height: 100%;
        object-fit: contain;
        cursor: pointer; /* Indique que l'image est cliquable */
        filter: brightness(0.5); /* Assombrit l'image */
    }

    /* Overlay AR ancré sur l'image */
    .scanner_completed--overlay {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background: rgba(255, 255, 255, 0.95);
        border: 3px solid #FF6B00;
        border-radius: 16px;
        padding: 1.5rem;
        text-align: center;
        min-width: 80%;
    }

    .scanner_completed--hotspot-title {
        color: #212121;
        font-size: 1.5rem;
        margin-bottom: 0.5rem ;
    }

    .scanner_completed--hotspot p {
        color: #666;
        margin: 0 0 1rem 0;
    }

    .scanner_completed--status {
        margin-bottom: 1rem;
    }

    .scanner_completed--status-text {
        display: inline-block;
        background: #4CAF50;
        color: white;
        padding: 0.5rem 1rem;
        border-radius: 20px;
        font-weight: bold;
        font-size: 0.9rem;
    }

    .scanner_completed--actions {
        margin-bottom: 0.8rem;
    }

    .scanner_completed--button {
        width: 100%;
        background-color: #FF6B00;
        color: white;
        padding: 1rem;
        font-size: 1rem;
        font-weight: bold;
        border: none;
        border-radius: 8px;
        cursor: pointer;
    }

    .scanner_completed--button:hover {
        background-color: #e66000;
    }

    .scanner_completed--footer {
        background: #212121;
        color: white;
        text-align: center;
        padding: 1rem;
    }

    .scanner_completed--footer-text {
        margin: 0;
        font-size: 0.9rem;
    }
    
</style>