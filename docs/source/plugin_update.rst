.. _plugin-update-label:

Plugin Update
==============

After the plugin is available 
После того как плагин написан и выложен в `магазине Oxwall <http://www.oxwall.org/store>`_ разработчикам зачастую требуется постоянный механизм позволяющий просто и
быстро вносить свои изменения в плагины и распространять эти изменения среди своих клиентов. Давайте посмотрим как это можно просто сделать на платформе Oxwall.

Исправляем ошибки в плагине
---------------------------

Наша задача исправить вымышленную ошибку в коде нашего плагина. Представим, что мы уже написали наш первый плагин и его **plugin.xml**
описывающий мета информацию плагина выглядит так: (подробнее про структуру файлов плагина можно прочитать в разделе - :ref:`plugin-structure-label`) :

.. code-block:: xml

    <?xml version="1.0" encoding="utf-8"?>
    <plugin>
        <name>My Super Plugin</name>
        <key>superplugin</key>
        <description>My super plugin.</description>
        <author>Me</author>
        <authorEmail>me@oxwall.org</authorEmail>
        <authorUrl>http://www.me.com</authorUrl>
        <developerKey>MY_DEV_KEY</developerKey>
        <build>1</build>
        <copyright>(C) 2015 My. All rights reserved.</copyright>
        <license>OSCL</license>
        <licenseUrl>http://www.oxwall.org/store/oscl</licenseUrl>
    </plugin>

Мы нашли и исправили ошибку и теперь просто повышаем номер `билда <https://en.wikipedia.org/wiki/Software_build>`_ в нашем **plugin.xml** c **1** до **2**. И наш результирующий файл стал выглядеть так:

.. code-block:: xml

    <?xml version="1.0" encoding="utf-8"?>
    <plugin>
        <name>My Super Plugin</name>
        <key>superplugin</key>
        <description>My super plugin.</description>
        <author>Me</author>
        <authorEmail>me@oxwall.org</authorEmail>
        <authorUrl>http://www.me.com</authorUrl>
        <developerKey>MY_DEV_KEY</developerKey>
        <build>2</build>
        <copyright>(C) 2015 My. All rights reserved.</copyright>
        <license>OSCL</license>
        <licenseUrl>http://www.oxwall.org/store/oscl</licenseUrl>
    </plugin>

Теперь можно запаковать наш плагин с обновленным файлом **plugin.xml**, а также с нашими исправлениями в коде и загрузить архив в магазин Oxwall
(не забудьте сделать пакет с исправлениями основным в настройках загруженного плагина). Система автоматически оповестит всех клиентов о наличии обновлений и
клиентам останется только нажать на ссылку обновить плагин в админ панели своего сайта. Но бывает ситуации когда не достаточно внести изменения только в файлы кода,
но также необходимо внести изменения в структуру базы данных, добавить/удалить виджет или просто выполнить произвольный **php** код, для этого мы можем написать скрипт обновления,
о чем и пойдет речь ниже.

Скрипты обновления
------------------

**Что такое скрипт обновления?** - это просто произвольный **php** скрипт который завязан на определенный билд плагина,
т.е если номер билда у нас **2**, то ему возможно будет соответствовать скрипт обновления с таким же номером, но не всегда, скрипты обновлений является опциональными.
И так представим, что нам нужно внести изменения в базу данных в таблицы нашего плагина, а также добавить новые переводы.
Для этого нам нужно создать в директории **update** нашего плагина директорию с названием **2** которая соответствует
нашему последнему билду с исправлениями (выше в разделе - :ref:`plugin-update-label` мы исправляли вымышленную ошибку) и так структура директорий нашего плагина должны выглядеть примерно так:

| **/**
| - - **bol/**
| - - **classes/**
| - - **components/**
| - - **controllers/**
| - - **mobile/**
| - - - - **classes/**
| - - - - **components/**
| - - - - **controllers/**
| - - - - **views/**
| - - - - *init.php*
| - - **static/**
| - - - - **css/**
| - - - - **js/**
| - - - - **images/**
| - - **views/**
| - - - - **components/**
| - - - - **controllers/**
| - - **update/**
| - - - - **2/ (наш скрипт обновлений)**
| - - *init.php*
| - - *cron.php*
| - - *activate.php*
| - - *deactivate.php*
| - - *install.php*
| - - *uninstall.php*
| - - *langs.zip*
| - - *plugin.xml*
|

Внутрь созданной директории помещаем наш скрипт обновления - **update.php** (название скрипта менять не нужно). Ниже приведу пример содержимого этого файла:

.. code-block:: php

    <?php

    // импорт новых переводов плагина
    Updater::getLanguageService()->importPrefixFromZip(dirname(__FILE__) . DS . 'langs.zip', 'superplugin') ;

    // добавляем новый индекс в таблицу
    $sql = "ALTER TABLE `".OW_DB_PREFIX."my_table` ADD UNIQUE `userId` (`userId`)";
    Updater::getDbo()->query($sql);

Скрипт обновления создан, теперь мы можем запаковать весь плагин и выложить его в магазине Oxwall.
С основными сервисами которые могут вам помогут эффективно работать при написании плагинов или обновлений можно познакомиться в разделе - :ref:`main-application-service-label`
