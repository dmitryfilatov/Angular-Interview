## <a name="what-is"></a>Что такое компонент?

Компонент — это основной строительный блок UI. Он контролирует часть UI с помощью своего шаблона и логики. Создать его можно с помощью CLI:

```bash
ng generate component <name>
```
для использования надо добавить его селектор в HTML:

```html
<app-name></app-name>
```
<br/>

## <a name="input_output"></a>Для чего используются декораторы @Input()и @Output()?

- @Input(): Передача данных от родительского компонента к дочернему.
- @Output(): Передача событий от дочернего элемента к родительскому с помощью EventEmitter.
<br/>

## <a name="idestroy"></a>Когда уничтожается компонент?

- навигация
- изменение *ngIf в родительском
- динамически
- удаление родительского
<br/>

## <a name="idestroy_what"></a>Что происходит при удалении компонента?

- в компоненте вызывается хук ngOnDestroy().
- удаляются все DOM-элементы, связанные с компонентом.
- удаляются все шаблонные подписки и слушатели событий, связанных с компонентом.
- удаляются все внутренние структуры данных и состояния
- рекурсивно удаляются все дочерние компоненты с теми же этапами удаления
<br/>

## <a name="emit"></a>Какие компоненты будут оповещены о том, что был emit события?

Только родительский, если он явно подписан на это событие в своём шаблоне.

Пример дочернего:

```typescript
import { Component, EventEmitter, Output } from '@angular/core';

@Component({
  selector: 'child-component',
  template: `<button (click)="emitEvent()">Emit Event</button>`
})
export class ChildComponent {
  @Output() customEvent = new EventEmitter<string>();

  emitEvent() {
    this.customEvent.emit('Hello from Child!');
  }
}
```
Подписка на событие в шаблоне родительского:

```html
   <child-component (customEvent)="handleCustomEvent($event)"></child-component>
```
<br/>
