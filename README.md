### React-приложение поиска книг e-library с помощью Google Books API.

**Внимание:** Google Books API не работает на территории Беларуси. Если вы находитесь в Беларуси, активируйте VPN перед использованием приложения (я использовал Psiphon).

Опубликованный проект на GitHub Pages: [тут](https://sob96.github.io/e-library/).

Для запуска приложения локально:
1. git clone https://github.com/Sob96/e-library.git
2. cd e-library
3. npm install
4. npm start

в `App` хранятся общие стейты, используемые в нескольких компонентах, контекст, через который они передаются, ф-ция fetchBooks, которая используется в компонентах приложения для получения массива данных из Google API Books. В этой же функции реализованы фильтрация и сортировка. Они происходят в реальном времени в отношении книг, которые пришли из Google Books API; фильтрация - в отношении книг, которые уже отрисованы на странице в соответствии с шагом пагинации, сортировка - в отношении всех книг, пришедших по запросу. Также в App происходит отрисовка компонентов приложения и роутинг.

React-приложение поиска книг e-library имеет 3 компонента: `Search`, `Books` и `Book`.

В компоненте `Search` осуществляется отрисовка селектов и формы с инпутом и кнопкой. Тут же происходит валидация, получение данных из инпута и селектов.

В компоненте `Books` осуществляется пагинация, отрисовка книг, пришедших из Google Books API, их количества, анимации загрузки и кнопки "load more".

В компоненте `Book` происходит отрисовка книги, по которой кликнул пользователь. id книги приходит через useParams, после этого отправляется запрос с id для конкретной книги в Google Books API. На время загрузки книги также реализована анимация загрузки.

Обработка ошибок заключается в:
- .catch в fetch
- опциональных цепочках и заглушках img на случай, если какая-то часть данных книги не придет
- Error boundary, которым обернуто все приложение
