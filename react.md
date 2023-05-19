# Тестирование React
- [article - use](https://www.robinwieruch.de/react-testing-library/)
- [примеры тестирования компонентов](https://www.robinwieruch.de/react-testing-library/](https://github.com/nareshbhatia/react-testing-techniques/tree/main/docs))
- [article - pattern](https://frontend-stuff.com/blog/common-mistakes-with-react-testing-library/)
- [youtube](https://www.youtube.com/watch?v=T2sv8jXoP4s&list=PLC3y8-rFHvwirqe1KHFCHJ0RqNuN61SJd&index=1)
- [youtube](https://www.youtube.com/watch?v=7dTTFW7yACQ&list=PL4cUxeGkcC9gm4_-5UsNmLqMosM-dzuvQ&index=1)
- [role getByRole](https://www.w3.org/TR/html-aria/#toc) [role](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/textbox_role)
- [act](https://davidwcai.medium.com/react-testing-library-and-the-not-wrapped-in-act-errors-491a5629193b) [waitFor](https://testing-library.com/docs/guide-disappearance/)

Тестирование React будем проводить с помощью `React Testing Library`

## Возможности _**Testing Library**_

- render() -принимает любой JSX в качестве аргумента, чтобы отобразить его в качестве вывода. После чего появиться доступ к компоненту react.
- screen. -screen объект предоставляет доступ к document.body.
- toBeInTheDocument() -проверяет есть элемент в теле документа или нет.
- toHaveStyle() -проверяет есть ли стили.
- toBeRequired() -проверяет обязательно ли поле для ввода


## Существуют другие типы поиска, которые в большей степени зависят от элемента:
- `LabelText` - getByLabelText: <label for="search" />
- `PlaceholderText` - getByPlaceholderText: <input placeholder="Search" />
- `AltText` - getByAltText: <img alt="profile" />
- `DisplayValue` - getByDisplayValue: <input value="JavaScript" />

В чем разница между GetBy и queryBy?
GetBy возвращает элемент или ошибку. Удобным побочным эффектом GetBy является то, что он возвращает ошибку,
поскольку он гарантирует, что мы, разработчики, как можно раньше заметим, что в нашем тесте что-то не так.
Однако это затрудняет проверку элементов, которых там не должно быть.


* getAllBy
* queryAllBy
* findAllBy

expect(screen.getByText(/Searches for JavaScript/)).toBeNull();
- GetBy Ожидает что элемент должен быть найден если это не так test упадает.

expect(screen.queryByText(/Searches for JavaScript/)).toBeNull();
- queryBy позволяет убедиться что элемента нет. Т.е мы ищем элемент, и явно говорим что он отсутствует. Доказательство, что элемент отсутствует.
  
expect(await screen.findByText(/Signed in as/)).toBeInTheDocument();
- Вариант поиска findBy используется для асинхронных элементов, которые в конечном итоге будут там. Сам метод findByText возвращает promise.

- getByTestId('custom-element') <div data-testid="custom-element" />

## События: fireEvent abd UserEvent 

Функция fireEvent принимает элемент (здесь поле ввода по роли текстового поля) и событие (здесь событие, имеющее значение "JavaScript").
Выходные данные функции отладки должны отображать структуру HTML до и после события; и вы должны увидеть, новое значение поля ввода.

UserEvent - API имитирует фактическое поведение браузера более точно, чем fireEvent API.
Например, a fireEvent.change() запускает только change событие единожды, тогда как userEvent.type запускает change событие, на каждое keyDown,
keyPress и keyUp события.
Все методы UserEvent являются синхронными, за одним исключением: когда delay опция используется с userEvent.type


- waitFor Функция RTL возвращает обещание, которое выполняется либо при выполнении заданного логического условия, либо по истечении времени ожидания операции. Для этого теста мы будем использовать waitFor функцию, чтобы сообщить RTL, чтобы он ожидал, пока некоторый известный текст из сообщения отобразится на экране.

- act() принимает функцию в качестве своего первого аргумента и вызывает ее для применения к DOM (jsdom). После act() выполнения
функции вы можете создавать утверждения, чтобы это помогло приблизить выполнение тестов к тому, что испытывали бы реальные пользователи.
Тестирование кода вызывающего обновление состояния react должен быть завернут в act() 
