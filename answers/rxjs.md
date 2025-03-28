## <a name="http"></a>Как делать HTTP-запросы в Angular?

Использовать HttpClient:

```typescript
 this.http.get('api/url').subscribe(data => console.log(data));
 ```

Для этого нужно проимпортировать HttpClientModule. Обычно запрос возвращает массив сообщений JSON.
<br/>

## <a name="observable"></a>Что такое наблюдаемый объект (Observable)?

Это поток данных, который может выдавать (эмитировать) несколько значений с течением времени. Angular использует observables для асинхронных операций, таких как HTTP-вызовы и обработка событий.
<br/>

## <a name="promise_observable"></a>В чем разница между Promise и Observable?

- Promise: выдает одно значение и не может быть отменен.
- Observable: выдает несколько значений, может быть отменен и поддерживает такие операторы, как map и filter.
<br/>

## <a name="unsubscribe"></a>Как можно отменить подписку на Observable?

С помощью метода unsubscribe. Отписка освобождает ресурсы и предотвращает потенциальные утечки памяти, которые могут возникнуть, если подписка не будет отменена, особенно в ситуациях с долгоживущими потоками, такими как сетевые передачи или события пользовательского интерфейса.

```typescript
ngOnDestroy() {
  // Отмена подписки при уничтожении компонента
  this.subscription.unsubscribe();
}
```
<br/>

## <a name="cold_observable"></a>Что такое холодный наблюдаемый объект?

 - начинает эмиссию данных только в тот момент, когда на него кто-то подписывается
 - каждый подписчик получает полную последовательность данных с начала независимо от других

 ```typescript
import { Observable } from 'rxjs';

// Пример холодного наблюдаемого объекта
const coldObservable = new Observable(subscriber => {
  console.log('Observable executed');
  subscriber.next('Hello');
  subscriber.next('World');
  subscriber.complete();
});

// Подписка 1
coldObservable.subscribe(value => console.log('Subscriber 1:', value));
// Output на консоль:
// "Observable executed"
// "Subscriber 1: Hello"
// "Subscriber 1: World"

// Подписка 2
coldObservable.subscribe(value => console.log('Subscriber 2:', value));
// Output на консоль снова: потому что Observable отдельный
// "Observable executed"
// "Subscriber 2: Hello"
// "Subscriber 2: World"
 ```
<br/>

## <a name="cold_observable_example"></a>Приведите пример холодного наблюдаемого объекта в Angular

Например, HTTP-запрос в Angular, выполненный через HttpClient.

- при каждом HTTP-запросе создаётся Observable, который не начнёт эмитировать данные, пока не будет подписан. 
- если имеется несколько подписчиков на один и тот же HTTP-запрос, каждый из них запустит свой экземпляр этого запроса. Каждый раз при подписке запрос выполняется заново, и каждый подписчик получит результаты от своего вызова.

```typescript
import { HttpClient } from '@angular/common/http';
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html'
})
export class UserComponent implements OnInit {

  constructor(private http: HttpClient) {}

  ngOnInit() {
    // Создание холодного наблюдаемого объекта
    const observable = this.http.get('https://api.example.com/users/1');

    // Первая подписка - отправка HTTP-запроса
    observable.subscribe(response => console.log('Subscriber 1:', response));

    // Вторая подписка - ещё один HTTP-запрос
    observable.subscribe(response => console.log('Subscriber 2:', response));
  }
}
```
<br/>


## <a name="hot_observable"></a>Что такое горячий наблюдаемый объект?

Горячие наблюдаемые объекты (hot observables) начинают эмитировать значения независимо от подписчиков, и когда вы подписываетесь на горячий наблюдаемый объект, вы получаете текущие данные или поток с момента подписки.

Примеры: поток событий от UI или WebSocket соединение.
<br/>

## <a name="cold_to_hot"></a>Как преобразовать холодный наблюдаемый объект в горячий?

Например, с помощью share() или shareReplay().

- share(): Делает данные горячими, что позволяет распределять их между несколькими подписчиками.
- shareReplay(): Делает данные горячими и кэширует последние значения, что позволяет новым подписчикам получать недавно полученные данные без повторного запуска источника.

```typescript
private sharedData$: Observable<any>;

// Холодный объект, превращенный в горячий
this.sharedData$ = this.http.get('/api/data').pipe(
    share()
);
```

```typescript
private sharedData$: Observable<any>;

// Холодный объект, превращенный в горячий и с кэшированием последнего значения
this.sharedData$ = this.http.get('/api/data').pipe(
    shareReplay(1) // Рекомендуется использовать буфер как минимум на 1, чтобы каждый новый подписчик получил последнее значение. 
    // Число 1 указывает, сколько последних значений нужно сохранить и предоставить новым подписчикам. Это число называется "размером буфера".
);
```
<br/>

## <a name="observable_subject"></a>В чем разница между Observable и Subject?

