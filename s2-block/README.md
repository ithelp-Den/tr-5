# Блок S2 + попап-слайдер програм

Блок «SO WHAT DO YOU GET?» з сіткою програм і попапом на 16 слайдів.
Винесено 1 в 1 з `index.html`, `css-t2/main.css` і `js-t/modal.js`. Дизайн і логіка не змінювались.

## Що в папці

```
s2-block/
├── s2.html          ← HTML для вставки (блок s2 + попап)
├── css/s2.css       ← всі стилі блоку і попапу (десктоп + мобілка до 440px)
├── js/s2-modal.js   ← дані 16 слайдів + Swiper + відкриття/закриття попапу
├── images/          ← картинки блоку (imgn*.webp)
│   ├── icons/       ← зірочка стрічки, стрілки, іконки play/time/man
│   └── swipe/       ← обкладинки слайдів card1–card16
└── demo.html        ← готова сторінка, щоб перевірити блок окремо
```

## Як перенести в інший дизайн

1. Скопіювати папку `s2-block` у **корінь** сайту, поруч з `index.html`.
   Усі шляхи мають вигляд `./s2-block/...`, тому більше нічого правити не треба.
2. У `<head>`:
   ```html
   <link href="https://fonts.googleapis.com/css2?family=Anton&family=Source+Sans+3:wght@400;500;600;700;800;900&display=swap" rel="stylesheet">
   <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.css" />
   <link rel="stylesheet" href="./s2-block/css/s2.css?v=1">
   ```
3. З `s2.html`:
   - `<div class="s2">…</div>` вставити в потрібне місце сторінки;
   - `<div class="modal-overlay" id="programsModal">…</div>` вставити в `<body>` (краще перед `</body>`).
4. Перед `</body>` (Swiper обов'язково **перед** s2-modal.js):
   ```html
   <script src="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.js"></script>
   <script src="./s2-block/js/s2-modal.js?v=1"></script>
   ```

Якщо Swiper або шрифти на сторінці вже підключені, вдруге їх не додавай.

## Важливо

- **Ширина.** Блок зверстаний під макет 428px. До 440px усе перераховується у `vw`.
  На сторінці він має стояти в контейнері з `max-width: 440px` (як `.wrapper` в оригіналі).
- **Кнопка оплати.** Атрибути `data-pay="v1"`, `data-pay-price="v1"` і клас `check-click` обробляє скрипт платформи (`/_t/l.js`), а не цей блок.
  Посилання й ціну міняй прямо в `s2.html`.
- **Конфлікти класів.** Класи `.q-pill`, `.s2-marquee-*` і `.s2-star` використовуються і в інших блоках оригінального лендінгу (s4, st7, st8).
  Якщо в новому дизайні вже є `main.css` з цього лендінгу, правила просто збігаються: нічого не зламається.
- **Один попап на сторінку.** `id="programsModal"` і `id="modalSwiperWrapper"` унікальні: двічі вставляти не можна.
- **Порядок правил у `s2.css` не міняй.** `.s2-marquee-container` має йти після `.modal-marquee`, від цього залежить вигляд стрічки в попапі.

## Як правити контент

- **Тексти слайдів:** масив `programsData` на початку `js/s2-modal.js`.
  `theme: 'dark'` — білий текст на картці, будь-яке інше значення — чорний.
- **Яка картинка в сітці відкриває який слайд:** `data-slide="N"` у `s2.html`.
  `N` — це номер у `programsData`, рахунок з 0.
