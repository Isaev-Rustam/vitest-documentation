# Используй плагин ESLint для библиотеки тестирования
Если ты хочешь избежать некоторых распространенных ошибок, то официальные плагины ESLint могут сильно тебе в этом помочь:

- eslint-plugin-testing-library
- eslint-plugin-jest-dom

# Установка и базовая настройка
`yarn add -D vitest`
Для установки требуется `vite`
## Настройка base
Есть два способа настройки vitest:
- через vite.config.ts
- через vitest.config.ts

_В данном проекте мы рассмотрим только второй способ_
### vitest.config.ts
Создаем файл `vitest.config.ts` со следующим содержимым
```typescript
import { mergeConfig } from 'vite'
import { defineConfig } from 'vitest/config'
import viteConfig from './vite.config'

export default mergeConfig(viteConfig, defineConfig({
  test: {
  },
}))
```

## Запуск
- Для запуска тестов используется команда `yarn vitest`
- Для запуска проверки покрытия используется команда `yarn vitest run --coverage`

_Для работы функции coverage необходимо дополнительно установить:
`yarn add -D @vitest/coverage-c8'`_


## Настройка React
1. `yarn add -D jsdom` устанавливаем jsdom для доступа к html в vitest
2. Добавляем в настройку vite или vitest jsdom в качестве окружения
```js
test: {
    environment: 'jsdom',
},
```
3. `yarn add -D @testing-library/react @testing-library/jest-dom` подключаем саму библиотеку `React Testing Library`
4. `yarn add -D @testing-library/user-event` добавляем библиотеку, чтобы имитировать действия пользователей
5. Создаем файл setup, чтобы не писать настройки для каждого файла отдельно со следующим содержимым:
```js
//setup.js
import { expect, afterEach } from 'vitest';
import { cleanup } from '@testing-library/react';
import matchers from '@testing-library/jest-dom/matchers';

// extends Vitest's expect method with methods from react-testing-library
expect.extend(matchers);

// runs a cleanup after each test case (e.g. clearing jsdom)
afterEach(() => {
  cleanup();
});
```
6. Дорабатываем настройки vitest:
```js
  test: {
    globals: true,
    environment: 'jsdom',
    setupFiles: 'setup.js', // Нужно указать весь путь для файла setup.js
  },
```
