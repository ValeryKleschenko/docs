# Содержание

* <a href="#Архитектура-северной-части">Архитектура серверной части</a>
* <a href="#Описание-таблиц-БД">Описание таблиц БД</a>
    + <a href="#1-basemixin---абстрактный-класс-примесь">BaseMixin</a>
        - <a href="#Поля">Поля</a>
        - <a href="#">Связи с другими таблицами</a>
    + <a href="#2-user---Пользователи">User - Пользователи</a>
        - <a href="#Поля-2">Поля</a>
        - <a href="#">Связи с другими таблицами</a>
    + <a href="#3-userfavouritestore---Избранные-магазины-пользователя">UserFavouriteStore - Избранные магазины пользователя</a>
        - <a href="#Поля-3">Поля</a>
        - <a href="#">Связи с другими таблицами</a>
    + <a href="#4-role---Роли-пользователей">Role - Роли пользователей</a>
        - <a href="#Поля-4">Поля</a>
        - <a href="#">Связи с другими таблицами</a>
    + <a href="#5-group---Группы-пользователей">Group - Группы пользователей</a>
        - <a href="#Поля-5">Поля</a>
        - <a href="#">Связи с другими таблицами</a>
    + <a href="#6-corporation---Сеть-Магазинов-информация-о-ЮрЛице">Corporation - Сеть Магазинов, информация о Юр.Лице</a>
        - <a href="#Поля-6">Поля</a>
        - <a href="#">Связи с другими таблицами</a>
    + <a href="#7-store---Магазины">Store - Магазины</a>
        - <a href="#Поля-7">Поля</a>
        - <a href="#">Связи с другими таблицами</a>
    + <a href="#8-offer---Предложения">Offer - Предложения</a>
        - <a href="#Поля-8">Поля</a>
        - <a href="#">Связи с другими таблицами</a>
    + <a href="#9-shoppinglist---Списки-покупок">ShoppingList - Списки покупок</a>
        - <a href="#Поля-9">Поля</a>
        - <a href="#">Связи с другими таблицами</a>
    + <a href="#10-shoppinglistitem---Элементы-в-списках-покупок">ShoppingListItem - Элементы в списках покупок</a>
        - <a href="#Поля-10">Поля</a>
        - <a href="#">Связи с другими таблицами</a>

* <a href="#rest-api-myconomycom">Спецификация REST API</a>
    + <a href="#summary">Summary</a>
        - <a href="#quick-reference">Quick Reference</a>
            * <a href="#objects">Objects</a>
            * <a href="#users">Users</a>
            * <a href="#roles">Roles</a>
            * <a href="#groups">Groups</a>
            * <a href="#files">Files</a>
        - <a href="#request-format">Request Format</a>
        - <a href="#response-format">Response Format</a>
    + <a href="#">Objects</a>
        - <a href="#object-format">Object Format</a>
        - <a href="#creating-objects">Creating Objects</a>
        - <a href="#retrieving-objects">Retrieving Objects</a>
        - <a href="#updating-objects">Updating Objects</a>
        - <a href="#deleting-objects">Deleting Objects</a>
        - <a href="#data-types">Data Types</a>
    + <a href="#">Queries</a>
        - <a href="#basic-queries">Basic Queries</a>
        - <a href="#query-constraints">Query Constraints</a>
            * <a href="#filters">filters</a>
            * <a href="#limit">limit</a>
            * <a href="#offset">offset</a>
            * <a href="#order-by">order by</a>
            * <a href="#single">single</a>
        - <a href="#relational-queries">Relational Queries</a>
        - <a href="#"></a>
    + <a href="#">Users</a>
        - <a href="#signing-up">Signing Up</a>
        - <a href="#logging-in">Logging In</a>
        - <a href="#verifying-emails">Verifying Emails</a>
        - <a href="#requesting-a-password-reset">Requesting A Password Reset</a>
        - <a href="#retrieving-users">Retrieving Users</a>
        - <a href="#updating-users">Updating Users</a>
        - <a href="#querying">Querying</a>
        - <a href="#deleting-users">Deleting Users</a>
        - <a href="#linking-users">Linking Users</a>
        - <a href="#security">Security</a>
    + <a href="#">Roles</a>
        - <a href="#creating-roles">Creating Roles</a>
        - <a href="#retrieving roles">Retrieving Roles</a>
        - <a href="#updating-roles">Updating Roles</a>
        - <a href="#deleting-roles">Deleting Roles</a>
        - <a href="#security">Security</a>
        - <a href="#role-hierarchy">Role Hierarchy</a>
    + <a href="#">Groups</a>
        - <a href="#creating-groups">Creating Groups</a>
        - <a href="#retrieving-groups">Retrieving Groups</a>
        - <a href="#updating-groups">Updating Groups</a>
        - <a href="#deleting-groups">Deleting Groups</a>
        - <a href="#security">Security</a>
        - <a href="#group-hierarchy">Group Hierarchy</a>
    + <a href="#">Files</a>
        - <a href="#uploading-files">Uploading Files</a>
        - <a href="#associating-with-objects">Associating with Objects</a>
        - <a href="#deleting-files">Deleting Files</a>


