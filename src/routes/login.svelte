<script>

    let email = $state("");
    let password = $state("");

    const handleSubmit = () => {
        //Vérifier que les champs ne sont pas vides
        if (email === "" || password === "") {
            alert("L'e-mail et le mot de passe sont requis.");
            return;
        }
        if (!email.includes("@")) {
            alert("Veuillez entrer une adresse valide");
            return;
        };

        console.log("Email:", email);
        console.log("Password:", password);
    
        //Naviguer vers le dashboard si les champs sont valides
    };
</script>

<main>
    <img class="logo" src="/images/logo_btp.png"  height="100px" alt="Logo Chantier BTP"  />
      <h1>Bienvenue<br>sur l'application BTP-AR</h1>

    <form class="connexion_form" action="" method="post">
    <div class="connexion_box">
        <label class="connexion_label" for="mail">E-mail</label>
        <input class="connexion_input" bind:value={email} type="email" name="" id="mail">
    </div>
    <div class="connexion_box">
        <label class="connexion_label" for="password">Mot de passe</label>
        <input class="connexion_input" bind:value={password} type="password" name="" id="password">
    </div>
    <a href="#" class="connexion_forgot">Mot de passe oublié ?</a>
    <div>
    <button on:click={handleSubmit} class="connexion_button" type="button">Se connecter</button>
    </div>
</form>
</main>

<style>
    main {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh;
        font-family: 'Arial', sans-serif;
        margin: 1em;
    }
    h1 {
        color: #FF6B00;
        margin-bottom: 2em;
        text-align: center;
        font-size: 2em;
    }
    .connexion_form {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 1em;
    }
    .connexion_box {
        display: flex;
        flex-direction: column;
    }
    a {
     align-self: self-end;
     font-size: 0.9em;
     margin-bottom: 1.5em;
    }
    .connexion_button {
        background-color: #FF6B00;
        color: white;
        padding: 0.5em 1em;
        cursor: pointer;
        border-radius: 0.3em;
        border: 1px solid #ccc;
    }
    .connexion_input {
        padding: 0.5em;
        border: 1px solid #ccc;
        border-radius: 0.3em;
    }
   

</style>
