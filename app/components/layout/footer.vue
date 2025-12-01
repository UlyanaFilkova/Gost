<template>
  <footer class="footer">
    <div class="container">
      <div class="row top">
        <div class="col footer-about">
          <h2 class="footer-heading">Мультитул, г. Витебск</h2>
          <p>
            Надёжный белорусский поставщик крепежных изделий, ручного инструмента
            и электроинструмента из Китая, Тайваня и Европы.
          </p>
        </div>

        <div class="col footer-links-col">
          <h2 class="footer-heading">Ссылки</h2>
          <ul class="footer-links">
            <li><NuxtLink to="/catalog/">Каталог</NuxtLink></li>
            <li><NuxtLink to="/search/">Поиск</NuxtLink></li>
            <li><NuxtLink to="/brand/">Бренды</NuxtLink></li>
            <li><NuxtLink to="/sales/">Акции</NuxtLink></li>
            <li><NuxtLink to="/delivery/">Оплата и доставка</NuxtLink></li>
            <li><NuxtLink to="/contacts/">Контакты</NuxtLink></li>
          </ul>
        </div>

        <div class="col footer-contact">
          <h2 class="footer-heading">Контакты</h2>
          <ul class="footer-contact-list">
            <li>
              <i class="fa fa-location-arrow"></i>
              Беларусь, г. Витебск, пр-т Фрунзе, 39а, к.17
            </li>
            <li>
              <a href="tel:+375298135797">
                <i class="fa fa-phone"></i> +375 (29) 813-57-97
              </a>
            </li>
            <li>
              <a href="mailto:dm.krep@mail.ru">
                <i class="fa fa-envelope"></i> dm.krep@mail.ru
              </a>
            </li>
          </ul>
        </div>
      </div>

      <div class="row bottom">
        <p class="copyright">
          ООО Мультитул © |
          Разработка сайта —
          <a href="https://50tex.by" target="_blank">50 текс</a>
        </p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: var(--color-primary);
  color: var(--color-text-light);
  padding: 40px 0;
  font-size: 15px;
  line-height: 1.6;
}

.container {
  margin: 0 auto;
  padding: 0 20px;
}

.row.top {
  display: flex;
  flex-wrap: wrap;
  gap: 40px;
}

.col {
  flex: 1 1 calc(33% - 40px);
  min-width: 260px;
}

.footer-heading {
  font-size: 20px;
  margin-bottom: 15px;
  font-weight: bold;
  color: var(--color-accent);
}

.footer-links {
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer-links li {
  margin-bottom: 8px;
}

.footer-links a {
  color: var(--color-text-light);
  text-decoration: none;
  transition: color 0.2s ease;
}

.footer-links a:hover {
  color: var(--color-accent);
}

.footer-contact-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer-contact-list li {
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  gap: 10px;
}

.footer-contact-list a {
  color: var(--color-text-light);
  text-decoration: none;
  transition: color 0.2s ease;
}

.footer-contact-list a:hover {
  color: var(--color-accent);
}

.row.bottom {
  text-align: center;
  margin-top: 40px;
}

.row.bottom a {
  color: var(--color-accent);
}

.row.bottom a:hover {
  text-decoration: underline;
}

@media (max-width: 768px) {
  .col {
    flex: 1 1 100%;
  }
}
</style>