# Планируемая архитектура северной части
* * *

* язык разработки - python
* фреймворк - Flask
* СУБД - PostgreSQL 9.1 в облаке <a href="https://postgres.heroku.com/databases">Heroku.com</a>
* ORM - SQLAlchemy
* Кеш - Redis в облаке RedisToGo.com
* Очередь заданий - Celery-with-Redis, очередь крутятся в Worker Dyno также в <a href="https://heroku.com">Heroku.com</a>
* Счетчики статистики - MongoDB в облаке MongoLab.com
* Почта (массовые рассылки) - Mailchimp.com
* Почта (единичные письма) - Mandrill.com
* Хранение статики - AWS S3
* Преобразование картинок (создание версий под разные устройства) и прямое сохранение в S3 - Transloadit.com
* Поиск в API и на сайте - elasticsearch.com.
* Храние сессий - пока на клиенте в куках, там дальше может и в Redis перепишем

Весь сервер разделен на 4 отдельных приложения:

* Приложение - админка для сотрудников myconomy

	* название приложения - <code>**mcnmadmin**</code>
	* url адрес <code>**admin.myconomy.ru**</code> или <code>**mcnmadmin.herokuapp.com**</code>

* Приложение реализующее REST API

	* название приложения - <code>**mcnmapi**</code>
	* url адрес <code>**api.myconomy.ru**</code> или <code>**mcnmapi.herokuapp.com**</code>

* Приложение - личный кабинет

	* название приложения - <code>**mcnmpartner**</code>
	* url адрес <code>**partner.myconomy.ru**</code> или <code>**mcnmpartner.herokuapp.com**</code>

* Приложение - сайт для покупателей

	* название приложения - <code>**mcnmsite**</code>
	* url адрес <code>**myconomy.ru**</code> или <code>**mcnmsite.herokuapp.com**</code>

# Тестирование
* * *

**В качестве тестового стенда используется стенд на домене happyfire.ru**

# Описание таблиц БД
* * *

### 1. BaseMixin - абстрактный класс (примесь ко всем таблицам )

####Поля:
    id            - Integer(), primary_key=True # уникальный идентификатор
    created_at     - DateTime, default=datetime.utcnow, nullable=False # дата-время обновления записи
    updated_at     - DateTime, onupdate=datetime.utcnow, default=datetime.utcnow # дата-время добавления записи


### 2. User - Пользователи
Название таблицы: **users**

####Поля:

    username            - String(255), Юзернейм
    first_name          - String(255), Имя
    last_name           - String(255), Фамилия
    email               - String(255), nullable=False, unique=True)
    phone               - String(255), Мобльниый тел.
    password            - String(255), nullable=False), Хеш пароля
    active              - Boolean, default = False, Состояние (False-заблокирован True-активный)
    language            - String(2), default='ru', choices=('en','ru','de','es')
    website             - String(255),
    birthdate           - DateTime, Дата рождения
    about_me            - String(1000), Любая инфа о пользователе

    activatedAt         - DateTime, Дата активации аккаунта
    last_login_time     - DateTime, Дата поледнего входа
    last_login_ip       - String(255), Последний IP адрес с которого заходил пользователь
    current_login_time  - DateTime, Дата начала текущего логина
    current_login_ip    - String(255), Текущий IP пользователя
    login_count         - Integer, Количество логинов пользователя

