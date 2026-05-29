# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install      # install dependencies (required before first run)
npm run dev      # start dev server at http://localhost:5173
npm run build    # production build
npm run lint     # run ESLint
npm run preview  # preview production build
```

No test suite is configured.

## Architecture

React 19 + Vite app used as a teaching project. `transactions` state lives in `App` and is passed down to child components.

### Component tree

```
App                          — holds transactions state, passes it to children
├── Summary                  — computes and displays totalIncome, totalExpenses, balance
├── TransactionForm          — owns its own form fields state; calls onAdd(transaction) on submit
└── TransactionList          — owns its own filter state; receives transactions as prop
```

### Data flow
- `App` passes `transactions` to `Summary` and `TransactionList`, and `onAdd` to `TransactionForm`.
- `TransactionForm` converts `amount` to a `Number` before calling `onAdd`, so amounts are always stored as numbers.
- `categories` is a fixed constant array defined locally in both `TransactionForm` and `TransactionList`: `["food", "housing", "utilities", "transport", "entertainment", "salary", "other"]`.

### State shape
Each transaction: `{ id, description, amount (number), type ("income"|"expense"), category, date }`.
