.. _plugin-key-label:

Getting developer and plugin keys
====================================

Для того, чтобы начать разработку собственных плагинов или тем вам нужен ключ разработчика, а также ключ плагина или темы.

Что такое ключ разработчика?
----------------------------

Если вы планируете развивать свой бизнес вместе с **Oxwall** то вам необходимо получить уникальный идентификационный номер разработчика,
который нужно будет включать во все  свои плагины или темы в файл **plugin.xml** или **theme.xml**.

**Ключ разработчика** идентифицирует разработчиков плагинов или тем позволяя им сохранять авторство. Это один из наиболее важных параметров в файле **plugin.xml**
(Подробнее про структуру плагина можно прочитать в разделе :ref:`plugin-structure-label`) и **theme.xml**.

Для получения ключа разработчика вам нужно зарегистрировать новый аккаунт на  `oxwall.org <http://oxwall.org>`_ или использовать уже существующий аккаунт
если вы регистрировались ранее. После регистрации нужно перейти на страницу - `Dev-tools <http://www.oxwall.org/store/dev-tools>`_ и оттуда скопировать
уже сгенерированный для вас ключ.

В примере ниже можно видеть куда прописывать полученный вами ключ разработчика в файл **plugin.xml**

.. code-block:: xml

    <?xml version="1.0" encoding="utf-8"?>
    <plugin>
        <name>My Super Plugin</name>
        <key>superplugin</key>
        <description>My super plugin.</description>
        <author>Me</author>
        <authorEmail>me@oxwall.org</authorEmail>
        <authorUrl>http://www.me.com</authorUrl>
        <developerKey>------->MY_UNIQUE_DEV_KEY<-------</developerKey>
        <build>1</build>
        <copyright>(C) 2015 My. All rights reserved.</copyright>
        <license>OSCL</license>
        <licenseUrl>http://www.oxwall.org/store/oscl</licenseUrl>
    </plugin>

Что такое ключ плагина/темы?
----------------------------

Ключ плагина или темы - это просто уникальное название. Перед тем как начать разрабатывать собственный плагин или тему вам нужно удостовериться, что выбранный вами
ключ плагина или темы не используется другими плагинами или темами, проверка уникальности ключа осуществляеться на странице - `проверки ключа <http://www.oxwall.org/store/dev-tools>`_.
**Стоит отметить, что ключ плагина и темы должен быть прописан в нижнем регистре и не содержать никаких символов кроме латинских, а также цифр (a-z0-9).**

Ключ разработчика в купе с ключом плагина или темы идентифицирует ваш плагин среди других плагинов или тем, а также они используется во всей внутренней экосистеме `Oxwall <http://oxwall.org>`_.
К примеру панель администратора именно по этим ключам в плагинах или в темах может определить наличие новых обновлений или наличие прав на их использование.

В примере ниже можно видеть куда прописывать полученный вами ключ плагина в файле **plugin.xml**

.. code-block:: xml

    <?xml version="1.0" encoding="utf-8"?>
    <plugin>
        <name>My Super Plugin</name>
        <key>------->superplugin<-------</key>
        <description>My super plugin.</description>
        <author>Me</author>
        <authorEmail>me@oxwall.org</authorEmail>
        <authorUrl>http://www.me.com</authorUrl>
        <developerKey>MY_UNIQUE_DEV_KEY</developerKey>
        <build>1</build>
        <copyright>(C) 2015 My. All rights reserved.</copyright>
        <license>OSCL</license>
        <licenseUrl>http://www.oxwall.org/store/oscl</licenseUrl>
    </plugin>

