---
title: О проблемах растущего размера
layout: post
tags: [scalability]
alias: /2009/08/blog-post.html
---

Все таки интернет индустрия развивается. Теперь на каждом углу высоконагруженные проекты, миллионы пользователей, требования к high-availability, масштабиремости. Причем вот ведь странно. К масштабиремости всегда относятся как-то однобоко. Иногда ее путают с производительностью. А иногда не понимают что масштабируют.

Dan Pritchett, один из архитекторов eBay (теперь уже бывший), еще в 2006 году написал отличное эссе _You scaled your what?_ на тему векторов масштабирования (scaling vectors)[^you-scaled-your-what]. Действительно, существует масса направлений которые требуют внимания при интенсивном росте проекта, а следственно и сложности решаемых в проекте проблем. А это значит, что употребляя слово "масштабируемость", мы должны отдавать себе отчет в том, в каком контексте мы употребляем это слово.

Transactional scalability
-------------------------
Наверное, самый привычный вектор. Пропускная способность системы выражающаяся в количестве транзакций которые система может обслужить в единицу времени. Это есть ни что иное, как мера количества пользователей которые одновременно могут пользоваться системой. Когда говорят о масштабирумости в большинстве случаев имеют ввиду именно этот вектор. Простой и понятный большинству, он легко поддается измерению.

Data scalability
----------------
Тоже довольно популярный вектор. Насколько хорошо система справляется с ростом dataset'а. Бывает так, что система хорошо приспособлена к росту пользовательской аудитории, но плохо переносит возрастающий набор данных. Причиной может быть природа реляционных баз данных, которые плохо приспособлены к высокой конкурентной нагрузке.

Важно понимать, что цена хранения одного мегабайта данных зависит от цены потери одного мегабайта данных. При росте dataset'а, использовать один и тот же подход для хранения данных разной важности крайне неэффективно. Как и в случае с transactional scalability типичным ответом на data scalability является горизонтальное масштабирование.

Operational scalability
-----------------------
Очень важный вектор, который до поры до времени игнорируется многими командами. Программное обеспечение нуждается в поддержке. Его необходимо контролировать, мониторить, тестировать и выявлять ошибки (желательно раньше чем это сделают ваши пользователи), определять потенциально узкие места с точки зрения производительности (до того, как они вас "задушат"). Сложность всех этих процессов растет вместе со сложностью системы.

Представьте себе простое web-приложение работающее на одном сервере и использующее в качестве базы данных простые текстовые файлы. Такое приложение может представлять из себя буквально пару десятков скриптов. Вряд ли бы у вас возникли проблемы с организацией процесса разработки и тестирования такого приложения. А что если это система распределена по 15 серверам, написана на разных языках и использует самое различное middleware обеспечение? Как бы вы вообще запустили бы такую систему на машине разработчика? И стали бы вы вообще это делать?

Если не уделять внимания этому вектору, то при росте инфраструктурной сложности он вам нанесет "ответный удар", не сомневайтесь.

Feature time-to-market scalability
----------------------------------
Ничто так не омрачает большой проект, как большое количество программистов. Большое количество программистов = большое количество проблем. Но тем не менее, бизнес не стоит на месте — он растет. Много идей, кто-то должен их реализовывать. Для этого нужны новые люди. Но новые люди не всегда увеличивают производительность команды. Иногда все происходит совсем наоборот.

Умение при помощи растущего коллектива решать пропорционально растущий объем задач — это искусство.

Я назвал всего четыре вектора. Есть и другие, такие как: power scalability, deployability и другие. Более того внутри компании могут быть свои scaling vectors, которые обусловлены спецификой ее функционирования.

Конечно же (и это уже классика жанра), вы не сможете добиться максимума по всем направлениям — необходимо выбирать. Надо понимать, какие направления для вас являются приоритетными в краткосрочной перспективе, и что может изменится в долгосрочной. Поэтому, когда вы в следующий раз будете употреблять слово "масштабируемость", задумайтесь — _масштабируемость чего_?

[^you-scaled-your-what]: [Dan Pritchett: You Scaled Your What?](http://www.addsimplicity.com/adding_simplicity_an_engi/2006/11/you_scaled_your.html)