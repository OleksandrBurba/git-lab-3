# NOTES-l3

## Варіант
Номер варіанта 6, прізвище латиницею burba (Бурба Олександр, З-41).
Працюю з файлом STATUS.md у гілці lab3/variant-6-burba, тег v0.1-burba.

## 1. stash list
```
stash@{0}: On lab3/variant-6-burba: чернетка статусу v6
```
Прапор -u додав у схованку ще не відстежуваний draft-v6.txt, а -m дав запису нормальну назву. Після git stash pop запис пропав зі списку, а обидва файли я потім закомітив.

## 2. cherry-pick
```
feature/pick-6: b467029
lab3/variant-6-burba: 4725c3f
```
Зміни ті самі, але коміт новий: у нього інший батько і час створення, тому і хеш інший.

## 3. reflog
```
32d5a6f HEAD@{0}: commit (amend): Уточнити статус, варіант 6
4725c3f HEAD@{1}: cherry-pick: Оновити статус роботи
288137e HEAD@{2}: checkout: moving from feature/pick-6 to lab3/variant-6-burba
b467029 HEAD@{3}: commit: Оновити статус роботи
288137e HEAD@{4}: checkout: moving from lab3/variant-6-burba to feature/pick-6
```
У першому рядку коміт після amend, у другому старий хеш 4725c3f. Гілка на той момент ще не була запушена, тому amend був безпечний.

## 4. revert
```
c948f3d Revert "Зіпсувати рядок"
1fbea2b Зіпсувати рядок
32d5a6f Уточнити статус, варіант 6
288137e Закомітити чернетку після stash
f3a18e1 Додати STATUS.md для варіанта 6
f3de31d Initial commit
```
Поганий коміт уже лежав на GitHub, тому я не переписував історію, а додав зверху Revert. Обидва коміти видно в log.

## 5. тег
```
tag v0.1-burba
Tagger: Бурба Олександр <oleksandrburba15@gmail.com>
Date:   Tue Nov 17 18:16:19 2026 +0200

Перший зріз варіанта 6

commit c948f3d05b42c6ae3115004e2f97997aa0e4f714
Author: Бурба Олександр <oleksandrburba15@gmail.com>
Date:   Tue Nov 17 18:11:31 2026 +0200

    Revert "Зіпсувати рядок"
    
    This reverts commit 1fbea2bbdd3aa060c25090a880a4826e08081931.
```
Тег анотований, тому в ньому зберігся автор (Tagger), дата і повідомлення. З detached HEAD вийшов через гілку recover/v6.

## 6. rebase -i
```
було:
pick ca1403c WIP: чернетка
pick 623073a fix typo
стало:
pick ca1403c WIP: чернетка
squash 623073a fix typo
```
Результат: a334574 Оновити статус роботи
Чернетку і виправлення помилки склав в один коміт. Пушив тільки в свою гілку і тільки з --force-with-lease.

## 7. blame
```
f3a18e16 (Бурба Олександр 2026-11-17 17:48:36 +0200 3) Бурба Олександр, З-41, варіант 6
```
По blame видно, який коміт і коли останнім змінив рядок.

## 8. fork
origin - моя копія репозиторію на GitHub, туди я пушу.
upstream - репозиторій, від якого зроблено fork.
Щоб забрати свіжі зміни, роблю git fetch upstream і переношу їх у свою гілку.
Свою гілку пушу в origin, а Pull Request створюю в upstream/main.
