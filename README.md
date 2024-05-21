# Введение 

Этот плагин основан на «Zendo open source version of the LDAP plugin» на основе изменений, которые в настоящее время тестируются в версии 18.3

## Функция
1. Совместимость с локальными и LDAP-логинами пользователей
    * Установка плагина продолжается, синхронизация данных не повлияет на существующие методы входа в систему
    * Пожалуйста, проверьте, существует ли поле ldap в zt_user в используемой базе данных, если нет, то вам нужно добавить скрипт в каталог db, за подробностями обратитесь к главе «Структура каталогов» в Руководстве по разработке Zendo Secondary.
    * Пользователь admin также перезаписывается. Если данные, которые необходимо импортировать из LDAP, уже существуют в учетной записи администратора, не забудьте сначала создать резервную копию исходных данных.
2. Поддержка функции группировки по умолчанию, посадка данных в БД (таблица zt_usergroup)
3. Разделите поля **Протокол**, **Порт**.
4. Сохранение данных о новом номере мобильного телефона

### Инструкция по использованию
Вам нужно заархивировать каталог `ldap` или запустить скрипт `package.sh` непосредственно из текущего каталога.
### Конфигурация меню
Меню *LDAP* монтируется в `Backend->System Settings->LDAP`, и относится к модулю меню, соответствующему конфигурации `$lang->admin->menuList->system['subMenu']['ldap']`.

В настоящее время меню настроено в модуле `admin`, если вам нужно изменить его, вам просто нужно изменить его в соответствующем модуле.
EX: `$lang->admin->menuList->company['subMenu']['xxxx'] => array('link' => «{$lang->xxx->common}|xxxx|index|», 'subModule' => 'xxxx');`

### Модификация кода
Если вы хотите изменить/добавить свои собственные данные, например, добавить поля `dingding`/`weixin`.
Необходимые изменения.
1. Метод `sync2db` в `ldap/model.php`, измените объект `$user`, например, `$user->dinging = xxxx`.

### Debug 
1. Измените файл `vi /apps/zentao/config/my.php`, откройте Debug:
Измените значение параметра `$config->debug` на **`true`**.
2. проверьте журнал, каталог журнала находится в `/apps/zentao/tmp/log` или `/apps/zentao/tmp/log.14`, разница между этими двумя папками - разница в версии.

### Пример конфигурации

| опции | пример значения | обязательное поле | значение по умолчанию |
|  ----  | ----  | --- | --- |
|Базовая конфигурация||||
|||||
| протоколы  | 	ldap:// | T | ldap:// |
| LDAP сервер  | 	ldap.test.com | T | |
| порт  | 	389 | T | |
| searchDN  | ou=users,dc=test,dc=com | T| |
| BindDN  | cn=admin,dc=test,dc=com | T | |
| BindDN  | ou=users,dc=test,dc=com | T | | 
|||||
|Конфигурация||||
|||||
| Поля счета  | 	uid | T | uid |
| Группа пользователей по умолчанию  | выпадающий выбор | F | смотрители |
| Mail  | 	mail | F | mail |
| поле имени  | 	cn | T |cn |
| номер мобильного телефона  | 	mobile | F | mobile|


