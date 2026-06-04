# 🏗 Архитектура проекта

## Общая схема

```
┌─────────────────────────────────────────────┐
│                  FRONTEND                   │
│  SPA: карточки, колоды, режим изучения      │
└──────────────────┬──────────────────────────┘
                   │ REST API / JSON
┌──────────────────▼──────────────────────────┐
│                  BACKEND                    │
│  Node.js + Express                          │
│  Auth → Decks → Cards → Stats               │
└──────────────────┬──────────────────────────┘
                   │
┌──────────────────▼──────────────────────────┐
│                DATABASE                     │
│  SQLite (dev) │ PostgreSQL (prod)            │
└─────────────────────────────────────────────┘
```

## Основные сущности

### Card (Карточка)
- id, question, answer
- category, tags, difficulty
- deck_id (FK), author_id (FK)
- created_at, updated_at

### Deck (Колода)
- id, name, description
- author_id (FK)
- is_public, tags
- card_count, likes_count
- created_at, updated_at

### User (Пользователь)
- id, username, email
- avatar_url, bio
- created_at

### StudySession (Сессия изучения)
- id, user_id (FK), deck_id (FK)
- cards_reviewed, correct_answers
- duration_seconds
- created_at

## Режимы изучения

1. **Flip** — классические flip-карточки, отмечаешь знал/не знал
2. **Quiz** — выбор из 4 вариантов (AI-генерируемые дистракторы)
3. **Write** — вводишь ответ вручную
4. **SRS** — интервальное повторение (алгоритм SM-2)
