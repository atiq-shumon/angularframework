
```Javascript

export class BulkSalesModeFieldComponent implements OnDestroy,AfterViewInit,AfterViewChecked{

 paymentmodefromgroup:FormGroup;
 
 constructor(){
    this.paymentmodefromgroup=new FormGroup({});
 
 }
  ngOnInit(): void {
  this.paymentmodefromgroup.addControl("paymenttypes",new FormControl('',[Validators.required]));
    //  this.paramFormConfig[prop].value ||new Date()
    this.paymentmodefromgroup.addControl("date",new FormControl(new Date(),Validators.required));
    this.paymentmodefromgroup.addControl("reffNumber",new FormControl('',[Validators.required,Validators.minLength(2)]));
    this.paymentmodefromgroup.addControl("bank",new FormControl('',[Validators.required]));
    this.paymentmodefromgroup.addControl("branch",new FormControl(''));
    this.paymentmodefromgroup.addControl("bankaccount",new FormControl('',[Validators.required]));
    this.paymentmodefromgroup.addControl("amount",new FormControl({value: '', disabled: false},[Validators.required]));
 
  }
}
```
