# REVERSE_ENGINEERING_REPORT — hl7.fhir.r4.sv

## A. Загальний діагноз

### Виявлена архітектура
Інструкція щодо впровадження (IG) FHIR на основі SUSHI для шведо мовного пакунка (HL7 Sweden / hl7.fhir.r4.sv). Структура:

- `input/hl7.fhir.r4.sv.xml`: визначення IG (id, canonical, version, fhirVersion, сторінки, параметри)
- `input/translations/*.po`: 16 файлів перекладу gettext для CodeSystems
- `input/pagecontent/`: сторінки IG (index.md, translation-principles.md, тощо)
- `input/resources/`: лише `place-holder.txt` (жодних реальних ресурсів)
- `ig.ini`: конфігурація видавця IG
- `.github/workflows/validate-docs.yml`: CI для валідації з Sushi та IG Publisher

### Технології та залежності
- SUSHI / fsh-sushi
- FHIR R4 (fhirVersion: 4.0.1)
- IG Publisher (на основі Jekyll)
- Жодних реальних ресурсів FHIR (лише place-holder.txt)

### Стан підтримки
Гałтьова гілка: main. Репозиторій: https://github.com/HL7Sweden/hl7.fhir.r4.sv. Версія 0.1.0.

### Існуючі механізми тестування
Автоматизованих тестів не виявлено. Існуючий workflow CI (validate-docs.yml), але не тестує вміст FHIR.

### Обмеження дослідження
- SUSHI не встановлений; збірку IG не виконано.
- REA 6.7.0 не працює; лише статичний аналіз.

## B. Виявлені проблеми

| ID | Заголовок | Severity | Статус | Локація |
|----|-----------|----------|--------|----------|
| REA-sv-001 | `hl7.fhir.r4.sv.xml` використовує `releaselabel` (малі літери) | P3 | CONFIRMED | `hl7.fhir.r4.sv.xml:46` |
| REA-sv-002 | Файл `translation-princples.md` (помилка правопису) дублюється | P3 | CONFIRMED | `input/pagecontent/translation-princples.md` |
| REA-sv-003 | `input/resources/` містить лише `place-holder.txt` | P3 | CONFIRMED | `input/resources/` |

### Деталі підтверджених проблем

**REA-sv-001 (P3, CONFIRMED)**: XML IG використовує параметр `releaselabel` (усі маленькі літери) на рядку 46. Хоча деякі версії SUSHI приймають цей варіант, канонічна форма — `releaseLabel` (camelCase). Це може спричинити проблеми сумісності з строгишими версіями SUSHI.

Довід: `hl7.fhir.r4.sv.xml:46` — `<parameter><code value="releaselabel"/><value value="Working Copy"/>