[Important Links]

[Form Value Change Handling](https://github.com/atiq-shumon/angularframework/blob/master/formvaluechanges.md) || 

[Adding grid to data to main form group](#Adding-grid-to-data-to -main-form-group)


[Page Contents] || [Getting Key Value of Dropdown list](#Getting-Key-value-of-Dropdownlist)

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
