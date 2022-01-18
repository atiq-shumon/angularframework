


Data Grid Sub Form Complete Example || [Data Grid Sub Form HTML part](#Data-Grid-Sub-Form-HTML-part) || [Data Grid Sub Form CSS part](#Data-Grid-Sub-Form-CSS-part)
-----------------------------------------------

### DataGrid SubForm JS part
```Javascript
import {Component,  Input, OnDestroy, AfterViewInit,ViewChild, ChangeDetectorRef, Directive} from '@angular/core';
import {Subscription } from 'rxjs';
import { FormGroup, FormControl, Validators } from '@angular/forms';
import { HttpService } from '../../../services/http/http.service';
import { ProgressBarService } from '../../../services/loader/progressbar.services';
import { ToasterService } from '../../../services/toaster/toaster.services';
import { Router } from '@angular/router';
import { UserService } from '../../../services/user/user.service';
import { CONFIGURATION } from '../../../models/constants/app.constants';
import { rowsAnimation } from '../../../animations/angularanimations';
import { Utility } from '../../../services/utility';
import { MatTableDataSource } from '@angular/material/table';
import {NumberOnlyDirective} from '../../../directives/number-only.directive';
export interface Companies {
  value: string;
  display: string;
}

@Component({
  selector: 'balancetransfer',
  styleUrls: ['balancetransfer.component.css'],
  templateUrl: 'balancetransfer.component.html'
  //,
 //animations:[rowsAnimation]
})
export class BalanceTransferFieldComponent implements OnDestroy, AfterViewInit{
  serverPath:any;mrrinfo:any; oid:any;
  @Input() inputparams:any;
  @Input() controlname:any;
  @Input() formGroup:any;
   subscription:Subscription; ;
  company:string;
  supplierid:string; balance:any;
  suppliername:string; transactionperiod:string;
  json:any;baltext:any;isshowbalance:boolean;
  includeblnstransfer:any=false;
  path:any;
 companies: Companies[] = []; products: any[] = [];

 displayedColumns: string[] = ['company','product', 'amount','actions'];
 dataSource=new MatTableDataSource<any>();
 balancetransferformgroup:FormGroup;
  constructor(private cdr: ChangeDetectorRef, public progressbar:ProgressBarService,public toasterService:ToasterService,private httpServices:HttpService) {
    this.serverPath=CONFIGURATION.baseUrls.servericms;
    this.path=this.serverPath;
    this.json=this.inputparams;
    this.balancetransferformgroup=new FormGroup({});

}


changeValue(e){
  // console.log(e.target.value);
  // this.formGroup.get(this.controlname).setValue(e.target.value, {
  //   onlySelf: true
  // })
}
onSelectClicked(val:any){

}
ngAfterViewChecked(){
  //your code to update the model
  this.cdr.detectChanges();
}
ngAfterViewInit(){
  let company= JSON.parse(this.inputparams);
  if(Object.keys(company).length>0){
    this.companies.push({value: company.CompanyId,display: company.CompanyName});
    //this.customersbkp=this.companies;
    // const toSelect = this.customers.find(c => c.value === this.custs[0]);
//console.log( this.customers);
 this.formGroup.get(this.controlname).setValue(this.companies[0].value);
  }
}
serachInSmartCombo(data:string){

  // if(data.length>0) {
  //   this.companies=this.companiesbkp;
  //   let filtered=this.companies.filter(vl=>vl.display.toUpperCase().indexOf(data.toUpperCase())!==-1);
  //   this.companies=filtered;
  // }
  // else{
  //   this.companies=this.companiesbkp;
  // }

}
close(){
 // this.shouldshow=false;
}

handleSearch(v:any){

}
onCheckBoxChange(v:any){
   if(v===false){
    this.formGroup.get("balancetransferfield").setValue({});
   }
   else{
    this.formGroup.get("balancetransferfield").setValue(this.dataSource.data);
   }
}

onSelectClickedCriteria(v:any){
 // console.log(value);
 // console.log(value);
// this.curviewValue="Search " +this.crieteria.find(c=> c.value === v.value).viewValue+" ...";
}
  ngOnInit(): void {
      
    this.getcompanies();

    this.balancetransferformgroup.addControl("companyid",new FormControl('',[Validators.required]));
    this.balancetransferformgroup.addControl("productid",new FormControl('',[Validators.required]));
    this.balancetransferformgroup.addControl("transferamount",new FormControl('',[Validators.required]));

}
addToGrid(v:any){
 // console.log(v);
  let companytitle=this.companies.find(c => c.value === v.companyid).display;
  let producttitle=this.products.find(c => c.value === v.productid).display;
  this.dataSource.data = [...this.dataSource.data, {"companyid":v.companyid,"company":companytitle,"productid":v.productid,"product":producttitle, "amount":v.transferamount}];
  this.formGroup.get("balancetransferfield").setValue(this.dataSource.data);
  this.balancetransferformgroup.reset();
  // console.log(this.dataSource.data)
}
addinputform(){

}
deletetableItem(row:any,index:any){
    this.dataSource.data.splice(index, 1);
    this.formGroup.get("balancetransferfield").setValue(this.dataSource.data);
    this.dataSource._updateChangeSubscription();
}

getcompanies(){
  this.companies=[];
  let path=this.path+"/"+"sharedpage"+"/getcompany";
  let json={ActionControlMode:'all_sales_companies','Param1':'x'};
  //console.log(json);
  //console.log(path);
  this.progressbar.start();
  this.subscription=this.httpServices.postData(json,path).subscribe(data=>{
  this.companies=data;
  },(error:any)=>{this.toasterService.showToaster(error.toString(),'red-snackbar')},
  ()=>{this.progressbar.stop();}

  )

}
populateproducts(val:any){
  let companyId=val;
  this.products=[];
  this.balancetransferformgroup.get("productid").setValue('');
  let path=this.path+"/"+"sharedpage"+"/getproduct";
  let json={ActionControlMode:'company_wise','Param1':companyId};
  //console.log(json);
 // console.log(path);
  this.progressbar.start();
  this.subscription=this.httpServices.postData(json,path).subscribe(data=>{
   //console.log(data);
    let ddldata=data.map(x=>({'value': x.productID,'display':x.productName}));
    this.products=ddldata;
  },(error:any)=>{this.toasterService.showToaster(error.toString(),'red-snackbar')},
  ()=>{this.progressbar.stop();}

    )
  }

ngOnDestroy() {
  // unsubscribe to ensure no memory leaks
  this.subscription.unsubscribe();
}

getTotalAmount(){
  return Utility.tobdt(this.dataSource.data.map(t => t.amount).reduce((acc, value) => acc +  +value, 0));
}
addcomma(val:any){
  if(typeof val!=='undefined'){
    return Utility.tobdt(val);
  }
  else{
    return 'x';
  }

}
keyPressNumbersWithDecimal(event) {
  var charCode = (event.which) ? event.which : event.keyCode;
  if (charCode != 46 && charCode > 31
    && (charCode < 48 || charCode > 57)) {
    event.preventDefault();
    return false;
  }
  return true;
}
}
```

## Data Grid Sub Form HTML part
-------------------------------------------
```HTML
<div class="example-container">
  <mat-checkbox class="example-margin" (change)="onCheckBoxChange($event.checked)" [(ngModel)]="includeblnstransfer"><b>Include Balance Transfer?</b></mat-checkbox>
   <div style="background-color: #DFDFDE;border-radius: 10px;margin-top:.6rem;padding:.5rem;margin-bottom:.5rem;" *ngIf="includeblnstransfer">
    
    <div [formGroup]="balancetransferformgroup" style="display: flex;justify-content: space-between;border-radius: 10px; padding:.5rem;">
       <div   style="width:48%;">
        
          <mat-form-field style="width:100%;">
              <mat-select  (selectionChange)="populateproducts($event.value)" id="companyctl" placeholder="Company *"  formControlName="companyid" >
                <mat-select-search #companyFilterCtrl></mat-select-search>
                 <mat-option *ngFor="let company of companies|filter:companyFilterCtrl.value" [value]="company.value">
                {{company.display}}
               </mat-option>
               </mat-select>
              </mat-form-field>
              <div  style="color:red;margin-top:-10px;" *ngIf="balancetransferformgroup.controls['companyid'].touched && balancetransferformgroup.controls['companyid']?.errors?.required">
                 Company is required
             </div>
            </div>
            <div  style="width:48%;">
              <mat-form-field style="width:100%;">
                  <mat-select   id="productctl" placeholder="Product *"  formControlName="productid" >
                    <mat-select-search #productFilterCtrl></mat-select-search>
                     <mat-option *ngFor="let prod of products|filter:productFilterCtrl.value" [value]="prod.value">
                    {{prod.display}}
                   </mat-option>
                   </mat-select>
                  </mat-form-field>
                  <div  style="color:red;margin-top:-10px;" *ngIf="balancetransferformgroup.controls['productid'].touched && balancetransferformgroup.controls['productid']?.errors?.required">
                    Product is required
                </div>
                  </div>
               </div>
              
             <div style="width:48%; display: flex;">
              <div style="width:50%;">
              <mat-form-field [formGroup]="balancetransferformgroup"  style="width:100%;">
                  <mat-label>Amount *</mat-label>
                   <input matInput   (keypress)="keyPressNumbersWithDecimal($event)"
                      formControlName="transferamount" autocomplete="off"
                      id="amount" type="text">
                      
                </mat-form-field>  
                <div  style="color:red;margin-top:-10px;" *ngIf="balancetransferformgroup.controls['transferamount'].touched && balancetransferformgroup.controls['transferamount']?.errors?.required">
                  Amount is required
              </div>
            </div> 

               &nbsp;&nbsp; 
              

               <div style="width:50%;">
               <button (click)=addToGrid(balancetransferformgroup.value);   [disabled]="!this.balancetransferformgroup.valid" mat-raised-button [ngClass] = "{'enabled-color': this.balancetransferformgroup.valid} " style="border-radius:1rem;cursor: pointer;" ><mat-icon>check box</mat-icon>&nbsp;Add</button>
                
             </div>
             
                 <!-- table here  -->
                </div>

<div style="width: 100%;">
 <table #table mat-table [dataSource]="dataSource" class="mat-elevation-z8">

  <!--- Note that these columns can be defined in any order.
        The actual rendered columns are set as a property on the row definition" -->

  <!-- Position Column -->
  <ng-container matColumnDef="company">
    <th mat-header-cell *matHeaderCellDef> Company </th>
    <td mat-cell *matCellDef="let element"> {{element.company}} </td>
    <td mat-footer-cell *matFooterCellDef> </td>
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
  <td mat-cell *matCellDef="let element"> {{addcomma(element.amount)}} </td>
  <td mat-footer-cell *matFooterCellDef>  <b>{{getTotalAmount() }}</b> </td>
</ng-container>
  
     <!-- Action Column -->
    <ng-container  matColumnDef="actions">
      <th   mat-header-cell *matHeaderCellDef>
            <div  (click)="addinputform()" style="background-color:#ed1c24;color:white;cursor:pointer;padding:0 .5rem 0 .5rem;display: inline-flex;justify-content: center;align-items: center;margin:.5rem;"  >
             <mat-icon>add</mat-icon>
             </div>
          </th>

         <td  mat-cell *matCellDef="let row; let i=index;">
           <!-- *ngIf="Delete Allow" -->
           <button mat-icon-button  class="small" color="accent" (click)="deletetableItem(row,i)">
               <mat-icon  class="small" aria-label="Delete">delete</mat-icon>
             </button>
         </td>
         <td mat-footer-cell *matFooterCellDef></td>  

       </ng-container>

  <tr mat-header-row *matHeaderRowDef="displayedColumns"></tr>
  <tr mat-row *matRowDef="let row; columns: displayedColumns;"></tr>
  <tr  mat-footer-row *matFooterRowDef="displayedColumns"></tr>
</table>
</div> 
 </div>
```
Data Grid Sub Form CSS part
----------------------------------
```CSS

.example-container {
  display: flex;
  flex-direction: column;
  width: 99.95%;
  margin:0 auto;
  background-color: rgb(255, 255, 255,.7);
  /* min-width: 300px; */

}

.example-header {
  /* min-height: 64px; */
  /* padding: 8px 24px 0; */
  font-weight: bold;
}

.example-margin{
   padding:.1rem;
}

.mat-raised-button {
  padding: 0 .5rem 0 .5rem;
  margin: 6px 8px 6px 8px;
  min-width: 100px;
  border-radius: 0px;
  /* font-size: 14px; */
  text-align: center;
  /* text-transform: uppercase; */
  text-decoration:none;
  border: none;
  outline: none;
}

table {
  width: 100%;
  overflow: auto;
  border-collapse: collapse;
  margin:0 auto;
  }

  table td, table th {
    /* border: 1px solid #ddd; */
    /* border:1px solid #e0e0e0; */
    border: 1px solid rgba(1,1,1,.1);
    padding:.2rem;
    /* padding: 8px; */
    min-height: 1rem;
  }

/* .mat-table {

  max-height: 650px;
  width:100%;
    /* max-height: 80vh;
} */
/* .mat-table {
  display: block;
  width: 100%;

} */

.mat-form-field {
  font-size: .8rem;
  width: 100%;
  /* background:whitesmoke; */

}


/* .mat-table th,.mat-table tr,.mat-table td{
  border: 1px solid rgba(0,0,0,0.2);
} */

.mat-header-row {
  position: sticky;
  /* width:100%; */
  top: 0;
   /* color:white; */
  /* background:black; */
   background: #A9A9A9;

  z-index: 9999;
  height: 1.5rem;
  /* font-size: 14px; */

   /* font-size: 14px; */
   /* border: 1px solid rgba(0,0,0,0.2); */
}

.mat-cell {
    font-size: .70rem;

}

.hidden-row {
  display: none;
}

/* .mat-table th,.mat-table tr{
  border: 1px solid rgba(0,0,0,0.1);
} */

 .mat-row, .mat-footer-row,
.mat-header-row {
  /* display: flex; */
  /* border-bottom-width: 1px; */
  /* border-bottom-style: solid; */
  align-items: center;
   /* min-height: 25px; */
  /* padding: 0 5px; */
  cursor:pointer;
  /* min-height: 1.2rem; */
  height: 1.2rem;
 }
  .mat-header-row{
     font-weight: bold;
      /* min-height: 35px; */

   }
  .mat-header-cell {
     /* min-height: 30px; */
     /* padding:5px; */
     font-weight:bold;
     color:black;
  }
  .mat-row:hover{
     background-color:#f0f0f0;
     color:black;
     /* font-weight: bold; */

  }
  td.mat-cell, td.mat-footer-cell,th.mat-footer-cell, th.mat-header-cell {
    padding: 0;
    border:none;
    height:auto;
}
.mat-cell,.mat-footer-cell,
.mat-header-cell {
  flex: 1;
  overflow:hidden;
  word-wrap: break-word;

  /* border:none; */
  /* border:1px solid black; */
}

mat-row:nth-child(even){
          background-color:#f6f8fa;
          /*  */
          }

   mat-row:nth-child(odd){
          background-color:white;
          }

/* .mat-table-selectable .mat-row:hover
   {
    background: black;
  }
  .mat-row.selected {
    background: black;
  } */
.mat-row.highlight{
  background: #f6eaea;
  color:black;
  /* #d8d3cb; */

   /* font-weight: bold; */
  /* #708090; */
  /* #42A948;  green  */
}

.no-results {
  display: flex;
  justify-content: center;
  padding: 14px;
  font-size: 14px;
  font-weight: bold;
  font-style: italic;
  background-color: rgba(255,255,255,.3);
}
.footer-row {
  font-weight: bold;
}
.mat-paginator{
  background-color: transparent;
}

.pclass{
  padding:.4rem;
  border:1px solid rgba(0,0,0,.3);
  margin:0 .1rem;
  font-weight: normal;


  /* height:1rem; */
}

.center-aligned-title{
  font-size: 1.2rem;
color: blue;
display: flex;
justify-content: center;
padding: .5rem;
background: gray;
opacity: .8;
}
.textwithinborder{
  border: 1px solid rgba(0,0,0,.5);
padding: .4rem;
background: white;
border-radius: .5rem;
}

```
