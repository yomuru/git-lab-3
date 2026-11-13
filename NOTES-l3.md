# NOTES-l3 — Практична робота №3

## Варіант
Журнал 37, 37 mod 10 = 7, варіант 7. Прізвище: Shvets (Швець Даніїл, група З-41).
Файл варіанта — NOTES.md, гілка здачі — lab3/variant-7-shvets, тег — v0.1-shvets.

## 1. stash list
```
stash@{0}: On lab3/variant-7-shvets: чернетка нотатки v7
```
Завдяки -u у stash потрапив і новий файл draft-v7.txt, а -m дало зрозумілу назву замість WIP on. Після pop запис зник зі списку, а draft-v7.txt я закомітив.

## 2. cherry-pick
```
feature/pick-7: a936d65 Додати пояснення гілки
lab3/variant-7-shvets: cfb9d83 Додати пояснення гілки
```
Хеші різні (a936d65 і cfb9d83), бо cherry-pick створює новий коміт з тим самим патчем, але з іншим батьком і часом. Пізніше цей коміт ще змінив amend, тому на гілці зараз інший хеш.

## 3. reflog
```
c4b07a7 HEAD@{0}: commit (amend): Уточнити пояснення гілки, варіант 7
cfb9d83 HEAD@{1}: cherry-pick: Додати пояснення гілки
c3d3449 HEAD@{2}: checkout: moving from feature/pick-7 to lab3/variant-7-shvets
a936d65 HEAD@{3}: commit: Додати пояснення гілки
c3d3449 HEAD@{4}: checkout: moving from lab3/variant-7-shvets to feature/pick-7
```
Зверху новий коміт після amend, нижче — старий хеш від cherry-pick. Amend я зробив до push, тому на origin старого коміту не було.

## 4. revert
```
ad0b8ca Revert "Зіпсувати рядок"
dec720e Зіпсувати рядок
c4b07a7 Уточнити пояснення гілки, варіант 7
c3d3449 Додати чернетку варіанта 7
ff49d7a Створити файл варіанта NOTES.md
c4b9aaf Initial commit
```
У історії лишились обидва коміти: «Зіпсувати рядок» і Revert. Гілка вже була на GitHub, тому помилку скасовано новим комітом, а не reset.

## 5. тег
```
tag v0.1-shvets
Tagger: Швець Даніїл <shaderr6s@gmail.com>
Date:   Fri Nov 13 18:26:35 2026 +0200

Перший зріз варіанта 7

commit ad0b8ca17e7ec37d6ca4eaf96a15ff9835c01c0b
Author: Швець Даніїл <shaderr6s@gmail.com>
Date:   Fri Nov 13 18:24:00 2026 +0200

    Revert "Зіпсувати рядок"
    
    This reverts commit dec720e5515c509a859474d33e5a69a13d320e30.
```
Тег анотований (-a), тому в ньому є Tagger, дата і повідомлення. Після git switch --detach я вийшов гілкою recover/v7, без комітів у detached HEAD.

## 6. rebase -i
```
до:
pick 2d1b0a1 WIP: чернетка
pick b5966d3 fix typo
після:
pick 2d1b0a1 WIP: чернетка
squash b5966d3 fix typo
```
Підсумковий коміт: 604c667 Пояснити особисту гілку
Два коміти «WIP: чернетка» і «fix typo» зібрано в один. Після переписування історії гілку запушено лише з --force-with-lease і лише на свою гілку.

## 7. blame
```
c3d3449f (Швець Даніїл 2026-11-13 18:08:09 +0200 4) Чернетка: перевірити, що потрапляє у stash.
```
blame показує, яким комітом і ким останній раз змінено кожен рядок файлу.

## 8. fork
origin — це мій fork на GitHub, куди я маю право push.
upstream — оригінальний репозиторій, з якого зроблено fork.
Нові зміни оригіналу забираю через git fetch upstream і переношу у свою гілку.
Свою гілку пушу в origin, а Pull Request відкриваю в upstream/main.
