## Обзор наиболее востребованных технологий, которые будут изучаться на курсе TopJava. Часть 2

## ![video](https://cloud.githubusercontent.com/assets/13649199/13672715/06dbc6ce-e6e7-11e5-81a9-04fbddb9e488.png) [Видео](https://drive.google.com/file/d/1JLIieojERPJQuqJXxJSC5tc4mzb_4JuU)

### Frameworks
Мы переходим к фреймворкам. Фреймворки нам нужны, чтобы взять 
готовое решение для определенной задачи и дописать только нужную 
для нас бизнес логику. В чем-то есть сходство с паттерном 
шаблонный метод, где определяют скелет алгоритма, перекладывая 
ответственность за некоторые его шаги на подклассы. Здесь же 
определяется скелет архитектуры, его базовые классы и даются 
различные реализации. Мы можем выбрать любую из них или написать собственную.

Например если мы создаем обычное web приложение, чтобы 
принимать HTTP запросы и отдавать HTTP ответы, нам не 
нужно создавать все web компоненты с нуля, мы берем 
готовый web фреймворк, такой как Spring MVC, и дописываем 
специфичную для нашего конкретного случая бизнес логику. 
Значительная часть кода за нас уже написана и протестирована.
Вэб приложение это безусловно не единственный пример. 
Могут быть приложения, которые занимаются запуском каких 
то периодических задач и не принимают HTTP запросов. 
Это может быть приложение, которое только общается с 
Message брокером, таким как RabbitMQ или Kafka - принимает 
сообщения и отправляет в него сообщения.
Для всех подобных задач существуют специальные фреймворки 
с готовыми решениями.

Одна бэкэнд система может иметь в себе множество компонентов, 
включающих разные виды упомянутых приложений. Подавляющее 
большинство современных приложений работают с HTTP 
(это взаимодействие с UI в браузере или между сервисами по REST).
Поэтому на этом курсе мы создаем как веб-приложение, работающее с UI, 
а также и REST API, готовое для интеграции с любыми другими сервисами 
(например с мобильным приложением).

>[JVM Ecosystem Report 2021](https://snyk.io/jvm-ecosystem-report-2021/) 
>показывает, что Spring является абсолютным 
>лидером среди фреймворков.

На первом месте упоминается **Spring Boot** и на втором **Spring MVC**. 

Здесь я хотел бы внести некоторую ясность.
Сердцем Spring является Spring Core, который реализует Dependency 
Injection.   
Этот компонент как правило используется во всех остальных 
проектах Spring Framework.

Spring Boot это надстройка над Spring Framework, 
которая позволяет быстро создавать приложения разных типов, 
использовать автоматическую конфигурацию для некоторых 
компонентов и использовать некоторые удобные встроенные 
инструменты, например готовые инструменты для мониторинга 
работы приложения (Spring Actuator).

Если мы создаем web-приложение, то мы можем создавать его с 
помощью Spring Boot, но Spring MVC, который является именно 
web фреймворком, также будет присутствовать в таком приложении 
и играть ключевую роль.

Spring Boot позволяет создавать очень простые приложения без 
единого конфигурационного класса, но как только мы пытаемся 
создать что то более сложное, нам приходится в любом случае 
создавать конфигурационные классы и настраивать все вручную 
точно так же, как в традиционном Spring приложении. 
По своему опыту могу сказать, что на реальных проектах 
такая ситуация возникает в большинстве случаев. 
Например как только тебе нужно настроить подключение 
к нескольким базам данных, а не к одной, ты вынужден 
создавать конфигурационные классы вручную.

В этом случае Spring Boot в какой то степени может даже 
навредить вашей продуктивности, потому что Вам придется 
разбираться какие автоконфигурационные классы отключить и так далее.

Мы изучаем Spring довольно глубоко.
Традиционно хорошо показал себя подход, при котором 
вначале изучается чистый Spring Framework, после чего 
мы переходим к использованию Spring Boot. Такой подход 
сохраняется и в этой версии курса. Без этого Spring Boot 
будет для вас черным ящиком, который вам будет очень 
сложно понять, настраивать и отлаживать.

### ORM frameworks
Отчеты, которые мы использовали обычно не включают информацию 
о самых популярных ORM фреймворках.

>Общеизвестно, 
>что **Hibernate** является достаточно популярным фреймворком 
>и наиболее часто упоминается в вакансиях, если сравнивать 
>его с другими ORM и инструментами для работы Java приложения 
>с базами данных. 

Вот одна из статей, которая также говорит о 
популярности Hibernate: [Top 5 Java ORM tools - 2022](https://www.knowledgefactory.net/2021/09/top-java-orm-tools-20XX.html)

**ORM** или **Object-relational-mapping** можно перевести как 
объектно-реляционное отображение, или преобразование.   
Это техника, которая позволяет создать виртуальную базу 
данных с помощью объектно ориентированного языка 
программирования и взаимодействовать с ней, в то время 
как взаимодействие уже с реальной базой данных выполняется 
фреймворком незаметно для нас.
Это облегчает работу, позволяет работать с привычными 
и удобными для использования Java объектами, вызывая 
их методы вместо того, чтобы писать SQL запросы к базе данных.

>Hibernate является реализацией спецификации JPA, 
>также как и менее популярный EclipseLink.   

Говоря простым языком JPA или Java Persistance API это 
набор интерфейсов  без реализации для работы с ORM, 
который включен в Jave EE стандарт. Отдельные провайдеры 
могут предоставлять свои реализации этого интерфейса.

Недостатками JPA и Hibernate являются удар по производительности 
и недостаточная гибкость. Вопрос производительности частично 
может быть решен с помощью различных техник оптимизации кода, 
наприсанного с использование JPA, ондако для некоторых 
приложений тот оверхэд, который несет в себе JPA является 
недопустимым и вы можете увидеть на некоторых проектах 
использование других подходов - начиная от использования 
чистого JDBC до использования MyBatis, JOOQ или каких 
то альтернативных решений.

В реальных приложениях те запросы к базе данных, 
которые создают наибольшую нагрузке на систему, 
могут быть оптимизированы для улучшения производительности - для 
них могут быть применены JDBC, альтернативные 
Hibernate фреймворки или запросы могут быть написаны 
с помощью нативных SQL запросов в JPA. 
Для остальных запросов, которые не приводят к 
большой нагрузке на систему, в том же приложении может 
быть применен Hibernate. 
Таким образом в одном приложении могут быть применены одновременно разные технологии.


На курсе вы изучите как работать с БД с помощью нескольких 
технологий - JDBC (а точнее Spring JDBC template), 
а также JPA и Spring DataJPA. 
Таким образом, вы сами не только увидите, но и почувствуете 
при написании кода в ваших домашних заданиях плюсы и минусы каждого подхода.

### Обзор пройденных тем
Давайте подведем промежуточные итоги по результатам этого урока.

В этом уроке мы:

* познакомились с тем, что такое фреймворки 
и для чего они нужны;
*  также посмотрели статистику, которая определяет 
Spring Framework как самый популярный фреймворк на рынке.
* также мы познакомились с ORM - подходом для упрощения работы 
с базами данных с использование объектно-ориентированного подхода. 
* узнали про JPA - java persistence API - протокол для работы с 
ORM и о  реализациях JPA. Hibernate является самой популярной реализацией JPA. 
* обсудили недостатки подхода ORM и познакомились с инструментами, 
которые могут быть использованы в качестве альтернативы.

В следующем коротком уроке мы завершим обзор используемых технологий.
Увидимся в следующем видео. 