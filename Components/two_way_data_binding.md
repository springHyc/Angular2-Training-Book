#使用双向数据绑定
双向数据绑定结合的输入和输出结合到使用一个单一的符号ngModel指示。
```html
<input [(ngModel)]="name" >
```
这在幕后做的是什么等同于：
```html
<input [ngModel]="name" (ngModelChange)="name=$event">
```
要创建自己的组件，支持双向绑定，你必须定义一个@Output属性匹配@Input，但与它后缀Change，例如：
```ts
import {Component, Input, Output, EventEmitter} from '@angular/core';

@Component({
  selector: 'counter',
  template: `
    <div>
      <p>
        <ng-content></ng-content>
        Count: {{ count }} -
        <button (click)="increment()">Increment</button>
      </p>
    </div>
  `
})
export class Counter {
  @Input() count: number = 0;
  @Output() countChange: EventEmitter<number> = new EventEmitter<number>();

  increment() {
    this.count++;
    this.countChange.emit(this.count);
  }
}
```
[查看示例](http://plnkr.co/edit/nwRNxpoTuk4M60Y5Khq8?p=preview)