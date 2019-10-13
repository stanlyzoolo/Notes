  # Архитектурный стиль, архитектурный паттерн, паттерн проектирования

**Архитектура программного обеспечения** (Software Architecture) - набор структур, необходимый для рассуждения о системе, содержащий элементы ПО, связи между ними и их свойства.

**Архитектор** — один из опытнейших программистов в команде, умеющий анализировать высокоуровневые проблемы и их решения.  

Каждый программист при написании кода вносит свой вклад в архитектуру приложения, и важно понимать, как это делать.

Важно понимать, что не существует универсальных решений для всех приложений: все они имеют свои сильные и слабые стороны. Подобрать хорошую архитектуру можно только при условии хорошего понимания требований приложения. Иногда не подходит ни одна существующая архитектура. Так появляются новые.

> Some architectural styles are often portrayed as ‘silver bullet’ solutions for all forms of software. However, a good designer should select a style that matches the needs of the particular problem being solved. 
**Roy Fielding, 2000**

Понятия *архитектурный стиль*, *архитектурный паттерн* и *паттерн проектирования не взаимоисключающие* (not mutually exclusive), а *взаимодополняющие* (complementary). Они отличаются своей областью применения (scope).

## Архитектурный стиль

**Архитектурный стиль** (Architectural Style) в общих чертах указывает, как организовать код в проекте. Это наивысший уровень детализации (granularity), абстракции (abstraction), на котором определяются слои, модули высшего порядка приложения и их отношения, взаимодействия друг с другом.

Архитектурные стили не привязаны к конкретной реализации.

### Примеры архитектурных стилей
* Компонетный (component-based)
* Монолитный (monolithic)
* Многослойный (layered)
* Событийный (event-driven)
* Клиент-серверный (client-server)
* Сервис-ориентированный (service-oriented)

## Архитектурный паттерн

**Паттерн, шаблон** — типичное решение широко распространённой проблемы. Отличается от *алгоритма* тем, что не содержит чёткой последовательности действий, а описывает общую концепцию (идею) решения, реализации которой могут сильно отличаться.

Паттерны следует использовать только при необходимости, в противном случае они могут лишний раз усложнить код.

**Архитектурный паттерн** (Architectural Pattern) решает проблемы, связанные с архитектурными стилями.

### Примеры проблем, которые решают архитектурные паттерны
* Как много уровней (tiers) будет в наше клиент-серверной архитектуре? Как они будут взаимодействовать?
* Какие модули высшего уровня будут в нашей сервис-ориентированной архитектуре?

### Примеры архитектурных паттернов
* MVC (Model-View-Controller)
* EBI (Entity-Boundary-Interactor)
* Трёхуровневый (three-tier)

## Паттерн проектирования

**Паттерн проектирования** (Design Pattern) решает какую-то локальную проблему в проекте, затрагивая лишь конкретный блок кода, но не весь код проекта целиком.

### Примеры проблем и решающих их паттернов проектирования
* Нужно за чем-то проследить в приложении и отреагировать соотвествующем образом (например, показать уведомление при появлении пользователя в сети) — поведенческий паттерн "Наблюдатель".
* Нужно написать простой интерфейс для работы со сложной системой, библиотекой, API н структурный паттерн "Фасад".

# Поддерживаемый код

Наличие **поддерживаемого кода** (maintainable code base) означает возможность применения максимума концептуальных изменений с минимальным изменением кода, то есть изменение одного блока кода должно оказывать минимально возможное влияние на другие блоки. В таком случае изменения делаются проще и быстрее, а баги появляются реже.

**Связность** (coupling) отражает зависимость блоков кода друг от друга. Два блока кода **сильно связны** (highly coupled), если изменения в одном блоке порождают изменения в другом, **слабо связны** (loosely coupled), если один блок не зависит или почти не зависит от изменений другого. 

**Сплочёность** (cohesion) отражает, насколько тесно связаны по смыслу функции одного модуля. **Низкая сплоченность** (low cohesion) характерна модулям, имеющим разные несвязнные обязанности, **высокая сплочёность** (high cohesion) — модулям, функции которых выполняют во многом похожие задачи.

