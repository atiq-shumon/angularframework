[Important Links]

[Form Value Change Handling](https://github.com/atiq-shumon/angularframework/blob/master/formvaluechanges.md) || [Adding grid to data to main form group](#Adding-grid-to-data-to-main-form-group)


[Page Contents] || 

[Getting Key Value of Dropdown list](#Getting-Key-value-of-Dropdownlist) || [***** Adding sub Form Data to Grid](#adding-sub-form-data-to-grid) || [********Adding Footer To grid](#adding-footer-to-grid)

```Javascript

export class BulkSalesModeFieldComponent implements OnDestroy,AfterViewInit,AfterViewChecked{

 paymentmodeformgroup:FormGroup;
 
 constructor(){
    this.paymentmodefromgroup=new FormGroup({});
 
 }
  ngOnInit(): void {
  
  ----------------adding to main form group
  
  if(!this.formGroup.get('salesmode')){
      this.formGroup.addControl("salesmode",new FormControl());
      this.formGroup.addControl("creditpaymentdate",new FormControl(''))
      this.formGroup.addControl("adjustedamount",new FormControl(''))
    }
  
  ------------------------
  
  this.paymentmodefromgroup.addControl("paymenttypes",new FormControl('',[Validators.required]));
    //  this.paramFormConfig[prop].value ||new Date()
    this.paymentmodefromgroup.addControl("date",new FormControl(new Date(),Validators.required));
    this.paymentmodefromgroup.addControl("reffNumber",new FormControl('',[Validators.required,Validators.minLength(2)]));
    this.paymentmodefromgroup.addControl("bank",new FormControl('',[Validators.required]));
    this.paymentmodefromgroup.addControl("branch",new FormControl(''));
    this.paymentmodefromgroup.addControl("bankaccount",new FormControl('',[Validators.required]));
    this.paymentmodefromgroup.addControl("amount",new FormControl({value: '', disabled: false},[Validators.required]));
 
  }
reloadaddpaymentform(){
     this.paymentmodefromgroup.get('reffNumber').setValue('');
     this.paymentmodefromgroup.get('bank').setValue('');
     this.paymentmodefromgroup.get('date').setValue(new Date());
     this.paymentmodefromgroup.get("branch").setValue('');
     this.paymentmodefromgroup.get("amount").setValue('');
     this.paymentmodefromgroup.get("bankaccount").setValue('');
   }  
}
```

## Getting Key value of Dropdownlist
-----------------------------------------
```Javascript
let types=this.paymenttypes.find(c => c.value === paymenttypeid);
      //console.log(this.bankmasterdata);
      let banks=(typeof v.bank!=='undefined')?this.bankmasterdata.find(c => c.value === v.bank):{display:'',value:''};
  
  let data={paymenttype: types.display,paymenttypeoid:types.value, amount: amount, reffnumber: reffnumber, date: date, bankname: banks.display,bankoid:banks.value
        , branchname: branch};

```
# Adding grid to data to main form group
--------------------------------------------------
```Javascript
   onpaymentformgroupaddbuttonclick(v:any){

      let paymenttypeid=v.paymenttypes;
     // const toSelect = this.crieteria.find(c => c.value === 'getcustomer');
      let types=this.paymenttypes.find(c => c.value === paymenttypeid);
      //console.log(this.bankmasterdata);
      let banks=(typeof v.bank!=='undefined')?this.bankmasterdata.find(c => c.value === v.bank):{display:'',value:''};
    //  console.log(banks);
     // let paymenttypename=v.paymenttypes;
      let amount=v.amount;
      let reffnumber=v.reffNumber;
      let date=typeof v.date!=='undefined'? Utility.dateToYMD(v.date):'';
      let branch=v.branch;
      let data={paymenttype: types.display,paymenttypeoid:types.value, amount: amount, reffnumber: reffnumber, date: date, bankname: banks.display,bankoid:banks.value
        , branchname: branch};

       this.dataSource.data.push(data);
        this.dataSource.filter = "";
        this.formGroup.get("depositfieldId").setValue(this.dataSource.data);
    //  this.bulksalesmodeservice.addData(data);
      this.reloadaddpaymentform();
    //  console.log( this.bulksalesmodeservice.getValue);
    }
```
# adding sub form data to grid
----------------------------------------------
```Javascript
------------------------------------------
<button (click)=addToGrid(balancetransferformgroup.value);   [disabled]="!this.balancetransferformgroup.valid" mat-raised-button [ngClass] = "{'enabled-color': this.balancetransferformgroup.valid} " style="border-radius:1rem;cursor: pointer;" ><mat-icon>check box</mat-icon>&nbsp;Add</button>
------------------------------------------
addToGrid(v:any){
 // console.log(v);
  let companytitle=this.companies.find(c => c.value === v.companyid).display;
  let producttitle=this.companies.find(c => c.value === v.companyid).display;
  this.dataSource.data = [...this.dataSource.data, {"companyid":v.companyid,"company":companytitle,"productid":v.productid,"product":producttitle, "amount":v.transferamount}];
  this.balancetransferformgroup.reset();
  // console.log(this.dataSource.data)
}
```

# adding footer to grid
--------------------------------------------
```Html
  <!-- Position Column -->
  <ng-container matColumnDef="company">
    <th mat-header-cell *matHeaderCellDef> Company </th>
    <td mat-cell *matCellDef="let element"> {{element.company}} </td>
  </ng-container>
 <!-- Name Column -->
 <ng-container matColumnDef="product">
  <th mat-header-cell *matHeaderCellDef> Product </th>
  <td mat-cell *matCellDef="let element"> {{element.product}} </td>
  <td mat-footer-cell *matFooterCellDef>Total: </td>
</ng-container>

 <!-- Name Column -->
 <ng-container matColumnDef="amount">
  <th mat-header-cell *matHeaderCellDef> Amount </th>
  <td mat-cell *matCellDef="let element"> {{element.amount}} </td>
  <td mat-footer-cell *matFooterCellDef>  <b>{{getTotalAmount() }}</b> </td>
</ng-container>

--------------------------------


```
