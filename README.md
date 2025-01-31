# 📌 Что это и зачем?

Этот репозиторий содержит:

✅ **Списки доменов и IP-адресов**, используемых голосовыми серверами Discord, API и GUI.  
🛠 **Скрипты**:
- 📌 Парсинг IP из списка сабдоменов голосовых каналов.
- 🔍 Генерация и резолвинг сабдоменов `region[1-15000].discord.gg`.
- 📌 Создание и наполнение IPset списков с последующим импортом.
- 🔄 Конвертация в JSON для удобного импорта в **Amnezia**.

💡 **Репозиторий поможет настроить "корректную" маршрутизацию для "стабильной" работы Discord.**

---

## 📂 Структура Репозитория

### 🛠 Скрипты

| Скрипт | Описание |
|--------|----------|
| `main-domains-resolver.sh` | Резолвит основные домены Discord, сохраняет их IP и генерирует JSON список готовый к импорту в Amnezia. |
| `voice-domains-generator.sh` | Генерирует и резолвит домены голосовых серверов для указанных регионов. Записывает результат в фолдер `regions/` |
| `json-voice-ip-converter.sh` | Конвертирует результаты резолвинга голосовых серверов в JSON-формат готовый к импорту в Amnezia. |
| `ipset-adder.sh` | Создает IPset списки и добавляет в них IP-адреса, а также импортирует их в заданный IPset лист (_по умолчанию `unblock`_). |

### 📁 Каталоги

📂 **amnezia/** – JSON-файлы с IP-адресами для Amnezia.
📂 **regions/** – списки IP-адресов голосовых серверов по регионам.
📂 **main_domains/** – списки основных доменов и IP.
📂 **voice_domains/** – списки голосовых доменов и IP.
📂 **custom-solutions/** – решения от **заинтересованных** и **неравнодушных**.

---

## 🚀 Использование

### 🔹 Резолвинг основных серверов Discord
```bash
./main-domains-resolver.sh
```
📌 **Результаты:**
- Основные IP-адреса → `./main_domains/discord-main-ip-list`
- JSON-список для Amnezia → `./amnezia/amnezia-discord-domains.json`

### 🔹 Генерация и резолвинг доменов голосовых серверов
📌 Запуск по умолчанию:
```bash
./voice-domains-generator.sh
```

Регионы генерируемые по умолчанию:
- russia
- bucharest
- finland
- frankfurt
- madrid
- milan
- rotterdam
- stockholm
- warsaw

_Отредактируйте переменную `DEFAULT_REGIONS` в `voice-domains-generator.sh`, чтобы изменить пул регионов_

📌 Для конкретного региона:
```bash
./voice-domains-generator.sh singapore
```
✅ Результаты сохраняются в `regions/<имя региона>`

### 🔹 Конвертация в JSON для Amnezia
```bash
./json-voice-ip-converter.sh
```
📌 **Результаты:** JSON-файлы в `amnezia/`

### 🔹 Работа с IPset
📌 Добавить IP-адреса в IPset `unblock` (_имя листа по умолчанию_) в авто-режиме:
```bash
./ipset-adder.sh auto
```
📌 Добавить в кастомный IPset лист:
```bash
./ipset-adder.sh list <ip_list_name>
```
📌 Просто сгенерировать списки в IPset формате:
```bash
./ipset-adder.sh noipset
```
📌 Запуск в интерактивном режиме с выбором опций:
```bash
./ipset-adder.sh
```

---

## ⚙️ Требования

🔹 `jq` – для работы с JSON.
🔹 `parallel` – для параллельной обработки резолвинга.

---

## 🔥 Ветки `light` и `light-no-timeout`

Для роутеров с установленным **KVAS** доступна облегчённая версия репозитория в ветках:
🔹 [`light`](https://github.com/GhostRooter0953/discord-voice-ips/tree/light) – добавляет нулевые таймауты в IPset. Ветка ориентирована на **актуальную** версию КВАС'а, в бете которого используются таймауты.
🔹 [`light-no-timeout`](https://github.com/GhostRooter0953/discord-voice-ips/tree/light-no-timeout) – без таймаутов в IPset, что подходит для **релизной** версии КВАС'а (_как и ветка `master`_).
📌 **Подробнее о чудо-скрипте:** [kvas-adder](https://github.com/GhostRooter0953/discord-ips-kvas-adder)

---

## 📖 Короткий мануал по **Amnezia**

1️⃣ **Скачайте [репозиторий](https://github.com/GhostRooter0953/discord-voice-ips/tree/master)**.
2️⃣ **Включите раздельное туннелирование в Amnezia и выберите в селекторе "Только адреса из списка должны открываться через"**.
3️⃣ **Импортируйте списки:**
 📂 [Основные домены](https://github.com/GhostRooter0953/discord-voice-ips/blob/master/amnezia/amnezia-discord-domains.json).
 🎧 [Голосовые серверы](https://github.com/GhostRooter0953/discord-voice-ips/blob/master/amnezia/amnezia-voice-ip.json) (_или конкретный регион_).
4️⃣ **Подключитесь и проверьте работу Discord.** ✅

---

## 🔧 To-Do

🔹 **Доработка режимов под бета-версии КВАС'а (_ветка light_)**
🔹 **Сканер и резолвер сабдоменов, т.к. периодчески возникают подобные [ситуации](https://github.com/GhostRooter0953/discord-voice-ips/issues/1#issuecomment-2408466714)**
🔹 **Механизм автоматической актуализации IP списков и доменов в репозитории**
