- [ ] Пофіксити n+1 для auth/token/login
- [x] Пофіксити сваггер ендпоінту додавання керівника до групи
- [ ] -
- [x] Додати час до сповіщень для Лізи
- [x] Парсити особисту дату батьків і дітей
- [x] Продовжити з рефактором із https://chatgpt.com/c/600febe9-c49c-4e18-860f-fb7ef9e66105
- [x] Парсинг департаменту
- [x] Імпорт департаменту
- [x] Імпорт дитсадків
	- [ ] Імпортувати медіа і спитати в Микити за юзерів
- [ ] Імпорт аплікейшину
	- [x] kindergarten
	- [ ] group
		- [ ] Яку групу закидувати в CreateKindergartenApplication
	- [ ] ageGroup
		- [ ] Яку вікову групу закидувати в CreateKindergartenApplication
	- [x] parent
	- [ ] kid
		- [ ] Треба фетчити по $childData?
- [ ] Перевірити збереження файлів в бібліотеці


Questions:
- Що таке koatuu і katottg в Region моделі та чи треба мені це якось імпортувати?
- Що таке subdomain в departments сутності та звідки його брати? (Зараз зробив заглушкою)
- Не впевнений що зрозумів якого юзера треба прокидувати в CreateKindergarten->create($user, ...). Це для асоціації медіа з адмін юзером, чи що?
- Не до кінця розумію різницю між kindergarten_groups та kindergarten_age_groups.
- Мабуть, треба пояснення по групам та KindergartenApplication, бо я трохи заплутався і не впевнений як фіналізувати імпорт

Global importn notes:
- CreateUser ParentData атрибут додав тільки для імпорту, можно видалити після імпорту
- subdomain в departments зараз заглушка, бо не розумію звідки його брати
- CreateKindergarten->create() юзера прокидую заглушкою, змінити на динамічного юзера в залежності від відповіді Микити
- По kindergartens табличці не знаю звідки парсити інфу для колонок:
	- short_name
	- short_description
	- site
- StoreUploadedFromImport видалити після імпорту