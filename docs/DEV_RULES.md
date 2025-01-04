## Использование сторонних uikit-ов

Необходимо избегать (по возможности) прямого использования сторонних компонентов вне презентационного слоя  (каталога src/ui), только через компоненты-обертки, созданные в каталоге src/ui

## Export и import

* На уровне компонентов доступ к объектам осуществляется исключительно через именной импорт через index-файлы, которые реэкспортируют ТОЛЬКО
  **нужные**
  сущности;
* Как следствие, не допускается дефолтный экспорт за исключением компонентов типа pages из-за особенностей react;
* Неэкспортируемые компоненты считаются приватными и прямой доступ к ним запрещен.

## Работа с enum

* могут находиться в файлах с константами, если содержат константные значения
* не должны находиться в файлах с типами - types.ts
* именование: название enum c большой буквы, его члены uppercase-ом

## Использование цветов

Цветовая палитра находится в css переменных, определенных в infrastructure/theme. Использование цветов без переменных допускается, если они не относятся к цветовым токенам используемого ui-кита.

## Работа со styled-components

Компоненты styled-components помещаются в отдельный файл styles.ts внутри каждого модуля.

## Работа с константами

Константные переменные уровня приложения располагаются в директории **src/infrastructure/constants**

Наименование файлов констант -

* keys (константы, используемые в качестве ключей)
* strings (строковые константы, используемые в качестве заменителей текста)
* params (константы, являющиеся параметрами)

При необходимости можно сгруппировать связанные друг с другом по определенной логике константы в отдельном файле с 'говорящим' названием

## Работа с typescript

Использование type assertion

* Допустимо, если стоимость исправления интерфейса достаточно высокая, то можно использовать для информирования компилятора о корректном типе
* Допустимо, если компилятор не может корректно определить нужный тип, несмотря на то, что в коде имеются проверки
* Допустимо для типизации глобальных переменных и событий javascript
* Недопустимо во всех остальных случаях

Игнорирование предупреждений компилятора

* допустимо в крайних случаях (когда не получается по срокам задачи исправить сложную ошибку типов) с комментарием вида //@TODO исправить
* допустимо при необходимости использования any (когда это использование оправдано)
* в остальных случаях - недопустимо

## Наименование файлов и каталогов

Каталоги именуются с маленькой буквы по английски. Несколько слов разделяются нижним подчеркиванием.

Файлы, содержащие UI (react) компоненты используют UpperCamelCase. Все остальные camelCase.

Примеры:

- *src/ui/informer/Informer.tsx*
- *src/ui/informer/constants.ts*
- *src/ui/informer/exampleConstants.ts**
- *src/ui/informer/index.ts
- src/ui/informer/CustormInformer.tsx
- src/ui/informer_dark/InformerDark.tsx


## Тестирование

### Unit-тесты

Для написания тестов используется [react-testing-library](https://testing-library.com/docs/queries/about), [react-hooks](https://react-hooks-testing-library.com/installation#getting-started)

В качестве тест-раннера - [vitest](https://vitest.dev/guide/https://jestjs.io/ru)

#### Структура файлов

* Файлы с тестами располагаются в директории тестируемого компонента в каталоге __tests__
* На каждый тестируемый файл создается отдельный файл с тестами с названием "<имя файла>.test.{js,ts,tsx}"
* Допускается создавать один общий файл с тестами для нескольких файлов в рамках модуля, если количество тестов небольшое
* конфиги настроек тест раннера располагаются в пакете packages/configs, и подключаются отдельно в каждый проект

#### Правила написания тестов

* Файл с тестами должен содержать, как минимум, один вызов функции describe, 1м аргументом в которую передаются строка, содержащая название тестируемого файла и каталога его расположения в формате - в квадратных скобках [directory/fileName]
* Внутри функции describe содержатся вызовы функций it, содержащих тесты, с описанием теста
* Один тест должен содержать тест определенной бизнес-логики, не допускается в рамках одного теста проверять разный функционал
* При тестировании сложной бизнес-логики, которая может быть непонятна, необходимо описать тест кейсы в начале файла в формате jsDoc
* Data-атрибут для упрощения поиска в тестах нужных dom-элементов носит название data-testid, его значение именуется по БЭМ-методологии - ДИРЕКТОРИЯ__КОМПОНЕНТ_ЧАСТЬ

> **Не допускаются pull-request-ы в релизную ветку с неработающими тестами или ошибками линтинга!!!**