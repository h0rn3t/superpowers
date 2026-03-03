# Суперпотужності для Codex

Посібник з використання Superpowers з OpenAI Codex через вбудовану систему розпізнавання навичок.

## Швидке встановлення

Скажіть Codex:

```
Fetch and follow instructions from https://raw.githubusercontent.com/obra/superpowers/refs/heads/main/.codex/INSTALL.md
```

## Ручне встановлення

### Передумови

- OpenAI Codex CLI
- Git

### Кроки

1. Клонуйте репозиторій:
   ```bash
   git clone https://github.com/obra/superpowers.git ~/.codex/superpowers
   ```

2. Створіть посилання на навички:
   ```bash
   mkdir -p ~/.agents/skills
   ln -s ~/.codex/superpowers/skills ~/.agents/skills/superpowers
   ```

3. Перезавантажте Codex.

### Windows

Використовуйте junction замість посилання (працює без Developer Mode):

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.agents\skills"
cmd /c mklink /J "$env:USERPROFILE\.agents\skills\superpowers" "$env:USERPROFILE\.codex\superpowers\skills"
```

## Як це працює

Codex має вбудовану систему розпізнавання навичок — він сканує `~/.agents/skills/` під час запуску, парсить frontmatter SKILL.md і завантажує навички за потребою. Навички Superpowers стають видимими через одне посилання:

```
~/.agents/skills/superpowers/ → ~/.codex/superpowers/skills/
```

Навичка `using-superpowers` автоматично розпізнається і забезпечує дисциплінований приклад використання навичок — додаткової конфігурації не потрібно.

## Використання

Навички розпізнаються автоматично. Codex активує їх, коли:
- Ви згадуєте навичку за назвою (наприклад, "use brainstorming")
- Завдання відповідає опису навички
- Навичка `using-superpowers` спрямовує Codex на використання однієї з них

### Особисті навички

Створюйте свої навички в `~/.agents/skills/`:

```bash
mkdir -p ~/.agents/skills/my-skill
```

Створіть `~/.agents/skills/my-skill/SKILL.md`:

```markdown
---
name: my-skill
description: Use when [condition] - [what it does]
---

# My Skill

[Your skill content here]
```

Поле `description` визначає, як Codex вирішує активувати навичку автоматично — напишіть його як чітку умову активації.

## Оновлення

```bash
cd ~/.codex/superpowers && git pull
```

Навички оновлюються миттєво через посилання.

## Видалення

```bash
rm ~/.agents/skills/superpowers
```

**Windows (PowerShell):**
```powershell
Remove-Item "$env:USERPROFILE\.agents\skills\superpowers"
```

За бажанням видаліть клон: `rm -rf ~/.codex/superpowers` (Windows: `Remove-Item -Recurse -Force "$env:USERPROFILE\.codex\superpowers"`).

## Усунення неполадок

### Навички не відображаються

1. Перевірте посилання: `ls -la ~/.agents/skills/superpowers`
2. Перевірте наявність навичок: `ls ~/.codex/superpowers/skills`
3. Перезавантажте Codex — навички розпізнаються під час запуску

### Проблеми з junction в Windows

Junctions зазвичай працюють без спеціальних дозволів. Якщо створення не вдалося, спробуйте запустити PowerShell від імені адміністратора.

## Отримання допомоги

- Повідомляйте про проблеми: https://github.com/obra/superpowers/issues
- Основна документація: https://github.com/obra/superpowers