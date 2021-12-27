 [Learning Links](https://www.tektutorialshub.com/angular/valuechanges-in-angular-forms/)
 
 ValueChanges of FormControl
---------------------------------------
    
```Javascript
 onNgInit(){
  this.formGroup.get('balance').valueChanges.subscribe(x=>{
   this.customerBalance=x;
})
}

---------------------
 
this.reactiveForm.get("firstname").valueChanges.subscribe(selectedValue => {
  console.log('firstname value changed')
  console.log(selectedValue)                              //latest value of firstname
  console.log(this.reactiveForm.get("firstname").value)   //latest value of firstname
});
---------------------------------------
2
3
4
5
6
7
8
 
this.reactiveForm.get("firstname").valueChanges.subscribe(selectedValue => {
  console.log('firstname value changed')
  console.log(selectedValue)
  console.log(this.reactiveForm.get("firstname").value)
  console.log(this.reactiveForm.value)   //still shows the old first name
})
 
 

```