### Основные принципы поддерживаемого кода
1) *Инкапсуляция* (encapsulation). Процесс сокрытия внутренних деталей реализации.  
2) *Слабая связность* (low coupling). Достигается за счёт выбора правильного интерфейса.  
3) *Высокая сплочёность* (high cohesion).

Выполнение этих принципов концептуально изолирует код, делая его хорошо читаемым, тестируемым и переиспользуемым.

# Архитектурные паттерны

## MVC (1979)
В 1970-ых обязанности не разделялись: смешивание HTML, CSS и работы с базой данных считалось нормальной практикой. С ростом таких приложений становилось понятно, что они очень запутанны и их невозможно поддерживать (тратится слишком много ресурсов), поэтому нередко разросшиеся приложения приходилось переписывать с нуля.

В 1979 появился архитектурный шаблон **MVC** (Model-View-Controller), попытавшийся разрешить проблему, продвигая идею **разделения ответственности** (separation of concerns, SoC) между бэкендом и фронтендом, UI и бизнес-логикой.

**Бизнес-логика** (business logic, domain logic) — часть приложения, задающая бизнес-правила, определяющие, как данные (состояние, state) предметной области (domain) приложения создаются, хранятся и изменяются.

MVC разделяет приложение на 3 концептуальные единицы
* **Модель** (Model) представляет бизнес-логику (данные и правила, методы работы с ними) приложения; не содержит информации, как отобразить данные.
* **Представление** (View) — UI-компонента (кнопка, поле для ввода и прочее); то, что пользователь видит и с чем взаимодействует.
* **Контроллер** (Controller) выступает координатором между View и Model: решает, какие Views показывать и с какими данными, переводит действия пользователя (например, клик по кнопке) в бизнес-логику.

Модель может быть представлена объектом или структурой объектов.

### Особенности MVC  
1) View использует объекты данных напрямую из Model, чтобы эти данные отобразить.  
2) Когда данные в Model меняются, срабатывает событие, немедленно обновляющее View.  
3) Один View обычно привязан к одному Controller.  
4) Каждый экран может иметь несколько пар View-Controller.  
5) Controller может быть связан с несколькими Views. 

### Проблема MVC
Когда MVC прявился, HTTP ещё не было. Сейчас же при попытке описать полноценное приложение (HTTP-клиент + HTTP-сервер) понятно, что подлинный MVC работать не сможет: при обновлении данных в БД клиент не получает данные напрямую, а делает это по запросу к серверу (через Controller). Это можно решить при помощи веб-сокетов, но не всегда есть в этом необходимость

## Иерархический MVC (2000), PAC (1987)

**HMVC** (Hierarchical MVC) увеличивает модульность в контексте виджетизации UI-блоков.

Существует мнение, что авторы HMVC переосмыслили другой паттерн: **PAC** (Presentation-Abstraction-Control).

HMVC разбивает уроверь клиента (client tier) на иерархию из MVC-слоёв. Это называется **проектированием клиентского уровня** (client-tier architecture) и должно увеличивать масштабируемость приложения: каждый MVC-слой независим от других и может работать при отсутствии любого другого.

Controller, обрабатывающий основной запрос, пересылает подзапросы другим Controllers, чтобы получить рендеринг виджетов и включить их в рендеринг основного View.

## MVP (1996)

*MVC* был хорош для приложений своего времени, но приложения выросли и настало время изменений.

**MVP** (Model-View-Presenter) видоизменяет MVC, разделяя View и Model и осуществляя их коммуникацию только через **Presenter**.

*Presenter* также называют **Supervisor Controller**.

### Особенности MVP 
1) View пассивен (passive) и ничего не знает о Model. 
2) Presenter не содержит бизнес-логики, он просто вызывает методы Model, а затем передаёт необходимые данные во View.  
3) Только один Presenter для каждого View.  
4) Изменение данных в Model не вызывает немедленное обновление View: событие всегда проходит через Presenter, что позволяет в нём перед обновлением View проделывать дополнительную логику, связанную с представлением.

## MVVM (2005)
  
Сложность приложений продолжала расти и снова появилась необходимость изменений.

