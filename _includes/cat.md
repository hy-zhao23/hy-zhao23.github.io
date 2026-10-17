<div class="cat-divider">🐾</div>

<div class="cat-footer">
  <p><em>Meet Caterpillar, a.k.a. Kaiby. Her lab skills include, but are not limited to, chewing pens, napping, and keyboard dancing.</em></p>
  <div class="cat-gallery">
    <img src="./assets/img/cat/reviewing.jpg" alt="Caterpillar chewing a pen while I review a paper" loading="lazy">
    <img src="./assets/img/cat/napping.jpg" alt="Caterpillar asleep in her woven basket" loading="lazy">
    <img src="./assets/img/cat/laptop.jpg" alt="Caterpillar sitting on my laptop keyboard" loading="lazy">
  </div>
</div>

<style>
  .cat-divider {
    display: flex;
    align-items: center;
    gap: 12px;
    margin: 30px 0 14px;
    font-size: 1rem;
  }
  .cat-divider::before,
  .cat-divider::after {
    content: "";
    flex: 1;
    border-top: 1px solid #e5e5e5;
  }
  .cat-footer {
    font-family: "Chalkboard SE", "Chalkboard", "Comic Sans MS", cursive;
    font-size: 0.9rem;
    text-align: center;
  }
  .cat-footer p {
    margin: 0 0 10px;
  }
  .cat-gallery {
    display: flex;
    justify-content: center;
    gap: 8px;
  }
  .cat-gallery img {
    width: 80px;
    height: 80px;
    object-fit: cover;
    border-radius: 6px;
  }
  @media (prefers-color-scheme: dark) {
    .cat-divider::before,
    .cat-divider::after {
      border-top-color: #3a3b48;
    }
  }
</style>
