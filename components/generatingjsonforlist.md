```
let pmtdata= this.salesmodestring.split("~");
    if(pmtdata.length>1){
      this.formGroup.get('salesmode').setValue(pmtdata[0]);
      this.onSalesModeChange({value:pmtdata[0]});
      if(pmtdata[1].indexOf(';')!=='-1')
       {
          let strarr=pmtdata[1].split(';')
          strarr.forEach(element => {
            let arr=element.split(':');
               let json={'paymenttypeoid':arr[0],'paymenttype':arr[1],'amount':arr[2],'reffnumber':arr[3],'date':arr[4],'bankname':arr[6],'bankoid':arr[5],'branchname':arr[7]};
              this.bulksalesmodeservice.addData(json);
          });

      }
      else { /* else of pmtdata[1].indexOf(';')!=='-1') */

        if(pmtdata[1].indexOf(':')!=='-1'){
            let arr=pmtdata[1].split(':');
             let json={'paymenttypeoid':arr[0],'paymenttype':arr[1],'amount':arr[2],'reffnumber':arr[3],'date':arr[4],'bankname':arr[6],'bankoid':arr[5],'branchname':arr[7]};
            this.bulksalesmodeservice.addData(json);
        };
      }
      ```
