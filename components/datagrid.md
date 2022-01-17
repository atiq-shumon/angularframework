[Important Links]

[FormGroup and Data grid](https://github.com/atiq-shumon/angularframework/blob/master/components/datagridandformgroup.md) || [Adding Grid data to main Form Group](https://github.com/atiq-shumon/angularframework/blob/master/components/datagridandformgroup.md#Adding-grid-to-data-to-main-form-group)




[Page Contents]

#### ts part
```Javascript

displayedColumns: string[] = ['company','product', 'amount','actions'];
 dataSource=new MatTableDataSource<any>();
 
  constructor(...........){
  
  
  }
  
addToGrid(){
  this.dataSource.data = [...this.dataSource.data, {"company":"ctg","product":"bag", "amount":500}];
}

or 
this.dataSource = [newRow, ...this.dataSource];
----------------------------------------------------------------
deletetableItem(row:any,index:any){
    this.dataSource.data.splice(index, 1);
    this.dataSource._updateChangeSubscription();
}

  ```
  ### Htmls
``` html  
 -------------------------------------------
 <button  (click)="addToGrid()" mat-raised-button  style="border-radius:1rem;cursor: pointer;" ><mat-icon>check box</mat-icon>&nbsp;Add</button>
 ------------------------------------------- 
 
  <table #table mat-table [dataSource]="dataSource" class="mat-elevation-z8">

  <!--- Note that these columns can be defined in any order.
        The actual rendered columns are set as a property on the row definition" -->

  <!-- Position Column -->
  <ng-container matColumnDef="company">
    <th mat-header-cell *matHeaderCellDef> Company </th>
    <td mat-cell *matCellDef="let element"> {{element.company}} </td>
  </ng-container>
 <!-- Name Column -->
 <ng-container matColumnDef="product">
  <th mat-header-cell *matHeaderCellDef> Product </th>
  <td mat-cell *matCellDef="let element"> {{element.product}} </td>
</ng-container>

 <!-- Name Column -->
 <ng-container matColumnDef="amount">
  <th mat-header-cell *matHeaderCellDef> Amount </th>
  <td mat-cell *matCellDef="let element"> {{element.amount}} </td>
</ng-container>
  
     <!-- Action Column -->
    <ng-container  matColumnDef="actions">
      <th   mat-header-cell *matHeaderCellDef>
           <!-- <button mat-icon-button color="primary" (click)="addNew()"> -->
             <!-- <mat-icon class="small">add</mat-icon> -->
            <!-- </button> -->
            <!-- <button (click)="addcruditem()" mat-mini-fab>+</button> -->
            <!-- <mat-chip (click)="addcruditem()">Add(+)</mat-chip> -->
            <!-- <div (click)="addcruditem()" >+</div> -->
            <div  (click)="addinputform()" style="background-color:#ed1c24;color:white;cursor:pointer;padding:0 .5rem 0 .5rem;display: inline-flex;justify-content: center;align-items: center;margin:.5rem;"  >
             <mat-icon>add</mat-icon>
             <!-- <div>Add</div> -->
           </div>
          </th>
         <!-- </mat-header-cell> -->

         <td  mat-cell *matCellDef="let row; let i=index;">
            <!-- *ngIf="edit Allow"  *ngIf="tv.isUpdateAllow"-->

           <!-- *ngIf="Delete Allow" -->
           <button mat-icon-button  class="small" color="accent" (click)="deletetableItem(row,i)">
               <mat-icon  class="small" aria-label="Delete">delete</mat-icon>
             </button>
           <!-- *ngIf="View Details Allow" -->
           <!-- <button *ngIf="isViewDetailsAllow"  mat-icon-button  class="small" color="accent" (click)="getviewdetailscrudForm(row)"> -->
               <!-- <mat-icon  style="color: green;" class="small" aria-label="Delete">remove_red_eye</mat-icon> -->
             <!-- </button> -->
         </td>


       </ng-container>

  <tr mat-header-row *matHeaderRowDef="displayedColumns"></tr>
  <tr mat-row *matRowDef="let row; columns: displayedColumns;"></tr>
</table>
  ```
