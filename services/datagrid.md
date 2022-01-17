
Datagrid service
----------------------------------

```Javascript

import {Injectable} from '@angular/core';
import {BehaviorSubject,Observable} from 'rxjs';


@Injectable()
export class DepositService {
  //private readonly API_URL = 'https://api.github.com/repos/angular/angular/issues';
  private checkeddata;
  private subject: BehaviorSubject<any[]> = new BehaviorSubject<any[]>([]);

  //private selectClicked: BehaviorSubject<any[]> = new BehaviorSubject<any[]>([]);
  //private expandedContents: BehaviorSubject<any[]> = new BehaviorSubject<any[]>([]);

  constructor () {}
  public get getValue() {
    return this.subject.getValue();

  }
  getData(): Observable<any> {
    return this.subject.asObservable();
  }

  setData(value:any) {
    // set the latest value for _data BehaviorSubject
   // console.log(value);
    this.subject.next(value);
 }
 addData(data:any) {
  //console.log(addconfig);
 // console.log('config.data');
 // console.log(addconfig.data);
  const currentValue = this.subject.value;
//console.log(currentValue);
 // console.log(addconfig.index);
 // console.log(currentValue[addconfig.index]);
  const updatedValue = [...currentValue, data];
  //console.log(updatedValue);
  this.subject.next(updatedValue);
}
 remove_data(index:any){
  //console.log('index');
  if(this.subject.value.length>-1){
       this.subject.value.splice(index,1);
     }
   // console.log(this.subject.value);
   // this.subject.next(this.subject.value);
  }
}
```
