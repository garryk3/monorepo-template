## Базовая структура каталога компонента react(preact)

- **index.ts** - (точка входа в компонент) - реэкспортирует необходимые файлы, извне допускается импорт только из этого файла
- **components/**- каталог для расположения файлов - частей основного компонента при его декомпозиции (опционален, может быть заменен на отдельный файл с компонентом при небольшом размере)
- **hooks/** - каталог для хуков, если в компоненте более одного, иначе хуки могут располагаться к корне компонента
- __tests__/ - каталог для тестов
- **[ReactComponent].tsx** - файл компонента, при наличии каталога **components** располагается в нем, иначе в корне компонента. (название соответствует названию каталога компонента: *pages/test_component -> TestComponent.tsx*)
- **selectors.ts** - файл с селекторами
- **adapters.ts** - файл с адаптерами данных
- **helpers.ts** - файл со вспомогательными утилитами
- **types.ts** - файл с интерфейсами
- **constants.ts** - константные переменные компонента
- **styles.ts** - css стили, styled-components
- **validationSchema.ts** - схемы валидации для форм (yup, zod)

Обязательно наличие файлов index.ts, [ReactComponent].tsx - остальные файлы и каталоги опциональны, зависят от сложности компонента.