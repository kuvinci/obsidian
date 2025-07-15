#Laravel #PHP #back-end 

- **symfony/console:v6.4.4:** Provides features to build **console applications**
- **doctrine/annotations:2.0.1**: Allows to implement **annotations** using docblocks
- **dragonmantank/cron-expression:v3.3.3:** Helps in calculating the next run of a **Cron job**
- **laravel/sanctum:v3.3.3:** Provides a featherweight **authentication** system for SPAs (single page applications), mobile applications, and simple, token based APIs.
- **lcobucci/jwt:4.3.0:** Implementation of the **JWT** format
- **monolog/monolog:3.5.0:** **Logs** both in production and during development
- **guzzlehttp/guzzle:7.8.1:** Comprehensive **HTTP client**


### Notes
- createDefaultStructure()
- private readonly ClassName $object
- apiRecourse якщо можливо
- Unit тести тестять простенькі класси, Feature на апішку чи веб роути
- [https://laravel.com/docs/11.x/database-testing](https://laravel.com/docs/11.x/database-testing) - unit test factories
- [https://laravel.com/docs/11.x/container](https://laravel.com/docs/11.x/container) - DI контейнер
- А ось це поліморфні звʼязки в базі, що я хотів показати в прикладі з Notes [https://laravel.com/docs/11.x/eloquent-relationships#polymorphic-relationships](https://laravel.com/docs/11.x/eloquent-relationships#polymorphic-relationships)

### Task
Додати нотатки (задати та подивитись нотатку по апі)
Моделі:
- teacher
- lesson
- student
- Note
	- Fields:
		- content_type=teacher/lessson/student
		- content_id
Поліморфний зв'язок?
### Questions:
- [x] Як працюють аннотації? DocBlock для автогенерації доків?
	- [x] (make docs)
- [x] Коли юзати Policy а коли Gate?

### Сповіщення
- [ ] Laravel reverb
- [ ] Доробити API в модулі users
- [ ] В доках конфлюєнсу Roles and Permissions
- [ ] Module common DTO
- [ ] ValueObjects
- [ ] FloatingPaginationTest.php
- [ ] Почитати за Swagger

Фідбек по сповіщенням
- [ ] Зробити DTOшку
- [ ] декілька сповіщень за раз
- [ ] редагування
- [ ] 401 помилка якщо не аутентифіковано
- [ ] 403 якщо просить не свої повідомлення
- [ ] пусте 201 якщо записів немає
- [ ] 200, через кому що отримані всі повідомлення, через кому перелік усіх які є
- [ ] Прописати Policies
- [ ] прописувати респонси на початку роботи
- [ ] А база працює? А ми попали в чергу?
- [ ] А якщо сповіщення в месенджери, чи не варто організувати сповіщення як івенти і поставити в чергу?
- [ ] Роберт Мартін "Чистий Код", "Чиста архітектура"

### Сповіщення питання:
1. Якщо не вибрати "Сповістити всіх користувачів", кого ми тоді оповіщаймо?
2. Чому, коли ми нажимаємо на галочку "Сповістити всіх користувачів" нам відкривається попап для сповіщення специфічних груп або користувачів 
3. 
4. Срок давності сповіщення?
5. Коли нотіфікейшин вважається прочитаним?
6. Групи користувачів це: Співробітники/Учні/Батьки цієї школи? Чи є додаткова логіка? Чи можуть бути вибрані декілька груп?
7. Чи буде можливість редагування сповіщення?