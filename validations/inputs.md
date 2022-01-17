Number Only inputs
--------------------------
```html
  <mat-form-field [formGroup]="balancetransferformgroup"  style="width:50%;">
                  <mat-label>Amount *</mat-label>
                   <input matInput   (keypress)="keyPressNumbersWithDecimal($event)"
                      formControlName="transferamount" autocomplete="off"
                      id="amount" type="text">
                </mat-form-field>  
----------------------------------------------
keyPressNumbersWithDecimal(event) {
  var charCode = (event.which) ? event.which : event.keyCode;
  if (charCode != 46 && charCode > 31
    && (charCode < 48 || charCode > 57)) {
    event.preventDefault();
    return false;
  }
  return true;
}
      
```