**MVVM** (Model-View-ViewModel) призван разделить UI-дизайн и бизнес-логику таким образом, чтобы за них могли отвечать разные люди, использующие разные технологии для этих целей.

### Особенности MVVM
1) Один ViewModel соответствует только одному View и наоборот.
2) Вся логика из View перемещается во ViewModel, чтобы упростить View и позволить ему выполнять свою задачу (визуализация).
3) Отношение один к одному установлено между данными во View и данными во ViewModel.
4) Изменение данных во ViewModel вызывает немедленное обновление View.

## EBI (1992)

Архитектурный шаблон **Entity-Boundary-Interactor** (EBI) был опубликован Иваром Якобсоном в одной из серии книг об объектно-ориентированной разработке ПО.

Изначально автор назвал архитектуру Entity-Interface-Control, но затем переименовал для понимания, что Interface не связан с одноимённой конструкцией в языках программирования, а Control не связан с Controller в MVC.

**Entity-объекты** содержат данные системы и всю логику, напрямую связанную с этими данными (такую логику, которая при внесении изменений в Entity тоже должна изменяться; меняется структура — меняются методы работы с ней).

**Boundary-объекты** содержат в себе весь функционал, касающийся интерфейса системы (системного окружения).
 
Любое взаимодействие с системой происходит через Boundary. Действующее лицо (actor) может быть не только человеком, но и другим устройсвом или сторонним API.

Антипаттерн: Entity содержит лишь данные, всё поведение выносится в Boundary. 

**Interactor-объекты** содержат поведение, не вошедшее в Boundary и Entity (обычно это операции над несколькими Entity, результат  которых возвращается в Boundary; похоже на сервисы).

*Interactors* важны, поскольку они содержат специфическую логику для конкретных *Boundaries*, в то время как *Entity* содержит общую (generic) логику для всех *Boundaries*. В случае, если вся логика будет храниться в *Entity*, некоторые *Boundaries* будут иметь доступ к тому, к чему не должны, что увеличивает сложность и может привести к ошибкам.

Обычные объектно-ориентированные методологии помещают все обязанности в одну сущность, не разделяя их между тремя описанными типами объектов, но автор книги считает, что такое разделение (инкапсуляция) обязанностей позволяет сделать систему более гибкой к изменениям, которые в этом случае становятся локальными: изменяется только один объект системы.

### Сравнение EBI и MVC
Так же, как в MVC Model представляет весь бэкенд (все сущности, сервисы и их связи), EBI представляет Boundary как одно целостное соединение с окружающим миром. Boundary представляет весь уровень представления, который соответствует Model и Controller в совокупности в MVC. Entities являются физическими сущностями, хранящими данные вместе со своим поведением. Interactors связывают уровень представления и Entities вместе.

MVC и EBI не заменяют, а дополняют друг друга.  
При их совместном использовании получился бы паттен View-Controller-Interactor-Entity.

## Пакеты

Слово "**функциональный** (functional; блок кода, метод, класс и тд) отражает чисто техническую роль в приложении, оно не связано с предметной областью. Примеры функционального: слой (layer), фабрика (factory), View.

Слово "**концептуальный**" (conceptual; блок кода, метод, класс и тд) отражает бизнес-роль в приложении, оно напрямую связано с предметной областью (domain). Примеры концептуального: User, Article, Comment, Like.

Одна и та же вещь в зависимости от того, с какой стороны на неё смотреть, может быть функциональной и концептуальной одновременно.

**Пакет** — сгруппированный набор классов.  
**Модуль** — функциональный пакет.  
**Компонента** — концептуальный пакет.

<!-- **Приложение** — UI, представленный набором компонент. -->

Описанные принципы написания поддерживаемого кода часто применяются к отдельным классам, но также и к *пакетам* (*модулям*, *компонентам*). Это позволяет разрабатывать их максимально независимо друг от друга, разделяя обязанности между разными командами разработчиков.

В *хорошо организованном проекте* (well-organised codebase) есть только одно конкретное место, где может лежать какой-то блок кода. 
Можно не знать точное местоположение, но есть только один логический путь, ведущий туда. Это позволяет избежать несогласованности данных, потерянного и дублированного кода, экономит время и нервы разработчиков.

