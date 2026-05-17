# LLORA — AI Dashcam Landing

Премиум landing-page для **LLORA** — AI-видеорегистраторов и платформы управления флотом для логистики США.

Сайт построен как **single-page** с разделами: Hero, Trust, Why LLORA, Программа (Fleet Manager), Камеры (Hardware), AI Vision, Платформа (specs), Тариф, Заявка.

## Запуск

Это статический сайт — никакой сборки не нужно.

**Самый простой вариант:**
```bash
# Python (есть на macOS / Linux / Windows + Python)
python -m http.server 8080
# Откройте http://localhost:8080
```

Или открыть `index.html` напрямую в Chrome / Edge / Safari (двойной клик).

Подготовленные конфигурации для dev-серверов лежат в `.claude/launch.json`.

## Стек

- **HTML / CSS / JS** — без фреймворков, без npm, без сборки
- Один файл `index.html` (~150 KB) — весь CSS и JS inline
- Шрифт **Inter** через Google Fonts (CDN)

## Структура

```
.
├── index.html          # вся вёрстка + стили + JS в одном файле
├── screens/            # скриншоты платформы Union, фото продуктов
│   ├── dashboard.png
│   ├── live-video.png
│   ├── alert-map.png
│   ├── safety-scores.png
│   ├── product-dual.png        # фото LLORA Dual (TODO)
│   ├── product-5channel.png    # фото LLORA 5-Channel (TODO)
│   └── pilot-bg.jpg            # фоновое фото для cinematic-секции (TODO)
├── .claude/
│   └── launch.json     # dev-server конфиги
└── README.md
```

## Что нужно докинуть в `screens/`

| Файл | Назначение |
|---|---|
| `product-dual.png` | Фото LLORA Dual (камера) |
| `product-5channel.png` | Фото LLORA 5-Channel |
| `hero-video.mp4` (опционально) | Видео в hero-ноутбуке |

Подробности — в комментариях `<!-- TODO: ... -->` внутри `index.html`.

## Подключение бэкенда

Форма заявки шлёт `POST` с JSON:
```json
{
  "name": "...",
  "company": "...",
  "email": "...",
  "phone": "+1 (...) ...-....",
  "fleet_size": "1-9 | 10-49 | 50-174 | 175-999 | 1000+",
  "ts": "ISO timestamp"
}
```

Заменить плейсхолдер на реальный endpoint в `index.html` (поиск `TODO: replace with real endpoint`):

```js
await fetch('https://your-api.com/api/leads', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify(data)
});
```

## Особенности

- **JS-snap скролл** — каждое колесо мыши плавно ведёт к следующему разделу (отключается на mobile / `prefers-reduced-motion`)
- **Бесконечный marquee** интеграций в Trust-секции
- **Табы платформы** с переключением скриншотов
- **Inline-валидация** формы + toast-уведомления
- **A11y:** focus-visible, ARIA-роли, клавиатурная навигация, prefers-reduced-motion
- **Responsive:** 3 брейкпоинта (1080 / 900 / 760)

---

© 2026 Route ELD LLC
