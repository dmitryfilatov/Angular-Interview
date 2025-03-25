# Вопросы с ответами для собеседования по Angular.

## Содержание


<details>
	<summary>Вопросы по архитектуре</summary>
	- <a href="answers/architecture.md#what-is">Зачем нужен NgModule?</a> <br/>
    - <a href="answers/architecture.md#lazy-load">Что такое ленивая загрузка модулей?</a> <br/>
    - <a href="answers/architecture.md#di">Что такое внедрение зависимостей?</a> <br/>
    - <a href="answers/architecture.md#service">Что такое сервис?</a> <br/>
    - <a href="answers/architecture.md#srp">В чём заключается принцип единственной ответственности?</a> <br/>
	- <a href="answers/architecture.md#dip"><b>В чём заключается принцип инверсии зависимостей?</b></a> <br/>
    - <a href="answers/architecture.md#di_hierarhy"><b>Кратко опишите иерархию инжекторов в Angular</b></a> <br/>
    - <a href="answers/architecture.md#di_rereg"><b>В чём заключается принцип переопределения зависимостей?</b></a> <br/>
</details>

<details>
	<summary>Вопросы по компонентам</summary>
    - <a href="answers/component.md#what-is">Что такое компонент?</a> <br/>
    - <a href="answers/component.md#input_output">Для чего используются декораторы @Input()и @Output()?</a> <br/>
    - <a href="answers/component.md#idestroy">Когда уничтожается компонент?</a> <br/>
    - <a href="answers/component.md#idestroy_what">Что происходит при удалении компонента?</a> <br/>
    - <a href="answers/component.md#emit">Какие компоненты будут оповещены о том, что был emit события?</a> <br/>
</details>

<details>
	<summary>Вопросы по шаблонам</summary>
    - <a href="answers/template.md#ngif">Как реализовать условный рендеринг в шаблоне?</a> <br/>
    - <a href="answers/template.md#var">Что такое переменная шаблона?</a> <br/>
    - <a href="answers/template.md#ng_container">В чем различия ng-content и ng-container?</a> <br/>
    - <a href="answers/template.md#bind_attr">Можно ли в шаблоне делать привязку к артибутам?</a> <br/>
    - <a href="answers/template.md#compile_template"><b>Как Angular компилирует шаблон компонента?</b></a> <br/>
    - <a href="answers/template.md#compile_types"><b>Какие бывают виды компиляции шаблона?</b></a> <br/>
</details>

<details>
	<summary>Вопросы по RxJs</summary>
    - <a href="answers/rxjs.md#http">Как делать HTTP-запросы в Angular?</a> <br/>
    - <a href="answers/rxjs.md#observable">Что такое наблюдаемый объект (Observable)?</a> <br/>
    - <a href="answers/rxjs.md#promise_observable">В чем разница между Promise и Observable?</a> <br/>
    - <a href="answers/rxjs.md#unsubscribe">Как можно отменить подписку на Observable?</a> <br/>
    - <a href="answers/rxjs.md#cold_observable">Что такое холодный наблюдаемый объект?</a> <br/>
    - <a href="answers/rxjs.md#cold_observable_example">Приведите пример холодного наблюдаемого объекта в Angular</a> <br/>
    - <a href="answers/rxjs.md#hot_observable">Что такое горячий наблюдаемый объект?</a> <br/>
    - <a href="answers/rxjs.md#cold_to_hot">Как преобразовать холодный наблюдаемый объект в горячий?</a> <br/>
    - <a href="answers/rxjs.md#observable_subject">В чем разница между Observable и Subject?</a> <br/>
    - <a href="answers/rxjs.md#behaviorsubject">Что такое BehaviorSubject и в чем его основное отличие от Subject?</a> <br/>
    - <a href="answers/rxjs.md#replay_behavior">Чем ReplaySubject отличается от BehaviorSubject?</a> <br/>
    - <a href="answers/rxjs.md#concat">Как реализовать несколько разных последовательных HTTP-запросов?</a> <br/>
    - <a href="answers/rxjs.md#usecase"><b>Как реализовать следующий сценарий?</b></a> <br/>
</details>

<details>
	<summary>Вопросы по управлению состоянием</summary>
    - <a href="answers/state.md#cache">Как кэшировать данные в Angular?</a> <br/>
    - <a href="answers/state.md#ngrx">Что такое NgRx?</a> <br/>
    - <a href="answers/state.md#ngxs">Что такое NGXS?</a> <br/>
</details>

<details>
	<summary>Вопросы по формам</summary>
    - <a href="answers/forms.md#react_default">В чем разница между реактивными формами и формами на основе шаблонов?</a> <br/>
</details>

<details>
	<summary>Вопросы по тестированию</summary>
    - <a href="answers/tests.md#performance">Как протестировать производительность приложения?</a> <br/>
</details>

<details>
	<summary>Вопросы по анимации</summary>
	- <a href="answers/animations.md#transition">Как определяется переход между двумя состояниями в Angular?</a> <br/>
	- <a href="answers/animations.md#wildcard">Что такое состояние wildcard?</a> <br/>
	- <a href="answers/animations.md#trigger">Что такое триггер анимации?</a>
</details>

<details>
	<summary>Вопросы по развертыванию</summary>
	- <a href="answers/build.md#how_build">Как собирается Angular- приложение?</a> <br/>
    - <a href="answers/build.md#how_webpack">Что делает Webpack?</a> <br/>
    - <a href="answers/build.md#load_browser">Как Angular-приложение загружается в браузер?</a> <br/>
    - <a href="answers/build.md#what_bundles">Что собой представляют бандлы и зачем они нужны?</a> <br/>
    - <a href="answers/build.md#what_package">Для чего нужен файл package.json?</a> <br/>
</details>


<details>
	<summary>Вопросы по TypeScript</summary>
    - <a href="answers/typescript.md#type">Что такое псевдоним типа?</a> <br/>
	- <a href="answers/typescript.md#interface_type">В чём отличие interface от type?</a> <br/>
    - <a href="answers/typescript.md#class_type">В чём отличие class от type?</a> <br/>
    - <a href="answers/typescript.md#type_intersection">Что такое пересечение типов?</a> <br/>
    - <a href="answers/typescript.md#override_function">Есть ли в TypeScript перегрузка функций?</a> <br/>
    - <a href="answers/typescript.md#this">Как в TypeScript определить на какой тип указывает this внутри функции?</a> <br/>
    - <a href="answers/typescript.md#annotationthis">Когда нужно и когда не нужно применять аннотацию типов?</a> <br/>
    - <a href="answers/typescript.md#struct_typing">Что такое структурная типизация?</a> <br/>
    - <a href="answers/typescript.md#unknown">Что такое тип unknown и для чего он используется?</a> <br/>
    - <a href="answers/typescript.md#rest_types">Что такое остаточные типы?</a> <br/>
    - <a href="answers/typescript.md#spread">Что такое оператор распространения?</a> <br/>
    - <a href="answers/typescript.md#namespaces">Чем пространство имён типов отличается от пространства имён значений?</a> <br/>
    - <a href="answers/typescript.md#symbol">Для чего используется тип symbol?</a> <br/>
 </details>