Группируя классы в пакеты по каким-то критериям (концептуально), мы можем рассуждать об организации проекта на высшем уровне абстракции, управляя отношениями между этими пакетами.

## Принципы пакетов

### Принципы сплочёности пакетов (cohesion)
* **Reuse-Release Equivalency (RRE)**. Пакеты должны выпускаться и версионироваться отдельно друг от друга, чтобы всегда можно было выбрать старую версию пакета, если новая не корректно работает.
* **Common-Reuse Principle (CRP)**. Классы в пакете переиспользуются (reuse) вместе. Переиспользуешь один — переиспользуешь все.
* **Common-Closure Principle (CCP)**. Классы, изменяющиеся вместе, должны быть упакованы (packeged) вместе. Чтобы в случае изменений изменялся только один пакет, не затрагивая другие.

### Принципы связности пакетов (coupling)
* **Acyclic-Dependencies Principle (ADP)**. Циклы в графе пакетных зависимостей недопустимы.
* **Stable-Dependencies Principle (SDP)**. Зависимости в направлении стабильности. Часто меняющиеся части системы должны зависеть от редко меняющихся (стабильных), но не наоборот. 
* **Stable-Abstractions Principle (SAP)**. Стабильные пакеты должны быть более абстрактными и содержать те классы и модули, которые можно расширять, а не те, которые должны изменяться. При изменении классов в пакете велика вероятность изменений их использования, а значит и изменений в зависимых пакетах.

# Архитектурные стили

## Монолитная архитектура

Первые приложения были достаточно простыми.  
Изначально они состояли из одного файла, затем из нескольких, но всё ещё достаточно простыми.

## DDD (2003)

Архитектура **Domain-Driven Design** (DDD) предложана Эриком Эвансом.

Идея DDD: при разработке проекта основное внимание должно уделяться основной предметной области и её логике. Для этого нужно тестное сотрудничество между техническими специалистами и экспертами предметной области.

### Единый язык

**Единый, повсеместный, общий  язык** (Ubiquitous language) — общий язык между предметной областью и её технической реализацией. Источником этого языка должна быть предметная область (бизнес).  

Каждая предметная область имеет свои определения, часто встречающиеся в требованиях заказчика, но программисты часто переименовывают многие вещи по-своему, создавая таким образом свою собственную модель предметной области, придумывают свои понятия, которые потом нужно объяснять другим программистам. Так возникают барьеры недопонимания, чего нужно избегать.

Разработка единого языка требует много времени на тщательный анализ требований и консультации с экспертами предметной области, но это позволяет создать внутреннюю базу знаний клиента. 

### Слои в DDD
* **Пользовательский интерфейс** (User Interface) обеспечивает взаимодействие окружающего мира с приложением, преобразуя входные данные в команды приложению (аналогично Boundary в EBI).
* **Слой приложения** (Application Layer) управляет объектами предметной области (Domain Objects), чтобы выполнять приходящие команды — **Случаи использования** (the Use Cases). Не содержит бизнес-логику. На этом слое лежат *Сервисы приложения* (Application Services), являющиеся контейнерами, в которых используются такие объекты предметной области, как Репозитории, Domain-сервисы, Сущности, Value-объекты (аналогично Interactor в EBI, но не все "не Boundary, не Entity" объекты, а только соотвутствующие *Случаям использования*).
* **Слой предметной области** (Domain Layer) содержит всю бизнес-логику. (аналогично Entity в EBI).
* **Инфраструктура** (Infrastructure) содержит технические возможности, которые поддерживают слои выше (например, отправка сообщений).

### Объекты предметной области

**Контекст** (Context) — окружение рассматриваемого объекта, влияющее на его смысл.

**Предметная область** (Domain) — сфера знаний, к которой относится программа.

**Модель** (Model) — система абстракций, описывающая выбранные аспекты предметной области и использующаяся для решения её проблем.

**Сущность** (Entity) — объект, имеющий индивидуальные черты. Имеет уникальный идентификатор (id). Две Сущности считаются разными даже в случае совпадения всех свойств.

