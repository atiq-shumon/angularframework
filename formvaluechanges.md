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
 
this.reactiveForm.get("firstname").valueChanges.subscribe(selectedValue => {
  console.log('firstname value changed')
  console.log(selectedValue)
  console.log(this.reactiveForm.get("firstname").value)
  console.log(this.reactiveForm.value)   //still shows the old first name
})
 
 

```

Value Changes and Validators
-----------------------------------
```Javascript

  this.formGroup.get('salesmode').valueChanges
       .subscribe(value => {
          if(value==='C') {
            //console.log(value);
            this.formGroup.get('adjustedamount').clearValidators();
            this.formGroup.controls["adjustedamount"].updateValueAndValidity();
            this.formGroup.get('creditpaymentdate').setValidators([Validators.required]);
        } 
          if(value==='A') {
            //console.log(value);
            this.formGroup.get('creditpaymentdate').clearValidators();
            this.formGroup.controls["creditpaymentdate"].updateValueAndValidity();
            this.formGroup.get('adjustedamount').setValidators([Validators.required]);
        
          }
  });
   
```