####Связи с другими таблицами:
    1. настройки пользователя
    settings     - relationship('UserSettings', backref=db.backref('user'))

    2. список всех ролей данного пользователя
    roles        - relationship('Role', secondary=roles_users, backref = db.backref('users_with_this_role'))

    3. список всех групп куда входит этот пользователь ролей
    groups       - relationship('Group', secondary=groups_users, backref = db.backref('users_in_this_group'))

    4. список всех списков покупок у этого пользователя
    lists        - db.relationship('ShoppingList', backref=db.backref('user'))

    5. список всех предложения, созданых пользователем
    offers       - relationship('Offer', backref=db.backref('who_add'))

    6. список всех магазинов, созданых пользователем
    stores       - relationship('Store', backref=db.backref('who_add'))

    7. список всех corporation, созданых пользователем
    corporations - relationship('Corporation', backref=db.backref('who_add'))


### 3. UserFavouriteStore - Избранные магазины пользователя
Название таблицы: **favourite_stores**

####Поля:
    user_id   - Integer(), ForeignKey('users.id')  # id пользователя, кто добавил предложение
    store_id  - Integer(), ForeignKey('stores.id') # id магазина

### 4. Role - Роли пользователей
Название таблицы: **roles**

####Поля:
    name         - String(80), unique=True, Название Роли
    description  - String(1000), Описание Роли

### 5. Group - Группы пользователей
Название таблицы: **groups**

####Поля:
    name         - String(80), unique=True, Название Группы
    description  - String(1000), Описание Группы

### 6. Corporation - Сеть Магазинов, информация о Юр.Лице
Название таблицы: **corporations**

####Поля:
    name        - String(255), unique=True, Название ЮЛ, пример "ОАО Ромашка"
    network     - String(255), unique=True, Название Сети магазинов, пример "Перекресток"
    description - String(1000), Описание ЮЛ
    president   - String(255), Директор
    INN         - String(255), ИНН
    KPP         - String(255), КПП
    Bank        - String(255), Банк
    Account     - String(255), Расчетный счет

### 7. Store - Магазины
Название таблицы: **stores**

####Поля:
    name        - String(255), nullable=False, Название, пример "Перекресток"
    description - String(1000), Описание магазина
    network     - String(255), Название сети, пример "Перекресток", выбирается из списка известных сетей
    city        - String(255), nullable=False, Город, пример "Москва", выбирается из списка известных городов
    region      - String(255), Район города, пример "ЦАО", , выбирается из списка известных районов/округов
    metro       - String(255), Ближайшее метро, пример "Арбатская", выбирается из списка известных станций метро
    address     - String(1000), Адрес, пример "ул. Бутырская, д. 20"
    phone       - String(255), Телефон, пример "+7(495)123-34-45"
    lat         - Float(), широта
    lng         - Float(), долгота
    user_id     - Integer, ForeignKey('users.id'), id пользователя, кто добавил предложение

    delivery    - Boolean, default=False, True - есть доставка, False - нет доставки (по умолчанию)
    onlineonly  - Boolean, default=False, True - только онлайн, False - обычный розничный магаз (по умолчанию)



### 8. Offer - Предложения

Название таблицы: **offers**

####Поля:
    name             - String(255), Название предлоджения, пример "Колбаса Охотничья"
    description      - String(1000), Описание акции
    store_id         - Integer, ForeignKey('stores.id'), id магазина, чье предложение
    price            - Float, стоимость предложения, например "1234.70"
    measure          - Integer, тип едницы товара
    user_id          - Integer, ForeignKey('users.id'), id пользователя, кто добавил предложение
    type             - Integer, тип предложения 0-обычное, 1-спец предложение
    background_color - String(10), цвет фона предложения в интерфейсе (актуально для спец. предложений)
    border_color     - String(10), цвет рамки предложения в интерфейсе (актуально для спец. предложений)
    text_color       - String(10), цвет текста предложения в интерфейсе (актуально для спец. предложений)
    logo             - String(1000), ссылка на лого (актуально для спец. предложений)
    oldprice         - Float, стоимость предложения, например "234.70" (актуально для спец. предложений)
    datefinish       - DateTime, дата-время окончания действия предложения


####Справочники:
	Типы едниц товаров - measure
		0 - за 1шт
		1 - за 1упк
		2 - за 1кг
		3 - за 1л
		4 - за 1пучок

####Связи с другими таблицами:
    items       - relationship('ShoppingListItem', backref=db.backref('offer'))


### 9. ShoppingList - Списки покупок

Название таблицы: **lists**

####Поля:
    name        - String(255)
    description - String(1000)
    user_id     - Integer, ForeignKey('users.id')

