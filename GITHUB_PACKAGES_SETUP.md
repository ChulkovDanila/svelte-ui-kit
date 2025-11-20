# Настройка публикации в GitHub Packages

## 📝 Как получить GITHUB_TOKEN

### Вариант 1: Personal Access Token (для локальной публикации)

1. Перейдите на GitHub: https://github.com/settings/tokens
2. Нажмите **"Generate new token"** → **"Generate new token (classic)"**
3. Дайте токену имя, например: `svelte-uikit-publish`
4. Выберите срок действия (рекомендуется: `90 days` или `No expiration`)
5. Выберите права (scopes):
   - ✅ `write:packages` - для публикации пакетов
   - ✅ `read:packages` - для чтения пакетов
   - ✅ `delete:packages` - для удаления пакетов (опционально)
6. Нажмите **"Generate token"**
7. **ВАЖНО**: Скопируйте токен сразу! Он больше не будет показан.

### Вариант 2: GITHUB_TOKEN в GitHub Actions (автоматический)

Для GitHub Actions используется автоматический `GITHUB_TOKEN`, который создается автоматически для каждого workflow. Он уже настроен в файле `.github/workflows/publish.yml`.

**Ничего дополнительно настраивать не нужно!** Просто создайте release или запустите workflow вручную.

---

## 🚀 Локальная публикация (вручную)

### Windows PowerShell:

```powershell
# Установите токен как переменную окружения
$env:GITHUB_TOKEN="ваш_токен_здесь"

# Войдите в npm
npm login --registry=https://npm.pkg.github.com --scope=@chulkovdanila

# Опубликуйте пакет
npm publish
```

### Windows CMD:

```cmd
set GITHUB_TOKEN=ваш_токен_здесь
npm login --registry=https://npm.pkg.github.com --scope=@chulkovdanila
npm publish
```

### Linux/Mac:

```bash
export GITHUB_TOKEN="ваш_токен_здесь"
npm login --registry=https://npm.pkg.github.com --scope=@chulkovdanila
npm publish
```

---

## 🤖 Автоматическая публикация через GitHub Actions

### Способ 1: При создании Release

1. Перейдите в ваш репозиторий на GitHub
2. Нажмите **"Releases"** → **"Create a new release"**
3. Укажите версию (например: `v0.0.2`)
4. Заполните описание
5. Нажмите **"Publish release"**
6. GitHub Actions автоматически опубликует пакет!

### Способ 2: Ручной запуск

1. Перейдите в **"Actions"** в вашем репозитории
2. Выберите workflow **"Publish to GitHub Packages"**
3. Нажмите **"Run workflow"**
4. Выберите ветку (обычно `main`)
5. Нажмите **"Run workflow"**

---

## 📦 Установка пакета из GitHub Packages

Пользователи могут установить ваш пакет так:

### 1. Создать `.npmrc` в их проекте:

```
@chulkovdanila:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=ИХ_ТОКЕН
```

### 2. Установить пакет:

```bash
npm install @chulkovdanila/svelte-uikit
```

**Примечание**: Пользователям также нужен GitHub токен с правами `read:packages` для установки пакета.

---

## ✅ Проверка публикации

После публикации проверьте:

1. Перейдите на: https://github.com/ChulkovDanila?tab=packages
2. Должен появиться пакет `@chulkovdanila/svelte-uikit`
3. Или перейдите в репозиторий → **"Packages"** справа

---

## 🔄 Обновление версии

Перед каждой публикацией обновите версию в `package.json`:

```json
{
  "version": "0.0.2"  // увеличите версию
}
```

Или используйте npm команды:

```bash
npm version patch  # 0.0.1 → 0.0.2
npm version minor  # 0.0.1 → 0.1.0
npm version major  # 0.0.1 → 1.0.0
```

---

## 🛠️ Устранение проблем

### Ошибка: "401 Unauthorized"
- Проверьте, что токен правильный
- Убедитесь, что токен имеет права `write:packages`

### Ошибка: "403 Forbidden"
- Проверьте, что имя пакета в `package.json` совпадает с вашим GitHub username/org
- Убедитесь, что репозиторий существует

### Ошибка: "Package already exists"
- Увеличьте версию в `package.json`
- Или удалите старую версию через GitHub UI

---

## 📚 Полезные ссылки

- [GitHub Packages документация](https://docs.github.com/en/packages)
- [npm публикация в GitHub Packages](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-npm-registry)
- [GitHub Actions документация](https://docs.github.com/en/actions)

