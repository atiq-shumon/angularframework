[important links]

[Validator learning](https://blog.angular-university.io/angular-custom-validators/)


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