####Связи с другими таблицами:
    1. Список всех позиций в этом списке покупок:
    items - relationship('ShoppingListItem', backref=db.backref('list'))

    2. Настройки списка:
    settings - relationship('ShoppingListSettings', backref=db.backref('list'))


### 10. ShoppingListItem - Элементы в списках покупок

Название таблицы: **list_items**

####Поля:
    list_id   - Integer, ForeignKey('lists.id')
    offer_id  - Integer, ForeignKey('offers.id')
    purchased - Boolean, default=False # True - куплено, False - не куплено
    price     - Float # стоимость купленого товара по версии пользователя, например "1234.70"
    confirmed - Boolean # True - цена подтверждена, False - цена не подтверждена


# REST API Myconomy.com
* * *

## Summary

### Quick Reference
All API access is over HTTP, and accessed via <a href="http://myconomy.com/api"><code>http://myconomy.com/api</code></a> domain.
The relative path prefix /v1/ indicates that we are currently using version 1 of the API.

#### <a href="#objects">Objects</a>
* Corporation
* Store
* Offer
* ShoppingList
* ShoppingListItem
* FavoriteStore

<table class="endpoints">
    <tr>
        <th>
            URL
        </th>
        <th>
            HTTP Verb
        </th>
        <th>
            Functionality
        </th>
    </tr>
    <tr>
        <td class="url">
            <code>
                /api/v1/classes/&lt;className&gt;
            </code>
        </td>
        <td>
            POST
        </td>
        <td>
            <a href="#objects-creating">Creating Objects</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/classes/&lt;className&gt;/&lt;objectId&gt;
            </code>
        </td>
        <td>
            GET
        </td>
        <td>
            <a href="#objects-retrieving">Retrieving Objects</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/classes/&lt;className&gt;/&lt;objectId&gt;
            </code>
        </td>
        <td>
            PUT
        </td>
        <td>
            <a href="#objects-updating">Updating Objects</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/classes/&lt;className&gt;
            </code>
        </td>
        <td>
            GET
        </td>
        <td>
            <a href="#queries">Queries</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/classes/&lt;className&gt;/&lt;objectId&gt;
            </code>
        </td>
        <td>
            DELETE
        </td>
        <td>
            <a href="#objects-deleting">Deleting Objects</a>
        </td>
    </tr>
</table>

#### <a href="#users">Users</a>
<table class="endpoints">
    <tr>
        <th>
            URL
        </th>
        <th>
            HTTP Verb
        </th>
        <th>
            Functionality
        </th>
    </tr>
    <tr>
        <td class="url">
            <code>
                /api/v1/users
            </code>
        </td>
        <td>
            POST
        </td>
        <td>
            <a href="#users-signup">Signing Up</a>
            <br />
            <a href="#users-linking">Linking Users</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/login
            </code>
        </td>
        <td>
            GET
        </td>
        <td>
            <a href="#users-login">Logging In</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/users/&lt;objectId&gt;
            </code>
        </td>
        <td>
            GET
        </td>
        <td>
            <a href="#users-retrieving">Retrieving Users</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/users/&lt;objectId&gt;
            </code>
        </td>
        <td>
            PUT
        </td>
        <td>
            <a href="#users-updating">Updating Users</a>
            <br />
            <a href="#users-linking">Linking Users</a>
            <br />
            <a href="#users-email-verification">Verifying Emails</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/users
            </code>
        </td>
        <td>
            GET
        </td>
        <td>
            <a href="#users-querying">Querying Users</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/users/&lt;objectId&gt;
            </code>
        </td>
        <td>
            DELETE
        </td>
        <td>
            <a href="#users-deleting">Deleting Users</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/requestPasswordReset
            </code>
        </td>
        <td>
            POST
        </td>
        <td>
            <a href="#users-password-reset">Requesting A Password Reset</a>
        </td>
    </tr>
</table>

#### <a href="#roles">Roles</a>
<table class="endpoints">
    <tr>
        <th>
            URL
        </th>
        <th>
            HTTP Verb
        </th>
        <th>
            Functionality
        </th>
    </tr>
    <tr>
        <td class="url">
            <code>
                /api/v1/roles
            </code>
        </td>
        <td>
            POST
        </td>
        <td>
            <a href="#----creating-roles">Creating Roles</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/roles/&lt;objectId&gt;
            </code>
        </td>
        <td>
            GET
        </td>
        <td>
            <a href="#roles-retrieving">Retrieving Roles</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/roles/&lt;objectId&gt;
            </code>
        </td>
        <td>
            PUT
        </td>
        <td>
            <a href="#roles-updating">Updating Roles</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/roles
            </code>
        </td>
        <td>
            GET
        </td>
        <td>
            <a href="#roles-querying">Querying Roles</a>
        </td>
    </tr>
    <tr>
        <td>
            <code>
                /api/v1/roles/&lt;objectId&gt;
            </code>
        </td>
        <td>
            DELETE
        </td>
        <td>
            <a href="#roles-deleting">Deleting Roles</a>
        </td>
    </tr>
