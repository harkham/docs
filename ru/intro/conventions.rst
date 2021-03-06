Соглашения CakePHP
##################

Мы являемся большими поклонниками принципа "соглашения превыше конфигурации".
Несмотря на то, что изучение соглашений (перечень условных правил) CakePHP занимает какое-то время, их
знание сэкономит Вам огромное количество времени в будущем. Следуя соглашениям,
Вы получаете готовую функциональность без необходимости написания дополнительных
настроек. Также соглашения упрощают процесс совместной разработки, позволяя без
особых проблем другим разработчикам присоединиться к Вашему проекту, не вникая
во все тонкости его реализации.

Соглашения Контроллера
======================

Названия классов контроллера обычно пишутся во множественном числе, c
использованием ВерблюжьегоРегистра и оканчиваются на слово ``Controller``. К
примеру такие имена, как ``UsersController`` и ``ArticleCategoriesController``
хорошо соответствуют соглашениям.

Публичные методы контроллеров часто становятся так называемыми 'экшенами',
доступными через веб-браузер. К примеру такая часть URL-адреса ``/users/view``
по умолчанию соответствует методу ``view()`` контроллера ``UsersController``.
Защищенные (protected) или закрытые (private) методы не доступны системе
маршрутизации (роутинга).

URL-адреса и имена котроллеров
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Как Вы только что видели, контроллеры с названием из одного слова связываются с
соответствующим адресом URL в нижнем регистре. К примеру ``UsersController``
(объявленный в файле **UsersController.php**) доступен по адресу 
http://example.com/users.

Вы также можете вызывать контроллеры, имена которых состоят из нескольких слов, 
для этого, в соответствии с соглашениями, Ваши URL-адреса должны быть в нижнем
регистре разделенные дефисами с использованием класса ``DashedRoute``,
cледовательно ``/article-categories/view-all`` будет корректной формой обращения
к экшену ``ArticleCategoriesController::viewAll()``.

