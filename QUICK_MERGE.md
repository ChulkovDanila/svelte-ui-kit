# ⚡ Быстрый Merge Pull Request

## 🎯 Самый быстрый способ (3 клика!)

1. Откройте Pull Request на GitHub
2. Нажмите **"Merge pull request"** внизу страницы
3. Нажмите **"Confirm merge"**

**Готово!** PR объединён за 10 секунд! 🚀

---

## 🤖 Автоматические способы

### Вариант 1: Добавить метку

1. Откройте PR
2. Добавьте метку **"merge"** или **"auto-merge"**
3. Workflow автоматически объединит PR!

### Вариант 2: Автоматический merge при открытии

Workflow `.github/workflows/auto-merge.yml` автоматически объединяет PR при открытии (если нет конфликтов).

---

## ⚙️ Настройка для ещё более быстрого merge

### Отключить требование ревью:

1. **Settings** → **Branches**
2. Найдите правило для ветки `main`
3. Снимите галочку **"Require pull request reviews before merging"**
4. Сохраните

Теперь можно merge без ожидания ревью!

---

## 📝 Команды в комментариях

В комментарии PR напишите:
- `/merge` - объединить PR
- `/squash` - объединить с squash
- `/rebase` - объединить с rebase

---

## ✅ Что создано:

- ✅ `.github/workflows/auto-merge.yml` - автоматический merge
- ✅ `.github/workflows/merge-on-label.yml` - merge по метке
- ✅ `AUTO_MERGE_SETUP.md` - подробная инструкция

---

**Теперь merge PR занимает всего несколько секунд!** ⚡