</table>

#### <a href="#groups">Groups</a>
<table class="endpoints">
    <tr>
        <th>
            URL
        </th>
        <th>
            HTTP Verb
        </th>
        <th>
            Functionality
        </th>
    </tr>
    <tr>
        <td class="url">
          <code>
          /api/v1/groups
          </code>
        </td>
        <td>
            POST
        </td>
        <td>
            <a href="#groups-creating">Creating Groups</a>
        </td>
    </tr>
    <tr>
        <td>
          <code>
          /api/v1/groups/&lt;objectId&gt;
          </code>
        </td>
        <td>
            GET
        </td>
        <td>
            <a href="#groups-retrieving">Retrieving Groups</a>
        </td>
    </tr>
    <tr>
        <td>
          <code>
          /api/v1/groups/&lt;objectId&gt;
          </code>
        </td>
        <td>
            PUT
        </td>
        <td>
            <a href="#groups-updating">Updating Groups</a>
        </td>
    </tr>
    <tr>
        <td>
          <code>
          /api/v1/groups
          </code>
        </td>
        <td>
            GET
        </td>
        <td>
            <a href="#groups-querying">Querying Groups</a>
        </td>
    </tr>
    <tr>
        <td>
	        <code>
	        /api/v1/groups/&lt;objectId&gt;
	        </code>
        </td>
        <td>
            DELETE
        </td>
        <td>
            <a href="#groups-deleting">Deleting Groups</a>
        </td>
    </tr>
</table>

#### <a href="#files">Files</a>
<table class="endpoints">
    <tr>
        <th>
            URL
        </th>
        <th>
            HTTP Verb
        </th>
        <th>
            Functionality
        </th>
    </tr>
    <tr>
        <td class="url">
            <code>
                /api/v1/files/&lt;fileName&gt;
            </code>
        </td>
        <td>
            POST
        </td>
        <td>
            <a href="#files-uploading">Uploading Files</a>
        </td>
    </tr>
</table>

### Request Format
For POST and PUT requests, the request body must be JSON, with the Content-Type header set to <code>***application/json***</code>.


### Response Format
The response format for all requests is a JSON object.

Whether a request succeeded is indicated by the HTTP status code. A 2xx status code indicates success, whereas a 4xx status code indicates failure. When a request fails, the response body is still JSON, but always contains the field message which you can inspect to use for debugging. For example, trying to save an object with invalid keys will return the message:

		HTTP/1.1 400 Bad Request

		{"message": "Multiple results found"}

or

		HTTP/1.1 400 Bad Request

		{"message": "No result found"}

or

		HTTP/1.1 400 Bad Request

		{ "validation_errors":
		    {
		      "age": "Must be an integer",
		    }
		}


## Objects
### Object Format
### Creating Objects
To create a new object on Myconomy REST API, send a POST request to the class URL containing the contents of the object. For example, to create the object described above:

    curl -X POST \
	  -H "Content-Type: application/json" \
	  -d '{"name":"Пятерочка на углу","city":"Москва","metro":"Белорусская", "corporation_id":"2"}' \
	  http://myconomy.com/api/v1/classes/stores

When the creation is successful, the HTTP response is a 201 Created:

	Status: 201 Created

The response body is a JSON object containing the object **id** of the newly-created object:

	{
	  "id": 8
	}

### Retrieving Objects
Once you've created an object, you can retrieve its contents by sending a GET request to the object URL returned in the location header. For example, to retrieve the object we created above:

	curl -X GET \
	  http://myconomy.com/api/v1/classes/stores/8

When the retrieving objects is successful, the HTTP response is a 200 OK:

	Status: 200 OK

