# Вопросы по базам данных с собеседований

## Общие

1. Что такое реляционная база данных?

    <details>
      <summary>Ответ</summary>
      Реляционная база данных — это набор данных с предопределенными связями между ними. Эти данные организованны
      в виде набора таблиц, состоящих из столбцов и строк. В таблицах хранится информация об объектах, представленных
      в базе данных. В каждом столбце таблицы хранится определенный тип данных, в каждой ячейке — значение атрибута.
      Каждая строка таблицы представляет собой набор связанных значений, относящихся к одному объекту или сущности.
    </details>

1. Что такое таблица, кортеж? Что такое primary key?

    <details>
      <summary>Ответ</summary>
      Таблица — это набор элементов данных (значений), использующий модель вертикальных столбцов
      (имеющих уникальное имя) и горизонтальных строк. Таблица содержит определенное число столбцов, но может иметь
      любое количество строк.
      Каждая строка однозначно определяется одним или несколькими уникальными значениями,
      которые принимают её ячейки из определенного подмножества столбцов. Подмножество столбцов,
      которое уникально идентифицирует строку, называется первичным ключом(primary key).
      
      - Primary key не позволяет создавать одинаковые записи (строки) в таблице;
      - PK обеспечивают логическую связь между таблицами одной базы данных.
      
      По соглашению Rails предполагает, что для первичного ключа используется столбец _id_ в таблице,
      который автоматически создается для каждой вашей записи.
      
      **Кортеж** - это набор именованных значений заданного типа.
      
      ![Наглядный пример](http://citforum.ru/pictures/it/osbd/img00005.gif)
    </details>

1. Как реализованы связи между таблицами? Что такое foreign key?

    <details>
      <summary>Ответ</summary>
      Между двумя или более таблицами базы данных могут существовать отношения подчиненности. Отношения подчиненности
      определяют, что для каждой записи главной таблицы может существовать одна или несколько записей в подчиненной таблице.
      
      Существует три разновидности связей между таблицами базы данных:
      
      * «один-ко-многим»,
      
      * «один-к-одному»,
      
      * «многие-ко-многим».
      
      Внешний ключ **Foreign key**, кратко FK. Обеспечивает однозначную логическую связь, между таблицами одной БД.
      Для обеспечения ссылочной целостности в дочерней таблице создается внешний ключ. Во внешний ключ входят
      поля связи дочерней таблицы. Для связей типа "один-ко-многим" внешний ключ по составу полей должен совпадать
      с первичным ключом родительской таблицы.
      
      Например, есть две таблицы А и В. В таблице А (обувь), есть первичный ключ: размер,
      в таблице В (цвет) должна быть колонка с названием размер. В этой таблице «размер»
      это и будет внешний ключ для логической связи таблиц В и А.
      
      По соглашению Rails предполагает, что столбец, используемый для хранения внешнего ключа в этой модели, имеет имя модели с добавленным суффиксом _id_
    </details>

1. Как работает SELECT оператор?

    <details>
      <summary>Ответ</summary>
      SELECT - оператор запроса, возвращающий набор данных (выборку) из базы данных.
      
      Оператор SELECT состоит из нескольких предложений (разделов):
      
      Сам **SELECT** определяет список возвращаемых столбцов (как существующих, так и вычисляемых), их имена,
      ограничения на уникальность строк в возвращаемом наборе, ограничения на количество строк в возвращаемом наборе;
      
      **FROM** задаёт табличное выражение, которое определяет базовый набор данных для применения операций, определяемых
      в других предложениях оператора;
      
      **WHERE** задает ограничение на строки табличного выражения из предложения FROM;
      
      **GROUP BY** объединяет ряды, имеющие одинаковое свойство с применением агрегатных функций
      
      **HAVING** выбирает среди групп, определенных параметром GROUP BY
      
      **ORDER BY** задает критерии сортировки строк; отсортированные строки передаются в точку вызова.
      
      Синтаксис оператора SELECT:
      
      ```sql
      SELECT <column_list> 
      FROM <table_name> 
      [WHERE <условие>] 
      [GROUP BY <условие>] 
      [HAVING <условие>] 
      [ORDER BY <условие>] 
      ```
    </details>

1. Какие бывают виды JOIN? Как каждый работает?

    <details>
      <summary>Ответ</summary>
      INNER JOIN - оператор внутреннего соединения, соединяет две таблицы. Выбираются только совпадающие данные из
      объединяемых таблиц. 
      
      OUTER JOIN - существует два типа внешнего объединения: LEFT OUTER JOIN и RIGHT OUTER JOIN. 
      Работают они одинаково, разница заключается в том, что LEFT - указывает, что "внешней" таблицей будет находящаяся
      слева, а RIGHT - справа. Выбираются все данные из внешней таблицы + совпадения из второй таблицы.
      
      Cross/Full Join - FULL JOIN возвращает объединение объединений LEFT и RIGHT таблиц, комбинируя результат двух запросов.
      CROSS JOIN возвращает перекрестное объединение двух таблиц. Результатом будет выборка всех записей первой таблицы
      объединенная с каждой строкой второй таблицы. Важным моментом является то, что для кросса не нужно указывать
      условие объединения.
      
      ![Наглядный пример](https://zametkinapolyah.ru/wp-content/uploads/2016/07/type-join.png)
    </details>

1. Как работают INSERT, UPDATE, DELETE операторы?

    <details>
      <summary>Ответ</summary>
      INSERT — оператор, который позволяет добавить строки в таблицу, заполняя их значениями.
      Значения можно вставлять перечислением с помощью слова values и перечислив их в круглых скобках через запятую или
      оператором SELECT.
      
      Синтаксис:

      ```sql
      INSERT INTO table_name (column1, column2, column3, ...)
      VALUES (value1, value2, value3, ...);
      ```
      
      UPDATE — оператор, позволяющий обновить значения в заданных столбцах таблицы.
      
      Синтаксис:

      ```sql
      UPDATE table_name
      SET column1 = value1, column2 = value2, ...
      WHERE condition;
      ```
      
      DELETE — операция удаления записей из таблицы. Критерий отбора записей для удаления определяется выражением WHERE.
      В случае, если критерий отбора не определён, выполняется удаление всех записей.
      
      Синтаксис:

      ```sql
      DELETE FROM table_name WHERE condition;
      ```

    </details>

1. Что такое индексы? Для чего используются? Плюсы, минусы?

    <details>
      <summary>Ответ</summary>
      Индекс — объект базы данных, создаваемый с целью повышения производительности поиска данных. Таблицы в базе
      данных могут иметь большое количество строк, которые хранятся в произвольном порядке, и их поиск по заданному
      критерию путём последовательного просмотра таблицы строка за строкой может занимать много времени.
      Индекс формируется из значений одного или нескольких столбцов таблицы и указателей на соответствующие строки
      таблицы и, таким образом, позволяет искать строки, удовлетворяющие критерий поиска.
      
      Ускорение работы с использованием индексов достигается в первую очередь за счёт того, что индекс имеет структуру,
      оптимизированную под поиск.
      
      Для оптимальной производительности запросов индексы обычно создаются на тех столбцах таблицы,
      которые часто используются в запросах.  Однако, увеличение числа индексов замедляет операции добавления,
      обновления, удаления строк таблицы, поскольку при этом приходится обновлять сами индексы. Кроме того, индексы
      занимают дополнительный объем памяти.
    </details>

1. Какие виды индексов бывают?
    <details>
      <summary>Ответ</summary>
      
      "Золотое правило индексирования" — иметь индекс под каждый запрос.
      #### По порядку сортировки
      **Упорядоченные**  — индексы, в которых элементы поля(столбца) упорядочены.
      
      * Возрастающие
      
      * убывающие
      
      **Неупорядоченные** — индексы, в которых элементы неупорядочены.
      
      #### По источнику данных
      * Индексы по представлению (view)
      
      * Индексы по выражениям (например, в PostgreSQL)
      
      #### По воздействию на источник данных
      * Некластерный индекс
      
      * Кластерный индекс
      
      #### По структуре
      
      * B-деревья
      
      * B+-деревья
      
      * B*-деревья
      
      * Хеши
      
      #### По количественному составу
      * Простой индекс (индекс с одним ключом)
      
      * Главный индекс (индекс по первичному ключу)
      
      #### По характеристике содержимого
      
      * Уникальный индекс
      
      * Разреженный индекс (NoSQL)
      
      * Пространственный индекс
      
      * Составной пространственный индекс
      
      * Полнотекстовый (инвертированный) индекс
      
      * Хэш-индексы
      
      * Битовый индекс (bitmap index)
      
      * Обратный индекс (inverse index)
      
      * Функциональный (function-based) индекс (индекс по вычисляемому полю)
     
      * Первичный индекс
      
      * Вторичный индекс
      
      * XML-индекс
      
      #### По механизму обновления
      
      * Полностью перестраиваемый
      * Пополняемый (балансируемый)
      
      #### По покрытию индексируемого содержимого
      
      * Полностью покрывающий (полный) индекс
      
      * Частичный (partial) индекс
      
      * Инкрементный (Delta) индекс
      
      * Real-time индекс
      
      #### Индексы в кластерных системах
      
      * Глобальный индекс
      
      * Сегментный индекс
      
      * Локальный индекс
      
      http://tokarchuk.ru/2012/08/indexes-classification/
    </details>
1. Что такое полнотекстовый поиск?
1. Что такое транзакции?
    <details>
      <summary>Ответ</summary>
      
      Транза́кция — группа последовательных операций с базой данных, 
      которая представляет собой логическую единицу работы с данными.
      Транзакция может быть выполнена либо целиком и успешно (**Commit**),
      соблюдая целостность данных и независимо от параллельно идущих других транзакций,
      либо не выполнена вообще (**Rollback**), и тогда она не должна произвести никакого эффекта.
      
      https://ru.wikipedia.org/wiki/Транзакция_(информатика)
      
    </details>
1. Расскажите об уровнях изолированности транзакции
    <details>
      <summary>Ответ</summary>
      
      **Уровень изолированности транзакций** — условное значение,
      определяющее, в какой мере в результате выполнения логически параллельных транзакций в СУБД
      допускается получение несогласованных данных. Шкала уровней изолированности транзакций
      содержит ряд значений, проранжированных от наинизшего до наивысшего;
      более высокий уровень изолированности соответствует лучшей согласованности данных, 
      но его использование может снижать количество физически параллельно выполняемых транзакций.
      
      #### Проблемы параллельного доступа с использованием транзакций
      
      При параллельном выполнении транзакций возможны следующие проблемы:
      
      * потерянное обновление (англ. lost update)
      
      * «грязное» чтение (англ. dirty read)
      
      * неповторяющееся чтение (англ. non-repeatable read)
      
      * фантомное чтение (англ. phantom reads)
      
      #### Уровни изоляции
      
      Под «уровнем изоляции транзакций» понимается степень обеспечиваемой внутренними механизмами СУБД
      (то есть не требующей специального программирования) защиты от всех или некоторых видов
      вышеперечисленных несогласованности данных, возникающих при параллельном выполнении транзакций.
      
      Первый из них является самым слабым, последний — самым сильным,
      каждый последующий включает в себя все предыдущие.
      
      * Read uncommitted (чтение незафиксированных данных)
      * Read committed (чтение фиксированных данных)
      * Repeatable read (повторяемость чтения)
      * Serializable (упорядочиваемость)
      
      https://ru.wikipedia.org/wiki/Уровень_изолированности_транзакций
      
    </details>
1. Что такое блокировочные и версионные СУБД?
1. Что такое репликация, для чего нужна?
    <details>
      <summary>Ответ</summary>
      
      Репликация — одна из техник масштабирования баз данных. 
      Состоит эта техника в том, что данные с одного сервера базы данных постоянно копируются (реплицируются)
      на один или несколько других (называемые репликами). 
      Для приложения появляется возможность использовать не один сервер для обработки всех запросов, а несколько. 
      Таким образом появляется возможность распределить нагрузку с одного сервера на несколько.
      
      Существует два основных подхода при работе с репликацией данных:
      
      * Репликация Master-Slave;
      * Репликация Master-Master.
      
      https://highload.today/replikatsiya-dannykh/
      
    </details>

1. Что такое шардинг (партиционирование)?
    <details>
      <summary>Ответ</summary>
      
      Шардинг (иногда шардирование) — это другая техника масштабирования работы с данными. 
      Суть его в разделении (партиционирование) базы данных на отдельные части так, 
      чтобы каждую из них можно было вынести на отдельный сервер. 
      Этот процесс зависит от структуры Вашей базы данных и выполняется прямо в приложении в отличие от репликации:
    
      **Вертикальный шардинг**
      
      Вертикальный шардинг — это выделение таблицы или группы таблиц на отдельный сервер. 
      
      **Горизонтальный шардинг**
      
      Горизонтальный шардинг — это разделение одной таблицы на разные сервера. 
      Это необходимо использовать для огромных таблиц, которые не умещаются на одном сервере.
      
      https://highload.today/sharding-i-replikatsiya/
      
    </details>

1. Типичные bottle necks?
1. Объяснить разницу между SQL Injection and CSS Injection?
1. Что такое BETWEEN?

    <details>
      <summary>Ответ</summary>
      `BETWEEN` задает диапазон запроса, в котором будет осуществляться проверка условия. `BETWEEN` извлекает значения, 
      которые попадают в определённый набор. Часто используется для получения значений между двумя датами или числами, 
      и используется в запросах с WHERE, например BETWEEN min AND max.
    </details>
  
1. Чем Like отличается от Ilike?
1. Чем Having отличается от Where?
	
    <details>
      <summary>Ответ</summary>
      `Where` фильтрует строки.
      
      `Having` фильтрует группы (например, сначала группировка с применением `Group by`, а затем уже выборка по условию с применением `Having`).
      Пример можно посмотреть здесь: http://sql-tutorial.ru/ru/book_having_clause.html
    </details>

1. Что такое нормализация и денормализация базы данных?

    <details>
      <summary>Ответ</summary>
      Нормализация — процесс преобразования отношений базы данных к виду, отвечающему нормальным формам.

      Нормальные формы — это рекомендации по проектированию баз данных.

      Для нормализации необходимо упорядочить данные в группы и найти логические связи между этими группами данных.

      Денормализация — намеренное приведение структуры базы данных в состояние, не соответствующее критериям нормализации, обычно проводимое с целью ускорения операций чтения из базы за счет добавления избыточных данных.
      
      https://office-menu.ru/uroki-sql/51-normalizatsiya-bazy-dannykh
      https://oracle-patches.com/db/3632-нормализация-и-денормализация-базы-данных-нормальные-формы
    </details>

1. Основная причина, по которой Redis работает быстрее PostgreSQL?

    <details>
      <summary>Ответ</summary>
      Причина в месте хранения данных. В Redis данные хранятся в оперативной памяти, в PostgreSQL на жёстком диске.

      https://ru.wikipedia.org/wiki/Redis
      
    </details>

1. Приложение, базу, сервер не трогали - но спустя какое-то время запрос стал работать медленнее. Почему?

    <details>
      <summary>Ответ</summary>
      
      При выполнении запроса пишется статистика, которая содержит статистические характеристики по запросу. Если она забьется, или превысит какой-то порог - то запрос будет выполняться медленнее из-за большого разброса статистичеких значений. Индексы не помогут, и будут отбрасываться.
    </details>
    
1. Что такое журнал транзакций SQL?
    <details>
      Журнал транзакций SQL - это файл, содержащий журналы, которые были созданы в процессе регистрации транзакций, произошедших в базе данных.
      
      Журналы транзакций SQL являются последовательными по своей природе и могут быть разделены на куски, называемые виртуальными файлами журналов.
      
      Журнал транзакций SQL поддерживает следующее:
      
      * Восстановление незавершенных транзакций.
      * Rollback SQL транзакции.
      * Высокая доступность.
      * Восстановление БД
      
      Резервное копирование журнала транзакций - это не что иное, как резервное копирование всех транзакций базы данных, произошедших со времени последнего резервного копирования журнала транзакций. Эти резервные копии могут быть выполнены в полном и инкрементальном режимах.
      
    </details>

Где искать ответы:

* https://www.pgexercises.com — тренажер для написания запросов
* https://sqlzoo.net/
* https://sqlbolt.com/
* http://sql-tutorial.ru/sqlbook/ru

## PostgreSQL

Вопросы:

1. pgBouncer — что это и зачем нужно?
    <details>
    
      <summary>Ответ</summary>
      
      **pgbouncer** — это пул соединения для PostgreSQL. 
      Любое приложение может подключаться к pgbouncer так,
      как будто это сервер PostgreSQL, и  pgbouncer  будет создавать соединения к действующему серверу PostgreSQL или
      переиспользовать существующие соединения.
      
      Главная цель pgbouncer это снизить потери производительности при создании новых соединений (новых процессов) к PostgreSQL.
      
      pgbouncer поддерживает несколько типов создания новых соединений и переиспользования существующих соединений:
      
      **Пул сессий (Session pooling)**
      
      **Пул транзакций. (Transaction pooling)**
      
      **Пул операторов (Statement pooling)**
      
      http://evtuhovich.ru/blog/2012/02/12/pgbouncer/
      
      http://pgbouncer.ru/usage/
      
      https://postgrespro.ru/docs/postgrespro/10/pgbouncer
      
    </details>
1. Системы репликации, что это и зачем нужно?
1. PgQ (другие очереди)?
    <details>
      <summary>Ответ</summary>

      PgQ — это еще одна система очередей, написаная skytools на базе PostgreSql. 
      Если написать руками очередь на БД, то она будет работать медленно и создавать большую нагрузку. 
      В PgQ удалось избежать этого за счет использования «особой PostgreSql магии». 
      PgQ — транзакционная очередь, что гарантирует, что вы увидите каждой событией хотя бы один раз.

      Особенностью PgQ является то, что события из нее достаются пачками (batch). 
      Поэтому надо быть внимательным, чтобы не отреагировать на одно и то же событие несколько раз
      (например, если обработчик событий аварийно завершился, перед выходом стоит все необработанные события
      отправить на повтор и закрыть пакет).
      
      </details>
1. Что такое синхронные и асинхронные операции?
1. Как устроены и функционируют индексы PostgreSQL?
    <details>
      <summary>Ответ</summary>

       https://habr.com/ru/company/mailru/blog/261871/
    </details>

1. Как воплощён и работает механизм транзакций в PG?
    <details>
      <summary>Ответ</summary>
      
      Транзакция откатывается по явному `ROLLBACK TRANSACTION` или закрывается по явному `COMMIT TRANSACTION`. Если ни то, ни другое не было вызвано, транзакция будет продолжать висеть открытой. Посмотреть висячие транзакции можно командой `DBCC OPENTRAN`.
      
      https://postgrespro.ru/docs/postgresql/9.6/sql-rollback-prepared
    </details>


Где искать ответы:

* https://www.codecademy.com/learn/learn-sql
* http://2sql.ru/
