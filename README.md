spicy.history
=============

Приложение Django для SpicyCMS. Использует [концепцию реиспользования кода и конфигурации spicy.core](https://github.com/spicycms/spicy.core). Это простое приложение использует по умолчанию типовые шаблоны и часть логики ``spicy.core.admin``, определяет модели отзыва Feedback и шаблона отзыва FeedbackPattern для отслеживания обратной связи на сайте.

Для запуска необходима версия 1.4.11 - 1.5.12 Django.

Назначение
----------
Модуль предназначен для ведения истории изменений объектов на сайте, просмотра изменений в стиле ``git diff``, отката к предыдущим версиям. Вы можете настроить spicy.history так, чтобы отслеживать изменения документов, медиафайлов, профилей пользователей, любых других объектов, любых полей этих объектов.

Подключить spicy.history к вашему приложению
--------------------------------------------
Установите модуль с помощью pip: ``pip install git+https://github.com/spicycms/spicy.history#egg=spicy.history``.

Добавьте в настройки установленных приложений в ``settings.py``:
```
INSTALLED_APPS = (
    ...
    'spicy.history',
    ...
)
```

Добавьте в ``urls.py`` путь для модуля spicy.history в ``settings.py``:
```
urlpatterns = patterns('',
    ...
    url(r'^', include('spicy.history.urls', namespace='history')),
    ...
)
```
После этого необходимо выполнить ``manage.py syncdb``, чтобы Django создала таблицы spicy.history в базе данных. Ваше приложение настроено, чтобы использовать spicy.history. Теперь нужно [настроить](./README.md#Настройка-истории-для-объектов), для каких объектов на сайте вести историю.

Настройка истории для объектов
------------------------------
Вы можете указать spicy.history отслеживать любое поле любой модели приожения. Для этого в ``settings.py`` укажите:
```
OBSERVED_FIELDS = {
    'webapp.Document': ('body', 'slug', 'title', 'pub_date'),
    ...
}
```
В этом примере, spicy.history настроен на отслеживание модели документа ``Document``, будут сохраняться изменения для полей ``body``, ``slug``, ``title``, ``pub_date``. Аналогично вы можете добавить и другие модели в ``OBSERVED_FIELDS``, перечислив их поля.