The response body is a JSON object containing all the object-provided fields, plus the <code>created_at</code>, <code>updated_at</code>, and <code>id</code> fields:

	{
	  "id": 8,
	  "name": "\u041f\u0435\u0440\u0435\u043a\u0440\u0435\u0441\u0442\u043e\u043a",
	  "description": null,
	  "city": "\u041c\u043e\u0441\u043a\u0432\u0430",
	  "corporation_id": 1,
	  "user_id": 1,
	  "phone": null,
	  "address": null,
	  "metro": null,
	  "region": null,
	  "delivery": false,
	  "onlineonly": false,
	  "lng": null,
	  "lat": null,
	  "updated_at": "2012-08-20T12:16:40.686930",
	  "created_at": "2012-08-20T12:16:40.686916"
	}

	{
	  "id": 8,
	  "email": "mike@myconomy.ru"
	  "username": mike_klinkin,
	  "phone": "+79261234567",
	  "gender": 1,
	  "birthdate": "1984-08-20",
	  "state": 1,

	  "lists": [{...},...],
	  "stores": [{...},...],
	  "groups": [{...},...],
	  "corporations": [{...},...],
	  "roles": [{...},...],
	  "offers": [{...},...],

	  "updated_at": "2012-08-20T12:16:39.997156",
	  "created_at": "2012-08-20T12:16:39.997140",
	  "last_login_time": "2012-08-20T12:16:39.997156"
	}

### Updating Objects

To change the data on an object that already exists, send a PUT request to the object URL. Any keys you don't specify will remain unchanged, so you can update just a subset of the object's data. For example, if we wanted to change the **phone** field of our Store object:

	curl -X PUT \
	  -H "Content-Type: application/json" \
	  -d '{"phone":"+74951234567"}' \
	  http://myconomy.com/api/v1/classes/stores/8

When the updating is successful, the HTTP response is a 201 Created:

	Status: 201 Created

The response body is a JSON object containing all fields of object:

	{
	  "id": 8,
	  "name": "\u041f\u0435\u0440\u0435\u043a\u0440\u0435\u0441\u0442\u043e\u043a",
	  "description": null,
	  "city": "\u041c\u043e\u0441\u043a\u0432\u0430",
	  "corporation_id": 1,
	  "user_id": 1,
	  "phone": "+74951234567",
	  "address": null,
	  "metro": null,
	  "region": null,
	  "delivery": false,
	  "onlineonly": false,
	  "lng": null,
	  "lat": null,
	  "updated_at": "2012-08-20T12:16:40.686930",
	  "created_at": "2012-08-20T12:16:40.686916"
	}

### Deleting Objects
### Data Types

## Queries
### Basic Queries
You can retrieve multiple objects at once by sending a GET request to the class URL. Without any URL parameters, this simply lists objects in the class:

	curl -X GET \
	  http://myconomy.com/api/v1/classes/<className>

	Avaliable <className>:
		- corporations
		- stores
		- offers
		- lists
		- listitems
		- favstores

The return value is a JSON object that contains a results field with a JSON array that lists the objects.
For example output for offers className:

	{
	  "objects": [
	    {
	      "id": 1,
	      "name": "\u041a\u043e\u043b\u0431\u0430\u0441\u0430",
	      "description": "\u043e\u0431\u044b\u0447\u043d\u0430\u044f \u043a\u043e\u043b\u0431\u0430\u0441\u0430 \u043a\u043e\u043f\u0447\u0435\u043d\u043d\u0430\u044f",
	      "type": 1,
	      "measure": 1,
	      "price": 150.78,
	      "user_id": 1,
	      "store_id": 1,
	      "oldprice": null,
	      "color": null,
	      "datefinish": null,
	      "logo": null,
	      "updated_at": "2012-08-23T23:48:40.735655",
	      "created_at": "2012-08-23T23:48:40.735643",
	    },
	    {
	      "id": 2,
	      "name": "\u041c\u0430\u0441\u043b\u043e",
	      "description": "\u0441\u043b\u0438\u0432\u043e\u0447\u043d\u043e\u0435",
	      "type": 0,
	      "measure": 2,
	      "price": 34.2,
	      "user_id": 1,
	      "store_id": 1,
	      "oldprice": null,
	      "color": null,
	      "datefinish": null,
	      "logo": null,
	      "updated_at": "2012-08-23T23:48:40.739777",
	      "created_at": "2012-08-23T23:48:40.739763",
	    }
	  ],
	  "page": 1
	}

### Query Constraints
There are several ways to put constraints on the objects found, using the <code>**q**</code> URL parameter. The value of the <code>**q**</code> parameter should be encoded JSON. Thus, if you look at the actual URL requested, it would be JSON-encoded, then URL-encoded. The simplest use of the <code>**q**</code> parameter is constraining the value for keys.

