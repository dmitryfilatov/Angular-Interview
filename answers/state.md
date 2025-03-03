## <a name="cache"></a>Как кэшировать данные в Angular?

Способы кэширования данных в Angular:

- Сохранять данные в localStorage/sessionStorage
- Сохранять данные в переменной в сервисе
- Симулировать состояние с помощью BehaviorSubject и получать из него последнее значение
- Использовать кэширование в помощью RxJs
- Использовать библиотеку NgRx
- Использовать библиотеку NGXS

<br/>

## <a name="ngrx"></a>Что такое NgRx?

NgRx — это библиотека для Angular, предназначенная для управления состоянием приложения с использованием принципов и паттернов, вдохновленных Redux.

Базовые концепции:

- Store (Хранилище): централизованный объект состояния вашего приложения, представляющий единый источник истины.
- Actions (Действия): намерения изменения состояния (тип действия)
- Reducers (Редьюсеры): функции, описывающие, как состояние изменяется в ответ на действия. 
- Selectors (Селекторы): функции, помогающие извлечь куски состояния из хранилища.
- Effects (Эффекты): управляют побочными эффектами, вызванными действиями, выполняя асинхронные операции, и порождают новые действия.

Пример использования NgRx:

```typescript
// Action
export const increment = createAction('[Counter] Increment');

// Reducer
export const counterReducer = createReducer(
  initialState,
  on(increment, state => ({ count: state.count + 1 }))
);

// Selector
export const selectCount = createSelector(
  (state: AppState) => state.counter,
  (counter) => counter.count
);

// Effect
@Injectable()
export class CounterEffects {
  increment$ = createEffect(() => this.actions$.pipe(
    ofType(increment),
    // Вставить побочный эффект, если необходим
  ));

  constructor(private actions$: Actions) {}
}
 ```

<br/>

## <a name="ngxs"></a>Что такое NGXS?

MGXS - это библиотека для управления состоянием в Angular-приложениях, с более простым и интуитивно понятным API по сравнению с NgRx.

Базовые концепции NGXS:

- State (состояние): основная структура данных, хранящаяся централизованно. Каждое состояние определяется классом, который декорирован с помощью декоратора @State(). Внутри состояния можно определять свойства, описывающие данные, и методы-акции для их изменения.

- Actions (действия): намерения изменения состояния. Действия в NGXS представляются как простые классы, с читаемыми именами и опциональными полезными данными.

- Selectors (селекторы): способы извлечения и композиции данных из состояния. Селекторы позволяют создавать производные данные, не изменяя само состояние.

- Dispatch и Subscribe: Ngxs позволяет отправлять (dispatch) действия и подписываться (subscribe) на состояние для реагирования на изменения или извлечения данных.

Пример использования NGXS:

Определение состояния и действия:

```typescript
import { State, Action, StateContext, Selector } from '@ngxs/store';

// Определяем действие
export class AddItem {
  static readonly type = '[Shopping] Add Item';
  constructor(public payload: string) {}
}

// Определяем состояние
@State<string[]>({
  name: 'items',
  defaults: []
})
export class ItemsState {
  
  // Селектор для доступа к состоянию
  @Selector()
  static getItems(state: string[]) {
    return state;
  }

  // Обработка действия
  @Action(AddItem)
  add(ctx: StateContext<string[]>, action: AddItem) {
    const state = ctx.getState();
    ctx.setState([...state, action.payload]);
  }
}
 ```

Использование в компоненте:

```typescript

import { Component } from '@angular/core';
import { Store } from '@ngxs/store';
import { AddItem } from './items.state';

@Component({
  selector: 'app-item-manager',
  template: `
    <button (click)="addItem('New Item')">Add Item</button>
  `
})
export class ItemManagerComponent {
  constructor(private store: Store) {}

  addItem(item: string) {
    this.store.dispatch(new AddItem(item));
  }
}
 ```

<br/>