Пример Сущности: Несмотря на то, что в кинотеатре все места выглядят одинаково, каждое место имеет свой номер (уникальный идентификатор). Посетитель приходит и садится на место, указанное в его билете. 

**Value-объект** (Value Object) — неизменяемый (immutable) тип объекта, полностью определяемый значениями своих свойств. В отличие от Сущности не имеет уникального идентификатора (id). Два Value-объекта с одинаковыми свойствами считаются идентичными.

Пример Value-объекта: В общественном транспорте все места одинаковы: можно сесть куда угодно, нумерация не имеет значения. 

**Агрегат** (Aggregate) — коллекция объектов, связанных вместе корневой Сущностью — **корнем агрегата** (Aggregate Root). 

Корневой агрегат гарантирует согласованность изменений, вносимых в агрегат, не позволяя внешним объектам хранит ссылки на его элементы. 
Агрегаты можно рассматривать как ограниченный контекст, предоставляющий корневому объекту и всему графу объектов контекст, в котором они используются.

**Репозиторий** — объект, сохраняющий Сущности или Агрегаты в базовый механизм хранения или извлекающий ихиз него.  

Репозиторий является частью модели предметной области (domain model), поэтому он должен быть независим от поставщика (vendor) базы данных.

**Сервис** — объект, содержащий методы (команды), концептуально не привязанные к какому-либо объекту (Entity, Value-объекту). Не имеет состояния (stateless).

### Ограниченный контекст

В корпоративных (enterprise) системах, где работает огромное количество разработчиков, модель может сильно разрастить. Сложно держать всю структуру огромного проекта в голове. Сложно распределять обязанности, когда все работают в одном месте. В этом случае систему обычно разбивают на подсистемы. 

**Ограниченный контекст** (Bounded context) — подсистема в рамках DDD, определяющая контекст применения изолированной части модели.

Изолированность достигается разными способами (например, разделением схемы базы данных на части или разделением обязанностей между программистами по их умениям).  

Хорошее разделение: сильная функциональная связь внутри подсистем и слабая между подсистемами.

### Антикоррупционный слой

**Антикоррупционный слой** — промежуточный слой между двумя подсистемами, заменяющий их взаимодействие друг с другом на взаимодействие с собой; изолирующий подситемы друг от друга. В таком случае при удалении или замене одной из подсистем вторая останется неизменной (изменится только антикоррупционный слой).

Антикоррупционный слой можно использовать, когда одна или обе подсистемы не контролируются, или когда нужно предотвратить утечку из  модели одной системы в другую (изменяем одну подсистему под требования другой).

### Общее ядро

Иногда, несмотря на преимущества изолированности, имеет смысл использовать общий код между несколькими компонентами (чтобы не дублировать его). Компоненты остаются независимыми друг от друга, хотя и используют **общее ядро** (shared kernel). 

Так один компонент может прослушивать событие, запущенное другим копонентом. Другой пример: использование сервиса.

Изменять общее ядро нужно очень осторожно, поскольку оно может сломать сразу несколько компонент.

### Общая подобласть

**Подобласть** (subdomain) — хорошо изолированная часть предметной области (domain).

**Общая подобласть** (generic subdomain) — подобласть, которая не специфична конкретно для приложения, а может использоваться почти в любом другом. (например, рисование статистики, работа с камерой, платёжные методы).

Если в приложении есть общие подобласти, нужно уделять им как можно меньше внимания по сравнению с предметной область. Это не самая важная часть приложения, а если и важная, то не критичная (essential but not crucial). 

Общие подобласти лучше не писать, а устанавливать как сторонние пакеты.

## Кричащая архитектура (2011)

**Кричащая архитектура** (Screaming Architecture) предложена Робертом С. Мартином.  

Архитектура должна чётко показывать, в чём заключается суть системы.  

Первые папки в проекте должны быть связаны с предметной областью, верхним уровнем абстракции (Users, Admins, Messages), но не с названием технологий (mongodb, jwt, redis), не с функциональными блоками (services, controllers, repositories), не с механизмами доставки (http, console, sockets).