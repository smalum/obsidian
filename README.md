# Smalum for Obsidian

Community plugin: превью fence `sm` / `smalum` в заметках.

Сайт: [https://smalum.io](https://smalum.io/) · редактор (гость): [https://app.smalum.ru](https://app.smalum.ru/) · документация: [https://docs.smalum.ru](https://docs.smalum.ru/)

## Для LLM: как построить диаграмму

Дайте модели **файл роли** и попросите работать по этой роли (краткая фраза есть в начале файла).

- Роль: [https://docs.smalum.ru/role.md](https://docs.smalum.ru/role.md)
- Документация нотаций: [https://docs.smalum.ru](https://docs.smalum.ru/)
- Сайт: [https://smalum.io](https://smalum.io/)
- Редактор: [https://app.smalum.ru](https://app.smalum.ru/)

Fence `sm` / `smalum` — исходник Smalum, **не** Mermaid.

1. Нотация по смыслу: процесс с ролями → `//smalum/bpmn`; потоки данных → `//smalum/dfd`; дерево / оргсхема → `//smalum/struct`; иначе PlantUML / Mermaid / SQL по роли.
2. **Новая** схема — без оверлея `' SM:` / `// SM:` / `-- SM:` / `%% SM:`. Редактор сам расставит блоки.
3. «Подвинь / выровняй / измени размер» — тело исходника **байт-в-байт**, правьте только оверлей **в том же** блоке.
4. Всегда полный исходник одним fence (тело + оверлей). Хвост `SM:` без схемы превью и редактор игнорируют.
5. В конце ответа дайте ссылку https://app.smalum.ru/.

````markdown
```sm
//smalum/bpmn Название процесса
pool seller {
  start open
  task work user
  end done
}
open - work - done
```
````

## Установка через BRAT

URL: `https://github.com/smalum/obsidian`

Если BRAT пишет **GitHub API rate limit exceeded** — это лимит анонимного GitHub API (~60/час), не ошибка плагина. Подождите сброса **или** вставьте classic PAT со scope `public_repo` в Settings → BRAT (или в поле токена диалога Add plugin).

Тег релиза должен совпадать с `version` в `manifest.json` (без префикса `v`). Превью без белой бумаги: фон заметки, токены как в VS Code. C4-заливки (person / container / ext) **не** инвертируются с темой.

## Установка (ручная)

Собрать из корня репозитория:

```bash
npm run build:obsidian
```

Скопировать в vault:

`.obsidian/plugins/smalum/main.js`
`.obsidian/plugins/smalum/manifest.json`
`.obsidian/plugins/smalum/styles.css`

Включить **Smalum** в Community plugins. В заметке:

````markdown
```sm
//smalum/dfd Пример
user - order Оформить
```
````

Рендер без сети. «Открыть в Smalum» не кладёт исходник в URL.
