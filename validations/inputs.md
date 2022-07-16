Converting Enter press into tab press
----------------------------------------------
```html
document.addEventListener('keydown', function (event) {
  if (event.keyCode === 13 && event.target.nodeName === 'INPUT') {
    var form = event.target.form;
    var index = Array.prototype.indexOf.call(form, event.target);
    form.elements[index + 1].focus();
    event.preventDefault();
  }
});
```

Integer Only Inputs
----------------------------------------
```HTML
<input type="text" (keypress)="keyPressNumbers($event)" />
 ------------------------------------------
 keyPressNumbers(event) {
    var charCode = (event.which) ? event.which : event.keyCode;
    // Only Numbers 0-9
    if ((charCode < 48 || charCode > 57)) {
      event.preventDefault();
      return false;
    } else {
      return true;
    }
  }
```

Number with decimal inputs
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
Alpha Numeric
-----------------------------------
```HTML
<input type="text" (keypress)="keyPressAlphanumeric($event)" />
-----------------------------------------
keyPressAlphanumeric(event) {

    var inp = String.fromCharCode(event.keyCode);

    if (/[a-zA-Z0-9]/.test(inp)) {
      return true;
    } else {
      event.preventDefault();
      return false;
    }
  }
```
