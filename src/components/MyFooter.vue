<script>
import MyTitle from "./../components/MyTitle.vue";
import MyText from "./../components/MyText.vue";
</script>
<template>
  <footer>
    <div class="footer">
      <div class="column1">
        <p class="logo">HERMAN MILLER</p>
        <p>
          Recevez en avant-première les offres spéciales Herman Miller Gaming et
          les nouveaux lancements de produits par courrier électronique.
        </p>

        <p>INSCRIVEZ-VOUS À NOTRE NEWSLETTER</p>
        <input type="textarea" />
        <button>S'abonner</button>
      </div>

      <div class="column2">
        <div class="column-2">
          <p class="title-menu">SERVICE CLIENT</p>
          <a href="#">Garantie</a>
          <a href="#">Retour et remboursement</a>
          <a href="#">FAQ</a>
          <a href="#">Livraison</a>
        </div>

        <div class="column-2">
          <p class="title-menu">NAVIGATION</p>
          <a href="#">Accueil</a>
          <a href="#">Catalogue</a>
          <a href="#">Conseils</a>
          <a href="#">Connexion</a>
        </div>

        <div class="column-2">
          <p class="title-menu">ENTREPRISE</p>
          <a href="#">À propos</a>
          <a href="#">Contact</a>
        </div>
      </div>

      <div class="column">
        <p class="title-menu">Rejoignez-nous !</p>
        <a href="#"></a>
        <a href="#"></a>
        <a href="#"></a>
        <a href="#"></a>
      </div>
    </div>

    <div class="footer-legal">
      <ul>
        <li><a href="#">Mentions légales</a></li>
        <li><a href="#">Cookies</a></li>
        <li><a href="#">RGPD</a></li>
        <li><a href="#">CGV</a></li>
        <li><a href="#">Plan</a></li>
      </ul>

      <ul>
        <li><img src="" alt="" /></li>
        <li><img src="" alt="" /></li>
        <li><img src="" alt="" /></li>
        <li><img src="" alt="" /></li>
        <li><img src="" alt="" /></li>
      </ul>
    </div>
  </footer>
</template>

<style lang="scss" scoped>
div.footer {
  display: flex;
  margin: 46px;
  gap: 100px;
}
.column1 {
  width: 360px;
}
.column2 {
  display: flex;
  gap: 45px;
}

div.column-2 {
  display: flex;
  flex-direction: column;
}

.footer-legal {
  display: flex;
  margin: 45px;

  ul {
    list-style-type: none;
    display: flex;
    gap: 20px;
  }
}

p {
  color: #c5c5c5;
  font-family: $textFontFamily;
}

a {
  color: #c5c5c5;
  font-family: $textFontFamily;
}

.title-menu {
  font-size: 16px;
  color: white;
  font-family: $titleFontFamily;
}

.logo {
  font-family: $logoFontFamily;
  color: white;
  font-size: 25px;
  letter-spacing: 2.6px;
}
</style>
