#!/usr/bin/env python3
# brawl_stars_info.py
"""
Скрипт для сбора информации об игре Brawl Stars.
Создаёт структуру файлов для GitHub-репозитория.
"""

import os
import json
import datetime
from typing import Dict, List

# --- Конфигурация ---
REPO_NAME = "brawl-stars-info"
AUTHOR = "YourGitHubUsername"
DESCRIPTION = "Актуальная информация об игре Brawl Stars: бойцы, карты, события, обновления"

# Данные о бойцах (пример)
BRAWLERS = [
    {"name": "Спайк", "rarity": "Легендарный", "class": "Снайпер", "health": 2600, "damage": 800},
    {"name": "Кольт", "rarity": "Редкий", "class": "Стрелок", "health": 2800, "damage": 420},
    {"name": "Шелли", "rarity": "Начинающий", "class": "Боец ближнего боя", "health": 3000, "damage": 300},
    {"name": "Лу", "rarity": "Сверхредкий", "class": "Контроллер", "health": 2600, "damage": 400},
    {"name": "Фанг", "rarity": "Эпический", "class": "Ассасин", "health": 3200, "damage": 450},
]

# Новости (пример)
NEWS = [
    {"date": "2025-03-10", "title": "Обновление: новый боец Мелоди", "content": "Музыкальный ассасин с особыми способностями."},
    {"date": "2025-02-20", "title": "Киберспортивный сезон 2025", "content": "Старт квалификаций на мировое первенство."},
    {"date": "2025-02-01", "title": "Балансные изменения", "content": "Нерф Лолы и бафф Эдгара."},
]

# Режимы игры
GAME_MODES = [
    "Баунти", "Кража", "Горячая зона", "Натиск", "Удар чемпионов", "Вышибалы"
]

def create_directory_structure():
    """Создаёт папки под данные"""
    dirs = ['data', 'docs', 'images']
    for d in dirs:
        os.makedirs(d, exist_ok=True)
    print("✓ Папки созданы")

def save_brawlers_json():
    """Сохраняет список бойцов в JSON"""
    with open('data/brawlers.json', 'w', encoding='utf-8') as f:
        json.dump(BRAWLERS, f, ensure_ascii=False, indent=2)
    print("✓ Сохранены бойцы (data/brawlers.json)")

def save_news_json():
    """Сохраняет новости в JSON"""
    with open('data/news.json', 'w', encoding='utf-8') as f:
        json.dump(NEWS, f, ensure_ascii=False, indent=2)
    print("✓ Сохранены новости (data/news.json)")

def save_modes_txt():
    """Сохраняет режимы игры в текстовый файл"""
    with open('data/game_modes.txt', 'w', encoding='utf-8') as f:
        for mode in GAME_MODES:
            f.write(f"{mode}\n")
    print("✓ Сохранены режимы игры (data/game_modes.txt)")

def generate_markdown_report():
    """Генерирует информационный отчёт в формате Markdown"""
    md = f"""# 🎮 Brawl Stars Info

> Актуальная информация об игре Brawl Stars  
**Последнее обновление:** {datetime.datetime.now().strftime("%Y-%m-%d %H:%M")}  
**Автор:** {AUTHOR}

## 📊 Быстрая статистика
- **Бойцов в базе:** {len(BRAWLERS)}
- **Режимов игры:** {len(GAME_MODES)}
- **Новостей:** {len(NEWS)}

## 🥊 Список бойцов
| Имя | Редкость | Класс | Здоровье | Урон |
|-----|----------|-------|----------|------|
"""
    for b in BRAWLERS:
        md += f"| {b['name']} | {b['rarity']} | {b['class']} | {b['health']} | {b['damage']} |\n"

    md += "\n## 🎮 Режимы игры\n"
    for mode in GAME_MODES:
        md += f"- {mode}\n"

    md += "\n## 📰 Последние новости\n"
    for news in NEWS:
        md += f"### {news['date']} – {news['title']}\n{news['content']}\n\n"

    md += """
## 🔗 Полезные ссылки
- [Официальный сайт Brawl Stars](https://brawlstars.com)
- [Вики Fandom](https://brawlstars.fandom.com)
- [Поддержка Supercell](https://support.supercell.com)

---
*Скрипт автоматического сбора информации. Данные обновляются при каждом запуске.*
"""
    with open('docs/INFO.md', 'w', encoding='utf-8') as f:
        f.write(md)
    print("✓ Сгенерирован отчёт (docs/INFO.md)")

def generate_readme():
    """Создаёт основной README для репозитория GitHub"""
    readme = f"""# 🏆 Brawl Stars Info Repository

Этот репозиторий содержит автоматически собранную информацию об игре **Brawl Stars**.

## 📁 Структура
- `data/` – JSON/текстовые файлы с данными (бойцы, новости, режимы)
- `docs/` – сгенерированные отчёты в Markdown
- `brawl_stars_info.py` – основной скрипт сбора информации

## 🚀 Как обновить данные
```bash
python brawl_stars_info.py
