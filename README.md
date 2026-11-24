# TeamForge ⚔️

> **Tactical single-PC workspace & safe practice arena for competitive programming teams (ICPC / Codeforces).**

[![PHP Version](https://img.shields.io/badge/PHP-8.5-777BB4?style=flat&logo=php&logoColor=white)](https://www.php.net/)
[![Laravel](https://img.shields.io/badge/Laravel-11%2B-FF2D20?style=flat&logo=laravel&logoColor=white)](https://laravel.com/)
[![React](https://img.shields.io/badge/React-19-61DAFB?style=flat&logo=react&logoColor=black)](https://react.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-26-339933?style=flat&logo=node.js&logoColor=white)](https://nodejs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16%2B-4169E1?style=flat&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 🌐 English Version

### 📌 Project Overview

**TeamForge** is an open-core tactical dashboard and team management workspace designed specifically for competitive programming teams preparing for ICPC-style contests.

The primary obstacle during real 5-hour contests is the **inefficient sharing of a single workstation across three teammates**: one participant frequently gets stuck debugging code on-screen for 40+ minutes while the other two remain idle, and training directly on production platforms like Codeforces risks dropping individual competitive ratings.

**TeamForge** structures team practice into a streamlined, esports-grade experience:
* **Zero Rating Risk:** Conduct practice rounds using authentic Codeforces problem sets without risking rating deductions on official handles.
* **Single-PC Access Management:** Enforce an automated, intelligent keyboard queue with configurable time limits, timeouts, and rotation reminders.
* **Real-Time Synchronized Dashboards:** Keep the central workstation and members' mobile devices in sync using WebSockets.
* **Post-Contest Telemetry & Analytics:** Review Gantt-chart timelines of workstation usage, bottleneck detection, and penalty attribution.

---

### 💼 Distribution Model (Open-Core)

TeamForge follows an **Open-Core** distribution model, providing an open-source self-hosted baseline alongside managed cloud tiers for teams, clubs, and academic institutions:

#### 🟢 Community Edition (Open-Source / Self-Hosted)
* **100% Free and Open Source** under the MIT License.
* Full access to source code for local execution or private server hosting.
* Single-workstation queue scheduling and session timers.
* Automated contest generation via the Codeforces API.
* Unlimited local training sessions for self-hosted teams.

#### 🟣 Cloud Free Tier (Hosted Web Version with Limits)
* Instant web access with no server setup or database configuration required.
* 1 active team workspace.
* Up to 3 practice contests per month.
* 14-day history retention for contest telemetry.

#### 🔷 TeamForge Pro & Enterprise (Commercial Editions)
* **Pro (For Competitive Teams):**
  * Unlimited cloud-hosted training sessions.
  * In-depth telemetry (keyboard stall detection, penalty impact analysis).
  * Ghost Match Mode: compete in real time against historical team submissions.
  * Export comprehensive post-mortem reports to PDF.
* **Enterprise / Campus (For Universities & Coaches):**
  * Multi-team instructor dashboard to monitor entire university rosters.
  * Multi-tenancy isolation for computer science departments.
  * Custom internal mirror contests with centralized scoreboards.

---

### 🏛 Architecture & Design Patterns (OOP)

The application adheres to **SOLID** principles and classic **GoF** design patterns:

* **State Pattern:** Governs the lifecycle of the shared physical computer (`FreeState`, `OccupiedState`, `OverdueState`) and team member activity statuses.
* **Strategy Pattern:** Implements interchangeable queue allocation algorithms (FIFO, Shortest Job First, Urgency Priority).
* **Adapter Pattern:** Isolates external contest data providers (Codeforces API, AtCoder) behind unified typed interfaces.
* **Observer / Event-Driven Architecture:** Pushes real-time workstation status updates to connected client devices via WebSockets.

---

### 🛠 Tech Stack

* **Backend:** PHP 8.5, Laravel 11+
* **Frontend:** React 19, Inertia.js, Tailwind CSS
* **Runtime & Tooling:** Node.js 26, Vite
* **Database:** PostgreSQL 16+
* **Real-Time Engine:** Laravel Reverb (WebSockets)
* **Local Development Stack:** Laravel Herd, DBngin, TablePlus

---

### 🚀 Installation & Local Setup (Self-Hosted)

#### Prerequisites
* **PHP 8.5+** (with `pdo_pgsql`, `mbstring`, and `curl` extensions)
* **Composer 2+**
* **Node.js 26+** & **npm**
* **PostgreSQL 16+** (via DBngin, native service, or Docker)
* **Laravel Herd** (recommended for macOS/Windows)

#### Step 1: Clone Repository
```bash
git clone https://github.com/GubarVlad/teamforge.git
cd teamforge
```

#### Step 2: Install Dependencies
```bash
# Install PHP dependencies
composer install

# Install frontend JavaScript dependencies
npm install
```

#### Step 3: Configure Environment
1. Copy the example configuration file:
   ```bash
   cp .env.example .env
   ```
2. Generate an application encryption key:
   ```bash
   php artisan key:generate
   ```
3. Update database credentials in `.env`:
   ```env
   DB_CONNECTION=pgsql
   DB_HOST=127.0.0.1
   DB_PORT=5432
   DB_DATABASE=teamforge_dev
   DB_USERNAME=postgres
   DB_PASSWORD=
   ```

#### Step 4: Run Database Migrations
Create the `teamforge_dev` database in PostgreSQL (via TablePlus/DBngin), then execute:
```bash
php artisan migrate --seed
```

#### Step 5: Start Development Servers
When using **Laravel Herd**, the application is automatically accessible at:
```text
http://teamforge.test
```

To build and compile frontend assets with hot module replacement:
```bash
npm run dev
```

Run asynchronous background workers and WebSockets (in separate terminal sessions):
```bash
# Queue worker
php artisan queue:work

# WebSocket server
php artisan reverb:start
```

---

## 🇷🇺 Русская версия

### 📌 Описание проекта

**TeamForge** — это специализированная тактическая платформа и командное рабочее пространство для подготовки к олимпиадам по спортивному программированию в формате ICPC.

Главная проблема команд на 5-часовых соревнованиях — **хаос в распределении одного компьютера на троих**: один участник зависает за клавиатурой на долгую отладку (40+ минут), пока остальные бездействуют, а совместные тренировки на боевом Codeforces несут постоянный риск случайной потери личного рейтинга.

**TeamForge** структурирует командные тренировки по киберспортивным стандартам:
* **Zero Rating Risk:** генерация тренировок на реальных задачах Codeforces без риска потери очков на официальных аккаунтах.
* **Single-PC Management:** автоматизированная очередь к единственному компьютеру с контролем слотов времени и таймерами сессий.
* **Синхронизация в реальном времени:** единый дашборд для монитора соревновательного ПК и смартфонов/планшетов команды через WebSockets.
* **Телеметрия после контеста:** детальная аналитика использования машины (диаграммы Ганта, фиксация простоев, распределение штрафного времени).

---

### 💼 Модель распространения (Open-Core)

Проект развивается по модели **Open-Core**, объединяя открытую версию для комьюнити и коммерческие тарифы для клубов и университетов:

#### 🟢 Community Edition (Open-Source / Self-Hosted)
* **100% бесплатно и открыто** (лицензия MIT).
* Полный исходный код для самостоятельного запуска локально или на собственном сервере.
* Базовая очередь доступа к ПК и таймеры сессий.
* Генерация тренировочных контестов через Codeforces API.
* Неограниченное число тренировок для вашей команды.

#### 🟣 Cloud Free Tier (Бесплатная веб-версия с лимитами)
* Быстрый старт в браузере без необходимости разворачивать сервер или базу данных.
* 1 активная команда.
* Лимит: до 3 тренировочных контестов в месяц.
* Хранение истории телеметрии за последние 14 дней.

#### 🔷 TeamForge Pro & Enterprise (Коммерческая версия)
* **Pro (для команд):**
  * Безлимитные тренировочные сессии в облаке.
  * Продвинутая аналитика (детектор зависаний за ПК, штрафной аудит).
  * Режим «Ghost Match» (соревнование с виртуальными соперниками на базе архивов Codeforces).
  * Экспорт отчетов тренировок в PDF.
* **Enterprise / Campus (для вузов и тренеров):**
  * Тренерский дашборд: мониторинг прогресса десятков университетских команд.
  * Мультитенантность (изолированные пространства кафедры/клуба).
  * Проведение закрытых университетских сборов с централизованной таблицей.

---

### 🏛 Архитектура и паттерны (ООПиП)

Архитектура системы спроектирована по принципам **SOLID** с применением классических паттернов **GoF**:

* **State Pattern:** управление состояниями рабочего места (`FreeState`, `OccupiedState`, `OverdueState`) и участников команды.
* **Strategy Pattern:** взаимозаменяемые алгоритмы управления приоритетом очереди (FIFO, Shortest Job First, Urgency Priority).
* **Adapter Pattern:** унификация работы с внешними платформами (Codeforces API, AtCoder) через строгие интерфейсы.
* **Observer / Event-Driven:** доставка событий очереди и таймеров на мобильные клиенты через WebSockets.

---

### 🛠 Технологический стек

* **Backend:** PHP 8.5, Laravel 11+
* **Frontend:** React 19, Inertia.js, Tailwind CSS
* **Среда выполнения и сборка:** Node.js 26, Vite
* **База данных:** PostgreSQL 16+
* **Шина реального времени:** Laravel Reverb (WebSockets)
* **Локальное окружение:** Laravel Herd, DBngin, TablePlus

---

### 🚀 Установка и локальный запуск (Self-Hosted)

#### Системные требования
* **PHP 8.5+** (с модулями `pdo_pgsql`, `mbstring`, `curl`)
* **Composer 2+**
* **Node.js 26+** & **npm**
* **PostgreSQL 16+** (через DBngin или системный сервис)
* **Laravel Herd** (рекомендуется для macOS/Windows)

#### Шаг 1. Клонирование репозитория
```bash
git clone https://github.com/GubarVlad/teamforge.git
cd teamforge
```

#### Шаг 2. Установка зависимостей
```bash
# Установка PHP-пакетов
composer install

# Установка npm-зависимостей
npm install
```

#### Шаг 3. Настройка конфигурации
1. Создайте копию файла окружения:
   ```bash
   cp .env.example .env
   ```
2. Сгенерируйте ключ приложения:
   ```bash
   php artisan key:generate
   ```
3. Укажите параметры подключения к PostgreSQL в файле `.env`:
   ```env
   DB_CONNECTION=pgsql
   DB_HOST=127.0.0.1
   DB_PORT=5432
   DB_DATABASE=teamforge_dev
   DB_USERNAME=postgres
   DB_PASSWORD=
   ```

#### Шаг 4. Миграции и тестовые данные
Создайте базу данных `teamforge_dev` в TablePlus / DBngin и запустите:
```bash
php artisan migrate --seed
```

#### Шаг 5. Запуск серверов
В среде **Laravel Herd** проект сразу доступен по адресу:
```text
http://teamforge.test
```

Для сборки фронтенда (React + Vite) выполните:
```bash
npm run dev
```

Для обработки очередей и работы WebSockets (в отдельных окнах терминала):
```bash
# Воркер очередей
php artisan queue:work

# WebSocket-сервер
php artisan reverb:start
```

---

## 📄 License / Лицензия

TeamForge is distributed under the **MIT License**. For more information, see [LICENSE](LICENSE).  
TeamForge распространяется под лицензией **MIT**. Подробная информация находится в файле [LICENSE](LICENSE).