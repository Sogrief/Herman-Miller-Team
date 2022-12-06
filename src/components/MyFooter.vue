<script></script>
<template>
  <footer>
    <div class="footer">
      <div class="column">
        <p>
          Recevez en avant-première les offres spéciales Herman Miller Gaming et
          les nouveaux lancements de produits par courrier électronique.
        </p>

        <p>INSCRIVEZ-VOUS À NOTRE NEWSLETTER</p>
        <input type="textarea" />
        <button>S'abonner</button>
      </div>

      <div class="column">
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
  width: 1200px;
  height: 323px;
  float: left;
}
div.column {
  float: left;
  width: 400px;

  a {
    display: flex;
    flex-direction: column;
  }
}

div.column-2 {
  display: inline-block;
}
.footer-legal {
  display: inline;
  ul {
    list-style-type: none;
  }
}
</style>
