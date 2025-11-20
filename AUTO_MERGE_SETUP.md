# Настройка автоматического объединения Pull Request

## 🤖 Автоматический Merge через GitHub Actions

Создан workflow `.github/workflows/auto-merge.yml`, который автоматически объединяет Pull Request при выполнении условий.

## ⚙️ Как это работает

1. Workflow запускается при открытии или обновлении PR
2. Проверяет, что нет конфликтов
3. Автоматически объединяет PR методом "merge"

## 📋 Требования для автоматического merge

- ✅ PR должен быть без конфликтов
- ✅ Все проверки должны пройти (если настроены)
- ✅ Workflow должен иметь права на запись

## 🚀 Быстрый Merge вручную

### Способ 1: Через веб-интерфейс (Самый быстрый!)

1. Откройте Pull Request на GitHub
2. Нажмите кнопку **"Merge pull request"** внизу страницы
3. Выберите метод объединения:
   - **Create a merge commit** - сохраняет историю
   - **Squash and merge** - объединяет в один коммит
   - **Rebase and merge** - применяет поверх основной ветки
4. Нажмите **"Confirm merge"**

### Способ 2: Через метку (Label) - Автоматически!

1. Откройте Pull Request
2. Добавьте метку **"merge"** или **"auto-merge"**
3. Workflow автоматически объединит PR!

### Способ 3: Через комментарий в PR

Напишите в комментарии PR:
```
/merge
```

Или с указанием метода:
```
/merge squash
/merge rebase
```

### Способ 4: Через GitHub Actions (вручную)

1. Перейдите в **Actions** → **Auto-merge Pull Request**
2. Нажмите **"Run workflow"**
3. Введите номер PR
4. Нажмите **"Run workflow"**

## ⚙️ Настройка репозитория для быстрого merge

### Отключить требование ревью

1. Перейдите в **Settings** репозитория
2. Выберите **Branches** в меню слева
3. Найдите правило для вашей ветки (например, `main`)
4. Снимите галочку **"Require pull request reviews before merging"**
5. Сохраните изменения

### Включить авто-merge

1. В настройках ветки включите **"Allow auto-merge"**
2. PR будет объединён автоматически после прохождения всех проверок

## 🔧 Настройка workflow

Если нужно изменить метод объединения, отредактируйте файл `.github/workflows/auto-merge.yml`:

```yaml
merge_method: 'merge'  # или 'squash', 'rebase'
```

## 📝 Важные замечания

- Автоматический merge работает только если нет конфликтов
- Workflow требует прав на запись в репозиторий
- Некоторые настройки репозитория могут блокировать автоматический merge

## 🛠️ Устранение проблем

### Workflow не объединяет PR

1. Проверьте права workflow в настройках репозитория
2. Убедитесь, что нет конфликтов
3. Проверьте логи workflow в разделе Actions

### Кнопка "Merge" неактивна

1. Проверьте настройки ветки в Settings → Branches
2. Убедитесь, что все проверки пройдены
3. Разрешите конфликты, если они есть

## 📚 Полезные ссылки

- [GitHub: Merging a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/merging-a-pull-request)
- [GitHub Actions: Permissions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#permissions)

