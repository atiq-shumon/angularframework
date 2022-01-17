  #### onKeyUP event handling
  ```html
  <mat-form-field class="example-full-width">
      <mat-label>Adjusted Amount</mat-label>
      <input matInput (keyup)="onAdjustFieldkeyup($event)" placeholder="Adjusted Amount" value="" formControlName="adjustedamount" autocomplete="off">
    </mat-form-field>
    -----------------------------------------------
onAdjustFieldkeyup(event:any){
  console.log(this.formGroup.get('adjustedamount').value);
  console.log(this.customerBalance)
}
```    
