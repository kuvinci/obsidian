### Різниця між Laravel та WordPress
Laravel - MVC Framework

WordPress - Event Driven System (Готова система, плагіни, теми, функціонал)
---
### WordPress "під капотом"
Event Driven System (Hooks)
- Actions
- Filters
---
### WP Hooks
- Системні хуки
- Кастомні хуки
- Екшенши та Фільтри

```php
add_action('init', 'my_init_function');
add_filter('the_title', 'modify_title');
```

---
### Плагіни та теми
- Як працюють плагіни
- Маркетплейс плагінів
- Загальний опис, як працює тема і шо воно таке
---
### Структура WP теми
- Нафіга вони потрібні
- index.php
- style.css
- движок вибору шаблонів
---
### Структура бази даних
- **wp_posts**: posts, pages, CPT
- **wp_postmeta**: Додаткова інфа для постів (ACF і тд.)
- **wp_options**: Глобальні налаштування
- **wp_terms / wp_term_taxonomy / wp_term_relationships**: Таксономії
- **wp_users / wp_usermeta**: Без коментарів
- **wp_comments / wp_commentmeta**: Без коментарів


---
### Пост тайпи (Post Type)
---
### Таксономії (Categories, Tags і кастомні)
---
### Глобальні змінні
$post - дані сутності в поточному "циклі"
Коли перебираєте пости, можна тягнути різні дані, такі як:
```php
$post->ID,
$post->post_title, 
$post->post_content
// І ще купу іншого
```

---
$post не єдина, хоч і найчастіше смикається.

Ще є:
- **$wpdb** – глобальний об’єкт для взаємодії з базою даних.
- **$wp_query** – зберігає основний запит (головну вибірку контенту) для поточної сторінки.
- **$wp_rewrite** – об’єкт, відповідальний за переписування URL-адрес (friendly URLs).
- **$wp** – запит, маршрут, змінні запиту та інші дані, отримані після ініту WP.
- **$wp_roles** – (permissions/capabilities).
- **$current_user** – авторизований юзер.
- **$comment** – діч, нікому не потрібна

---

### WP Query
```php
$args = [
	'post_type' => 'book',
	'posts_per_page' => 5
];

$query = new WP_Query($args);
```
---
### Headless WP
---
### Популярні плагіни
- **Yoast SEO** або **All in One SEO**
- WooCommerce - ліпити магазин з гівна і палок
- Advanced Custom Fields (ACF) - Кастомні поля
- Query Monitor - Дуже зручний дебаг хуків, запитів, навантаження і тд
- Debug Bar - Теж для дебагу
- Log Deprecated Notices - Показує варнінги і старі функції
- Ну і ще мільйони інших

TEST

![[WordPress концептуально 2025-04-12 22.30.39.excalidraw]]

/excalidraw