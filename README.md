#!/usr/bin/env python3
# brawl_stars_info.py
# Полный автономный скрипт для сбора информации об игре Brawl Stars

import os
import json
import datetime
import sys

# ------ ДАННЫЕ (ИНФОРМАЦИЯ ОБ ИГРЕ) ------
BRAWLERS = [
    {"name": "Спайк", "rarity": "Легендарный", "class": "Снайпер", "health": 2600, "damage": 800},
    {"name": "Кольт", "rarity": "Редкий", "class": "Стрелок", "health": 2800, "damage": 420},
    {"name": "Шелли", "rarity": "Начинающий", "class": "Боец ближнего боя", "health": 3000, "damage": 300},
    {"name": "Бо", "rarity": "Эпический", "class": "Снайпер", "health": 3400, "damage": 520},
    {"name": "Лу", "rarity": "Сверхредкий", "class": "Контроллер", "health": 2600, "damage": 400},
    {"name": "Фанг", "rarity": "Эпический", "class": "Ассасин", "health": 3200, "damage": 450},
    {"name": "Эдгар", "rarity": "Сверхредкий", "class": "Ассасин", "health": 2800, "damage": 360},
    {"name": "Лола", "rarity": "Эпический", "class": "Поддержка", "health": 3100, "damage": 390}
]

NEWS = [
    {"date": "2025-03-10", "title": "Обновление: новый боец Мелоди", "content": "Музыкальный ассасин с особыми способностями."},
    {"date": "2025-02-20", "title": "Киберспортивный сезон 2025", "content": "Старт квалификаций на мировое первенство."},
    {"date": "2025-02-01", "title": "Балансные изменения", "content": "Нерф Лолы и бафф Эдгара."}
]

GAME_MODES = [
    "Баунти", "Кража", "Горячая зона", "Натиск", "Удар чемпионов", "Вышибалы", "Захват кристаллов"
]

# ------ ФУНКЦИИ (НЕ ВИДНЫ СНАРУЖИ, ТОЛЬКО РЕЗУЛЬТАТ) ------
def create_dirs():
    for d in ['data', 'docs']:
        os.makedirs(d, exist_ok=True)

def save_json(filename, data):
    with open(filename, 'w', encoding='utf-8') as f:
        json.dump(data, f, ensure_ascii=False, indent=2)

def save_txt(filename, lines):
    with open(filename, 'w', encoding='utf-8') as f:
        for line in lines:
            f.write(f"{line}\n")

def generate_info_md():
    md = f"""# 📊 Brawl Stars — информация об игре

**Актуально на:** {datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")}

## 🥊 Бойцы ({len(BRAWLERS)})
| Имя | Редкость | Класс | HP | Урон |
|-----|----------|-------|----|------|
"""
    for b in BRAWLERS:
        md += f"| {b['name']} | {b['rarity']} | {b['class']} | {b['health']} | {b['damage']} |\n"

    md += "\n## 🎮 Режимы игры\n" + "\n".join(f"- {m}" for m in GAME_MODES)
    md += "\n\n## 📰 Новости\n"
    for n in NEWS:
        md += f"**{n['date']}** — {n['title']}\n{n['content']}\n\n"
    return md

def generate_readme():
    return f"""# 🏆 Brawl Stars Info Repository

Автоматическая сборка информации об игре Brawl Stars.

## Данные в репозитории
- `data/brawlers.json` — все бойцы
- `data/news.json` — новости игры
- `data/game_modes.txt` — режимы
- `docs/INFO.md` — читаемый отчёт

## Запуск обновления
```bash
python brawl_stars_info.py