It can have the following mappings, all of which are optional:

#### filters

A list of objects of one of the following forms:

	{"name": <fieldname>, "op": <operatorname>, "val": <argument>}
or:

	{"name": <fieldname>, "op": <operatorname>, "field": <fieldname>}

In the first form, <operatorname> is one of the strings described in the <a href="#operators">Operators</a> section, the first <fieldname> is the name of the field of the model to which to apply the operator, <argument> is a value to be used as the second argument to the given operator. In the second form, the second <fieldname> is the field of the model which should be used as the second argument to the operator.

For example, if we wanted to retrieve offers with *type* == 1 and *name* field like %лбас%, we could do:

	curl -X GET \
	  -G \
	  --data-urlencode 'q={"filters": [{"name": "type", "op": "==", "val": 1},{"name": "name", "op": "like", "val": "%лбас%"}]}' \
	  http://myconomy.com/api/v1/classes/offers

<fieldname> may alternately specify a field on a related model, if it is a string of the form <relationname>__<fieldname>.

The returned list of matching instances will include only those instances which satisfy all of the given filters.

#### limit

A positive integer which specified the maximum number of objects to return.

#### offset

A positive integer which specifies the offset into the result set of the returned list of instances.

#### order_by

A list of objects of the form:

	{"field": <fieldname>, "direction": <directionname>}

where <fieldname> is a string corresponding to the name of a field of the requested model and <directionname> is either "asc" for ascending order or "desc" for descending order.

#### single

A boolean representing whether a single result is expected as a result of the search. If this is true and either no results or multiple results meet the criteria of the search, the server responds with an error message.

If a filter is poorly formatted (for example, op is set to '==' but val is not set), the server responds with <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html#sec10.4.1">400 Bad Request</a>.

### Operators
The operator strings recognized by the API incude:

	==, eq, equals, equals_to
	!=, neq, does_not_equal, not_equal_to
	>, gt, <, lt
	>=, ge, gte, geq, <=, le, lte, leq
	in, not_in
	is_null, is_not_null
	like
	has
	any

These correspond to SQLAlchemy column operators as defined <a href="http://docs.sqlalchemy.org/en/latest/core/expression_api.html#sqlalchemy.sql.operators.ColumnOperators">here</a>.




### Relational Queries

## Users
In general, users have the same features as other objects. The differences are that user objects must have a <code>**email**</code> and <code>**password**</code>, the password is automatically encrypted and stored securely, and Myconomy enforces the uniqueness of the email field.

### Signing Up
Signing up a new user differs from creating a generic object in that the <code>**email**</code> and <code>**password**</code> fields are required. And <code>**email**</code> must be unique. The <code>**password**</code> field is handled differently than the others; it is encrypted when stored in the Myconomy and never returned to any client request.

To sign up a new user, send a POST request to the users root. You may add any additional fields. For example, to create a user with a specific phone number:

	curl -X POST \
	  -H "Content-Type: application/json" \
	  -d '{"username":"apitest123","password":"p_n7!-e8","phone":"415-392-0202"}' \
	  http://myconomy.com/api/v1/users

When the creation is successful, the HTTP response is a 201 Created:
	Status: 201 Created

The response body is a JSON object containing the <code>**id**</code>, the <code>**created_at**</code> timestamp of the newly-created object, and the sessionToken which can be used to authenticate subsequent requests as this user:

	{
      "id": "g7y9tkhB7O",
	  "created_at": "2011-11-07T20:58:34.448Z",
	  "sessionToken": "pnktnjyb996sj4p156gjtp4im"
	}

### Logging In
### Verifying Emails
### Requesting A Password Reset
### Retrieving Users
### Updating Users
### Querying Users
### Deleting Users
### Linking Users
### Security

## Roles
### Creating Roles
### Retrieving Roles
### Updating Roles
### Deleting Roles
### Security
### Role Hierarchy

## Groups
### Creating Groups
### Retrieving Groups
### Updating Groups
### Deleting Groups
### Security
### Group Hierarchy

## Files
### Uploading Files
### Associating with Objects
### Deleting Files








