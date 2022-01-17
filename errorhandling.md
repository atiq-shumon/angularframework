[important links]

[Validator learning](https://blog.angular-university.io/angular-custom-validators/) || [Form Value Changes and Validators](https://github.com/atiq-shumon/angularframework/blob/master/formvaluechanges.md)


[Validation]

##### Adding Dynamic Validation to form control

```
ngOnInit(): void {
    this.formGroup.addControl('comments',new FormControl(''));
   // this.formGroup.controls[controlname]
   this.formGroup.get(this.controlname).valueChanges
  .subscribe(value => {
     if(value==='-1') {
      //console.log(value);
      this.formGroup.get('comments').setValidators([Validators.required]);
      this.formGroup.controls["comments"].updateValueAndValidity();
    } else {
      this.formGroup.get('comments').clearValidators();
      this.formGroup.controls["comments"].updateValueAndValidity();
    }
  });
}
```

Custom Validation Complete example
---------------------------------------------

HTML & CSS
```
.example-full-width{
  padding:.3rem .3rem 0 .3rem;
}

-----------------------
<div *ngIf="currentPaymentMode==='C'" style="background-color: #dfdf67;border-radius: 10px;margin-top:.6rem;padding:.5rem;" [formGroup]="formGroup">
    <mat-form-field class="example-full-width">
      <mat-label>Tentative Payment date * :</mat-label>
      <input matInput    formControlName="creditpaymentdate"  [matDatepicker]="spicker" >
       <mat-datepicker-toggle matSuffix [for]="spicker"></mat-datepicker-toggle>
      <mat-datepicker disabled="false" #spicker  ></mat-datepicker>
     
      <!-- <div  *ngIf="formGroup?.creditpaymentdate?.errors?.required">
        Your password must have lower case, upper case and numeric characters.
    </div>  -->
    </mat-form-field>
    <div  style="color:red;margin-top:-10px;" *ngIf="formGroup.controls['creditpaymentdate'].touched && formGroup.controls['creditpaymentdate']?.errors?.required">
        Date is required
   </div>
  </div>

  <div *ngIf="currentPaymentMode==='A'" style="width:100%; background-color: #70c08b;border-radius: 10px;margin-top:.6rem;padding:.5rem;display: flex;" [formGroup]="formGroup">
    <div>
    <mat-form-field class="example-full-width">
      <mat-label >Adjusted Amount *</mat-label>
      <input atiqs-number-only matInput (keyup)="onAdjustFieldkeyup($event)" placeholder="Adjusted Amount" value="" formControlName="adjustedamount" autocomplete="off">
          
    </mat-form-field>
    <div  style="color:red;margin-top:-10px;" *ngIf="formGroup.controls['adjustedamount'].touched && formGroup.controls['adjustedamount']?.errors?.required">
      Adjusted Amount Required
   </div>
   <div  style="color:red;margin-top:-10px;" *ngIf="isExceeding">
    Adjusted amount should not exceed Balance amount
 </div>
  </div>
    &nbsp;&nbsp;&nbsp; 
    <div style="padding:1rem;" class="example-full-width">
      <mat-label style="font-weight: bold;padding:1rem;">Balance Amount : {{customerBalance}}</mat-label>
     
    </div>
    
  </div>
```
#### Adding dynamic validation on radio button value change
```
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
#### onKeyup Custom validation 
```
onAdjustFieldkeyup(event:any){
 // console.log(this.formGroup)
  var textval=parseFloat(this.formGroup.get('adjustedamount').value.replace(/,/g, ''));
  var customerbal=Number(typeof this.customerBalance!=='undefined' && this.customerBalance.toString().indexOf(',')>-1?this.customerBalance.replace(/,/g, ''):this.customerBalance);
  //if()
   // console.log(Number(this.customerBalance.replace(/,/g, '')))
    if(Number(textval)>customerbal){
       this.isExceeding=true;
       this.formGroup.get('adjustedamount').setErrors({'exceed':'Adjustement exceeding balance is not allowed'}); 
    }
    else{
      this.isExceeding=false;
      setTimeout(() => {
        if (this.formGroup.get('adjustedamount').hasError('exceed')) {
          delete this.formGroup.get('adjustedamount').errors['exceed'];
          this.formGroup.get('adjustedamount').updateValueAndValidity();
        }
      }, 100);
     
     // this.formGroup.get('adjustedamount').setErrors({'exceed':null})
     
    }
}
```