- Observable: подписка получает новую копию данных
- Subject: все подписчики - одни и те же данные

Subject - пример "горячего" наблюдаемого объекта (hot observables). Он является одновременно и Observable, и Observer, и поэтому он позволяет активно транслировать данные нескольким подписчикам.
<br/>

## <a name="behaviorsubject"></a>Что такое BehaviorSubject и в чем его основное отличие от Subject?

Это наблюдаемый объект, который сохраняет последнее переданное ему значение и предоставляет его всем новым подписчикам сразу же после подписки — даже если это значение было передано до того, как подписчик подписался. Это основное отличие его от простого Subject, который не хранит предыдущие значения.

Он полезен в тех случаях, когда получаемое подписчиком значение должно быть известно до наступления новых событий, например, текущий статус пользователя.

```typescript
// начальное значение для всех новых подписчиков до получения других значений
const subject = new BehaviorSubject<number>(0); // начальное значение 0
```
<br/>

## <a name="replay_behavior"></a>Чем ReplaySubject отличается от BehaviorSubject?

Оба они относятся к т.н. "тёплым" наблюдаемым объектам (начинаются как "горячие", но новые подписчики могут получать последние или определённые начальные значения, даже если они подписались позже.)

ReplaySubje в отличие от BehaviorSubject:

- может хранить более одного значения, в зависимости от настроек
- поддерживает разграничение по времени: можно указать, как долго значения хранятся (в миллисекундах).

```typescript
const replaySubject = new ReplaySubject<number>(2); // храним два последних значения
replaySubject.next(1);
replaySubject.next(2);
replaySubject.next(3);

replaySubject.subscribe(value => console.log(`ReplaySubscriber: ${value}`));
// Выдаст 2, 3, потому что они были последними двумя значениями перед подпиской.
```

Пример использования ReplaySubject с временным окном:
```typescript
import { ReplaySubject } from 'rxjs';

// Создаем ReplaySubject, который хранит только последние значения за последние 500 миллисекунд.
const replaySubject = new ReplaySubject<number>(Infinity, 500);

replaySubject.next(1);
setTimeout(() => replaySubject.next(2), 100); // Через 100 мс добавляем 2
setTimeout(() => replaySubject.next(3), 200); // Через 200 мс добавляем 3
setTimeout(() => replaySubject.next(4), 700); // Через 700 мс добавляем 4

setTimeout(() => {
  // Подписываемся через 1000 мс после начала
  replaySubject.subscribe(value => console.log(`Subscriber: ${value}`));
  // На момент подписки, значения 1 и 2 устарели (пройдут более 500 мс с момента их эмиссии),
  // так что мы видим только 3 и 4 после подписки.
}, 1000);
```
<br/>

## <a name="concat"></a>Как реализовать несколько разных последовательных HTTP-запросов?

Можно воспользоваться оператором RxJS, таким как concatMap. Каждый последующий запрос ждёт завершения предыдущего перед своим началом.

```typescript
// Первый запрос для получения пользователя
  getUser(userId: string): Observable<User> {
    return this.httpClient.get<User>(`https://api.example.com/users/${userId}`);
  }

  // Второй запрос для получения профиля пользователя
  getUserProfile(userId: string): Observable<Profile> {
    return this.httpClient.get<Profile>(`https://api.example.com/users/${userId}/profile`);
  }

  // Метод для выполнения последовательных запросов
  getUserAndProfile(userId: string): Observable<Profile> {
    return this.getUser(userId)
     .pipe(concatMap(user => this.getUserProfile(user.id)) // Используем id пользователя для следующего запроса
    );
  }
```
<br/>

## <a name="usecase"></a>Как реализовать следующий сценарий?

1) сделать http-запрос
2) в случае ошибки повторить запрос три раза с интервалом в 5 секунд
3) закэшировать результат на 10 минут

```typescript
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Observable, of, timer } from 'rxjs';
import { catchError, delay, retryWhen, shareReplay, switchMap, take } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class DataService {

  // Параметры кэширования
  private cacheInterval = 10 * 60 * 1000; // 10 минут в миллисекундах
  private cachedData$: Observable<any>;

  constructor(private http: HttpClient) { }

  getData(): Observable<any> {
    if (!this.cachedData$) {
      this.cachedData$ = this.http.get('https://api.example.com/data').pipe(
        retryWhen(errors => 
          errors.pipe(
            delay(5000), // Задержка в 5 секунд
            take(3) // Повторить 3 раза
          )
        ),
        catchError(error => {
          // Обработка ошибки, если после 3 повторов она не исчезла
          console.error('Ошибка запроса:', error);
          return of(null); // Возвращаем null или пустое значение
        }),
        shareReplay(1) // Кэшируем только один последний эмит в течение заданного времени
      );

      // Сбрасываем кэш через 10 минут
      timer(this.cacheInterval).subscribe(() => this.cachedData$ = null);
    }

    return this.cachedData$;
  }
}
```
<br/>