and we can even [link](#head1234) to it so:

<a href="#" name="roles-creating"></a>
<a href="#" class="section section_minor" name="roles-creating_anchor"></a>
<h3>
    Creating Roles
</h3>
<p>
    Creating a new role differs from creating a generic object in that the
    <code>
        name
    </code>
    field is required. Roles must also specify an
    <a href="#users-security"><code>ACL</code></a>
    , which should be as restrictive as possible to avoid allowing the wrong
    users to modify a role.
</p>




1.
Просмотр спец предложений (1-hotdeals):

		GET http://<host>:<port>/api/v1/offers
		Параметр q равен:
		{"filters": [{"name": "type", "op": "==", "val": 1}]}
		Ответ:
		HTTP/1.1 200 OK


2.
Просмотр списка магазинов пользователя (5-profile):

		GET http://<host>:<port>/api/v1/users/<user_id>
		Параметр q равен:
		{"filters": [{"name": "type", "op": "==", "val": 1}]}
		Ответ:
		HTTP/1.1 200 OK



3.
Просмотр списков покупок пользователя (не отрисовано в дизайне страниц):

    GET http://<host>:<port>/api/v1/users/<user_id>
    или
    GET http://<host>:<port>/api/v1/lists
		Параметр q равен:
		{"filters": [{"name": "user_id", "op": "==", "val": <user_id>}]}
		Ответ:
		HTTP/1.1 200 OK

4.
Просмотр конкретного списка покупок пользователя (не отрисовано в дизайне страниц):

    GET http://<host>:<port>/api/v1/lists/<list_id>
		Ответ:
		HTTP/1.1 200 OK



5.
Добавление в список покупок новой позиции (1-add-suggestions):

    POST http://<host>:<port>/api/v1/listitems
    {"list_id": 2, "offer_id":3}
    ответ будет вида:
    HTTP STATUS: HTTP/1.1 201 Created
		{
		  "id": 3
		}
		id - идентификатор новой записи
6.
Удалить позицию из списка (1-list-complete-delete)

    DELETE http://<host>:<port>/api/v1/listitems/<item_id>
    если все нормально ответ будет вида:
    HTTP STATUS: HTTP/1.1 204 No Content

7.
Поиск магазина по координатам (2-shop-searching)
Клиент определяет координаты магазина в виде (xx.xxxx, yy.yyyy)
где xx.xxxx - широта, yy.yyyy-долгота. Далее нужно экспериментально подобрать погрешность поиска <epsilon> и сформировать
квадратную область поиска магазина

    GET http://<host>:<port>/api/v1/stores
		Параметр q равен:
		{"filters":
		  [
		    {"name": "lat", "op": "ge", "val": <xx.xxxx - epsilon searching>},
				{"name": "lat", "op": "le", "val": <xx.xxxx + epsilon searching>},
		    {"name": "lng", "op": "ge", "val": <yy.yyyy - epsilon searching>},
				{"name": "lng", "op": "le", "val": <yy.yyyy + epsilon searching>},
		  ]
		}
		Ответ:
		HTTP/1.1 200 OK
		{
		  "objects": [
		    {
		      "city": "\u041c\u043e\u0441\u043a\u0432\u0430",
		      "updated_at": "2012-08-13T22:28:43.493100",
		      "phone": null,
		      "network": "\u041f\u0435\u0440\u0435\u043a\u0440\u0435\u0441\u0442\u043e\u043a",
		      "metro": null,
		      "created_at": "2012-08-13T22:28:43.493085",
		      "region": null,
		      "who_add": {...},
		      "name": "\u041f\u0435\u0440\u0435\u043a\u0440\u0435\u0441\u0442\u043e\u043a",
		      "delivery": false,
		      "onlineonly": false,
		      "address": null,
		      "lat": null,
		      "user_id": 1,
		      "lng": null,
		      "id": 1,
		      "description": null
		    },
		    {
		      "city": "\u041c\u043e\u0441\u043a\u0432\u0430",
		      "updated_at": "2012-08-13T22:28:43.498919",
		      "phone": null,
		      "network": "\u041f\u044f\u0442\u0435\u0440\u043e\u0447\u043a\u0430",
		      "metro": null,
		      "created_at": "2012-08-13T22:28:43.498902",
		      "region": null,
		      "who_add": {...},
		      "name": "\u041f\u044f\u0442\u0435\u0440\u043e\u0447\u043a\u0430",
		      "delivery": false,
		      "offers": [],
		      "onlineonly": false,
		      "address": null,
		      "lat": null,
		      "user_id": 1,
		      "lng": null,
		      "id": 2,
		      "description": null
		    }
		  ],
		  "page": 1
		}

8.
