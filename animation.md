
Rich link
---------------------
[animation in depth](https://indepth.dev/in-depth-guide-into-animations-in-angular)

[another example](https://fireship.io/lessons/angular-router-animations/)

Enter And Exit Animations
-----------------------------
Angular also provides some useful aliases such as :enter and :leave to animate elements entering and leaving the DOM. 
These aliases are essentially transitions to and from the void state, i.e. void => * and * => void respectively. 
This is particularly useful for adding some animation to elements which are shown conditionally using *ngIf or *ngFor.
The code below shows how you can create a fade in and fade out animation.

```Javascript
trigger('fadeSlideInOut', [
	transition(':enter', [
		style({ opacity: 0, transform: 'translateY(10px)' }),
		animate('500ms', style({ opacity: 1, transform: 'translateY(0)' })),
	]),
	transition(':leave', [
		animate('500ms', style({ opacity: 0, transform: 'translateY(10px)' })),
	]),
]),

```

uses:
-------------
```
<div *ngIf="show" @fadeSlideInOut>...</div>

```
Reusing animations
------------------------------
```Javascript
// fade.animation.ts
export const Fade = trigger('fade', [
    transition(':enter', [
        style({ opacity: 0 }),
        animate('500ms', style({ opacity: 1 })),
    ]),
    transition(':leave', [animate('500ms', style({ opacity: 0 }))]),
]);
```
uses:
```Javascript
import { Fade } from './fade.animation';

@Component({
	animations: [Fade],
})
```
Fade animations
----------------------
```Javascript
import {
  trigger,
  animate,
  transition,
  style,
  query
} from '@angular/animations';

export const fadeAnimation = trigger('fadeAnimation', [
  transition('* => *', [
    query(
      ':enter',
      [style({ opacity: 0 })],
      { optional: true }
    ),
    query(
      ':leave',
      [style({ opacity: 1 }), animate('0.3s', style({ opacity: 0 }))],
      { optional: true }
    ),
    query(
      ':enter',
      [style({ opacity: 0 }), animate('0.3s', style({ opacity: 1 }))],
      { optional: true }
    )
  ])
]);

```