Когда Вы создаете ссылки с использованием  метода ``this->Html->link()``, Вы
можете воспользоваться следующими соглашениями для массива url::

    $this->Html->link('текст-ссылки', [
        'prefix' => 'MyPrefix' // ВерблюжийРегистр
        'plugin' => 'MyPlugin', // ВерблюжийРегистр
        'controller' => 'ControllerName', // ВерблюжийРегистр
        'action' => 'actionName' // верблюжийРегистр
    ]

Для более подробной информации о URL-адресах CakePHP и обработке параметров,
смотрите :ref:`routes-configuration`.

.. _file-and-classname-conventions:

Соглашения о Наименовании классов и Файлов
==========================================

В общих чертах, имена файлов должны совпадать с именами классов, и следовать
стандартам автозагрузки PSR-0 или PSR-4. Вот некоторые примеры имен классов и
их файлов:

-  Класс контроллера ``LatestArticlesController`` может быть найден в файле с
   именем **LatestArticlesController.php**
-  Класс компонента ``MyHandyComponent`` может быть найден в файле с
   именем **MyHandyComponent.php**
-  Класс таблицы ``OptionValuesTable`` может быть найден в файле с
   именем **OptionValuesTable.php**.
-  Класс объекта данных ``OptionValue`` может быть найден в файле с
   именем **OptionValue.php**.
-  Класс поведения ``EspeciallyFunkableBehavior`` может быть найден в файле с
   именем **EspeciallyFunkableBehavior.php**
-  Класс вида ``SuperSimpleView`` может быть найден в файле с
   именем **SuperSimpleView.php**
-  Класс хелпера ``BestEverHelper`` может быть найден в файле с
   именем **BestEverHelper.php**

Каждый файл может быть найден в соответствующей папке/пространстве имен в папке
вашего приложения.

.. _model-and-database-conventions:

Соглашения Модели и Базы данных
===============================

Имена классов таблиц обычно пишутся во множественном числе, c использованием
ВерблюжьегоРегистра. ``Users``, ``ArticleCategories``,
и ``UserFavoritePages`` - примеры хорошего соответствия соглашениям.

Имена таблиц, соответствующие шаблону CakePHP - это имена в форме
множественного числа, и если название состоит из нескольких слов, то
они разделяются подчеркиваниями. Такие имена, как ``users``,
``article_categories`` и ``user_favorite_pages`` соответствуют шаблону.

В соответствии с соглашениями, название таблиц и полей должны
именоваться английскими словами. Иначе, CakePHP, возможно, не сможет
выполнить правильные преобразования (из единственного во
множественное число и наоборот). Если же Вы хотите добавить правила обработки для
некоторых слов Вашего языка, Вы можете воспользоваться служебным
классом :php:class:`Cake\\Utility\\Inflector`.
Помимо определения этих пользовательских служебных правил, этот класс также
позволяет Вам проверять, что CakePHP понимает Ваш пользовательский синтаксис для
форм единственного и множественного числа. Смотрите документацию
:doc:`/core-libraries/inflector` для получения более подробной информации.

Имена полей, состоящие из двух и более слов, разделяются символом подчеркивания (например, first_name).

Внешние ключи, со связями между таблицами hasMany (один ко многим), belongsTo/hasOne (один к одному), распознаются по умолчанию как
имя связанной таблицы (в форме единственного числа) с последующим постфиксом
``_id``. Например, если таблица Users имеет связь hasMany с таблицей
Articles, то таблица ``articles`` будет ссылаться на таблицу ``users`` по
внешнему ключу ``user_id``. Для таких таблиц, как ``article_categories``, у
которых названия состоят из нескольких слов, внешним ключом будет поле
``article_category_id``.

Связывающие таблицы, используемые при связи BelongsToMany (многие ко многим) между
моделями, должны быть названы таким образом, чтобы имена связанных таблиц
перечислялись в алфавитном порядке (``articles_tags``, а  не ``tags_articles``).

При использовании первичного ключа, вместо обычного
автоинкрементного поля, Вы можете использовать 
UUID поле. CakePHP будет создавать уникальный 36-значный UUID
(:php:meth:`Cake\\Utility\\Text::uuid()`), каждый раз когда Вы сохраните новую запись, используя метод
``Table::save()``.

Соглашения Представления (Вида)
===============================

Имена файлам представления присваиваются в соответствии с названием метода контроллера использующего его, 
а если название метода состоит из нескольких слов, то они
разделяются символом подчеркивания. Методу ``viewAll()`` класса
``ArticlesController`` будет соответствовать шаблон
**src/Template/Articles/view_all.ctp**.

Общий принцип именования шаблонов:
**src/Template/Контроллер/имя_метода.ctp**.

Именуя части Вашего приложения в соответствии с соглашениями CakePHP, Вы
получаете готовую функциональность без проблем, связанных с необходимостью
написания дополнительных параметров. В результате так должно выглядеть Ваше приложение:

-  Таблица в базе данных: "articles"
-  Класс таблицы: ``ArticlesTable``, находится в файле **src/Model/Table/ArticlesTable.php**
-  Класс объекта данных: ``Article``, находится в файле **src/Model/Entity/Article.php**
-  Класс контроллера: ``ArticlesController``, находится в файле
   **src/Controller/ArticlesController.php**
-  Шаблон представления находится в файле **src/Template/Articles/index.ctp**

Используя данные соглашения, Вы будете точно знать, что запрос
http://example.com/articles/ вызывает метод ``index()`` контроллера
ArticlesController, где автоматически появилась модель Articles (которая уже
связана с таблицей ‘articles‘ в базе данных) и подключит соответствующее представление. Ни
одно из этих отношений не требует никаких настроек, а только создания
классов и файлов, которые все равно придется создать.

После того, как Вы познакомились с основами фреймворка
CakePHP, Вы можете ознакомиться с примером создания простого приложения -
:doc:`/tutorials-and-examples/bookmarks/intro` и увидеть все выше описанное на
практике.

.. meta::
    :title lang=ru: Соглашения CakePHP
    :keywords lang=ru: опыт веб-разработки,maintenance nightmare,метод index,legacy systems,названия методов,класс php,uniform system,config files,tenets,articles,соглашения,conventional controller,лучшие практики,maps,visibility,news articles,functionality,logic,cakephp,developers
