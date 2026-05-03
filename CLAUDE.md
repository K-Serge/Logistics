# Logistics Trucking — Business Plan Context

> Respond ALWAYS in Russian. Код, коммиты — на английском.

## Репо и файлы
- **GitHub Pages:** https://k-serge.github.io/Logistics/?lang=ru (пароль: `1885`)
- **Локальный запуск:** `python3 -m http.server 8787` → http://localhost:8787
- **Главный файл:** `index.html` (1791 строк)
- **Переводы:** `lang/ru.js` (LANG_RU) + `lang/en.js` (LANG_EN, ~519 ключей)
- **Стартер-пакет партнёра:** `~/MyDocumetns/AI/Cloude/contexts/business-transport/documents/trucking-starter-package.xlsx`
- **Сессионный контекст:** `~/MyDocumetns/AI/Cloude/contexts/business-transport/documents/trucking-session-context.md`

## ⛔ ПРАВИЛО i18n — ОБЯЗАТЕЛЬНО
**Никакого хардкода русского текста в index.html.** Любой видимый текст — только через ключи:
1. Добавить ключ в `lang/ru.js` (LANG_RU) — русский текст
2. Добавить тот же ключ в `lang/en.js` (LANG_EN) — английский перевод
3. В HTML: `<element data-i18n="ключ">` (applyLang подставит нужный язык)
4. В JS-коде: читать через `dict[key]` где `dict = lang === 'en' ? LANG_EN : LANG_RU`

## Архитектура HTML
- `data-i18n="t001"` на элементах → `applyLang(lang)` в JS
- Страницы: `data-page="start|documents|warehouse|truck|expenses|risks|notes|updates"` → `showPage(page)`
- URL: `?lang=ru` / `?lang=en`, хранится в localStorage
- Пароль: `localStorage('wp_auth')` = `1885`
- Хедер/статистика скрыты везде кроме `start` (класс `overview-only`)
- Мобиль 430px: дропдауны скрыты (`display:none !important`), один тап = смена вкладки
- Таблицы обёрнуты в `.table-wrap` (overflow-x: auto), брейкпоинты 900/480/380px

## Что сделано (предыдущие сессии)
- Навигация: кнопка "Start" не переименовывается
- Удалён зелёный callout "Подтверждённые данные" с главной
- Удалена кнопка "Очистить" из Заметок
- Пароль overlay — только EN текст
- Партнёр: Itzel Zaldivar 50/50 (iNear/Galyna убраны)
- Фавиконка: 🚚 SVG на #2563eb
- Мобильная адаптация (iPhone 17 Pro Max)
- applyLang всегда вызывается при загрузке

## Известные особенности
- `notesClear` ссылается на удалённую кнопку — null-guard есть, безвредно
- Таблицы 7+ колонок (Warehouse, Market Analysis) — горизонтальный скролл, это ОК

---

## Бизнес-модель

### Партнёры
- **Serge** (Serhii Klement) + **Itzel Zaldivar** — 50/50
- Charlotte/Matthews NC | Credit Serge: 811 | CDL не нужен (нанимаем W2)

### SC Lane (Westrock Coffee)
- **Маршрут:** Concord NC ↔ Summerville SC — 211 mi one-way / 422 mi r/t
- **Ставка:** $1,500/r/t (fuel included, **без FSC** — требовать reopener clause!)
- **Объём:** 50 r/t/мес = 25 в день × 2 смены
- **Revenue:** $75,000/мес = **$900k/year**
- **Водители:** $85k/year W2 + 12% burden + health benefits ($500/мес employer)
- **Парковка:** бесплатно на складе Westrock

### Корпоративная структура
```
Serge + Itzel (50/50 физлица)
  → Wyoming LLC (холдинг, анонимный) — $550 setup + $860-960/year
    → North Carolina LLC (операционная)
      → MC/DOT/IRP/IFTA/страховка
```
Nominee Manager на публичных записях → wyomingllcattorney.com

### 4 варианта

| Вариант | Trucks | Drivers | r/t/мес | Revenue | NET/year | CAPEX cash |
|---------|--------|---------|---------|---------|----------|------------|
| V1-half | 1 | 1 | 25 | $450k | $232k | $167k |
| V1 original | 1 | 2 | 50 | $900k | $489k | $189k |
| **V1-double ⭐** | **2** | **2** | **50** | **$900k** | **$468k** | **$287k** |
| V2 SC+VA | 2 | 3 | 73 | $1,384k | $715k | $329k |

### Рекомендация запуска: PacLease Year 1
- **PacLease Full-Service:** $7,500/мес all-in (ТО + ремонты + replacement truck)
  - TLG Peterbilt Charlotte: **(704) 597-8600**
  - Year 1 NET: ~$36k/мес, CAPEX: $95k
- **Year 2-3:** добавить 2-й трак financed → TopMark Funding (866) 627-6644, 4.9% APR

### Что покупать (при финансировании)
- ✅ Cascadia 2021-22 DD15 Gen5, 350-400k mi, ~$80k
- ✅ Peterbilt 579 X15, Kenworth T680
- ✅ Trailers: 2× Dry Van 53' 2020-22, ~$22k each (или 0 если Westrock supplies pool)
- ❌ Cascadia 2015-18 Gen4, International ProStar, Volvo VNL 2017-19

### CAPEX разбивка (V1 original, financed)
- Reserve fund: $15k (breakdown buffer)
- Working capital: $40k (AR bridge net-30/45 Westrock)
- Insurance первый взнос, ELD, регистрации, drug consortium

---

## Открытые вопросы Westrock (КРИТИЧНО до покупки)
1. Trailers — shipper-supplied или carrier? ($44k разница в CAPEX)
2. Письменный контракт + volume commitment 12+ мес?
3. **FSC reopener clause** (квартальный reset по EIA diesel index) — обязателен
4. Detention pay $50-75/hr после 2 hrs free?
5. Net pay terms (net-30/45 или quick-pay)?

---

## Roadmap запуска (90 дней)
- **W1-2:** Wyoming LLC, NC LLC, EIN, USDOT, MC application + Westrock confirm
- **W3-5:** Insurance quotes, IFTA/IRP, BOC-3, truck inspection, PacLease quote
- **W5-6:** MC active, IRP plates, vendor onboarding
- **W6-8:** Hire 2 drivers, ELD install, test runs
- **W8+:** First revenue
- **M6:** DAT spot market (диверсификация 20-30%)
- **M12-18:** 2-й трак

---

## Лицензии (~$1,500 итого)
LLC (WY + NC foreign entity $250) + USDOT + MC + BOC-3 + drug consortium + IRP + IFTA + ELD
