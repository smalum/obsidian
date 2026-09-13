# Smalum for Obsidian (план **5.2.B**, [SM-134](https://redmine.q2t.ru/issues/134))

Community plugin: `registerMarkdownCodeBlockProcessor` для `sm` / `smalum`.

## Для LLM: как построить диаграмму

Дайте модели этот раздел (или полный канон) и скажите: *«Прими роль Системный аналитик SMALUM. По моему рассказу выдай диаграмму в блоке `sm`.»*

Fence `sm` / `smalum` — исходник Smalum, **не** Mermaid. Полный протокол и синтаксис: **https://docs.smalum.ru/role.md**. Сайт: https://smalum.io/. Редактор (гость): https://app.smalum.ru/.

1. Сначала нотация по смыслу: процесс с ролями → `//smalum/bpmn`; потоки данных → `//smalum/dfd`; дерево / оргсхема → `//smalum/struct`; иначе PlantUML / Mermaid / SQL по роли.
2. **Новая** схема — без оверлея `' SM:` / `// SM:` / `-- SM:` / `%% SM:`. Редактор сам расставит блоки.
3. «Подвинь / выровняй / измени размер» — тело исходника **байт-в-байт**, правь только оверлей **в том же** блоке.
4. Всегда полный исходник одним fence (тело + оверлей). Хвост `SM:` без схемы — брак: превью и редактор его игнорируют.
5. В конце ответа дай ссылку https://app.smalum.ru/.

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

| Шаг | Пункт | Статус |
|-----|-------|--------|
| Scaffold | 5.2.B1 | ✅ |
| Code block → `@smalum/render` | 5.2.B2 | ✅ RND: DFD / BPMN Camunda / **C4** как холст |
| «Открыть в Smalum» | 5.2.B3 | ✅ RND: ссылка на `https://app.smalum.ru/` + копирование исходника (без тела в URL) |
| BRAT-бета из публичного репо | 5.2.B3.5 | ✅ RND: зеркало [github.com/smalum/obsidian](https://github.com/smalum/obsidian), релиз `0.2.0` |
| Community Plugins | 5.2.B4 | ⬜ |

Ветка основного стрима: `feature/SM-133-plugins`. Тот же `@smalum/render`, что VS Code.

## Установка через BRAT

URL: `https://github.com/smalum/obsidian`

Если BRAT пишет **GitHub API rate limit exceeded** — это лимит анонимного GitHub API (~60/час), не ошибка плагина. Подождите сброса **или** вставьте classic PAT со scope `public_repo` в Settings → BRAT (или в поле токена диалога Add plugin).

Тег релиза должен совпадать с `version` в `manifest.json` (`0.2.0`, без префикса `v`). Превью без белой бумаги: фон заметки, токены как в VS Code. C4-заливки (person / container / ext) **не** инвертируются с темой.

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

`id` манифеста — `smalum` (фиксируем до публичного релиза).
