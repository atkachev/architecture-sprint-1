1 и 2 Уровень. 3 уровень не делал.
Легенда: Приложение на данный момент не большое, но в дальнейшем предполагается добавление новых функций и модулей, а
также сверхвысокие нагрузки.
Разбиваем приложение Mesto на микрофронтенды. Используем Вертикальная нарезку.

1. Этап: Предварительный анализ
   Технологии оставим те же React, но если появится необходимость каждый микрофронтенд сможет выбрать нужный ему
   язык/фреймворк.
2. Этап: Определяем бизнес-функции, которыми будут заниматься разные команды:
   Структура микрофонтендов:
    1. User:
        - регистрация пользователя
        - логин/войти в систему
        - редактирование мето информации о пользователе
        - редактирование аватара
    2. Card:
        - отображение списка фотографий
        - загрузка фотографий
        - удаление фотографий
        - сбор и учет лайков под фото

   **Components**
   
   **User:**
   - App.js // Компонент высшего уровня React
   - EditAvatarPopup.js // Редактирование аватара 
   - EditProfilePopup.js // Редактирование профиля пользователя 
   - Header.js // Компонент регистрации/входа 
   - InfoTooltip.js // Компонент результата регистрации 
   - Login.js // Компонент логина 
   - ProtectedRoute.js // Компонент редиректа для гостя 
   - Register.js // Компонент регистрации 

     **Card:**
   - AddPlacePopup.js // Компонент добавления новой карточки. Использует 
   - App.js // Компонент высшего уровня React 
   - Card.js // Компонент карточка 
   - Footer.js // Компонент  
   - ImagePopup.js // Компонент просмотра изображения карточки 
   - Main.js // Компонент список карточек 
   - PopupWithForm.js // Компонент добавление новой карточки. 

3. Этап:
   Методы интеграции микрофронтендов:
   Интегрировать микрофронтенды будем с помощью Run time подхода. Получим преимущества:
    - Развёртывать модули независимо.
    - Динамически обновлять отдельные модули.
    - Сделать масштабирование гибким.

   Методы композиции микрофронтендов:
   Выбираем Гибридная композиция, получаем преимущества, Серверной и Клиенсткой композиций.
   Для реализации прийдется в backend-e добавить слой BFF для каждого микрофронтенда(userBFF, cardBFF)

4. Этап: Инструменты для создания микрофронтендов:
   Будем использовать **Webpack Module Federation**
   Module Federation объединяет разные модули приложения в единое целое и позволяет им использовать общий код.
   В такой композиции есть две роли — хост и удалённый модуль:
    - Хост (host) — это основное приложение. Добавим приложение с именем host.
    - Удалённый модуль (remote) — это отдельный микрофронтенд. В нашем приложени их два: **Card**, **User**
      Конфигурация Module Federation:
    - Чтобы создать микрофронтенды, нужно написать конфигурацию Module Federation для хоста и для каждого удалённого
      модуля.
    - webpack.config.js for User
    - webpack.config.js for Card
    - webpack.config.js for Host
5. Этап: Настройка межмодульного взаимодействия:
   Используем Взаимодействие на основе API. Микрофронтенд общается только со своим микросервисом. Между микрофронтами
   нету прямой связи.   
   <img height="350" src="5-etap.jpg" width="450"/>