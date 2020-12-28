setting basepath in angular(index.html)
-------------------------------------
```
<base href="/">
```
***href="/" means root folder(i.e. 192.168.44.31) in iis or application server***
```
ng build --prod  --base-href="/icmsuinew/"
```
***means base href that is ="/" then icmsuinew/ so full access path 192.168.44.31/icmsuinew/***

setting basepath in angular(angular.json)
-------------------------------------
```
"root": "/"
```
deploy script: [link](https://stackoverflow.com/questions/55402751/angular-app-has-to-clear-cache-after-new-deployment/55403095)
----------------------------
```
 ng build --prod --aot --outputHashing=all

```

File Downloading
-------------------------------------------
#### add MIME Type

  ##### File name extension:
         .apk
  ##### MIME Type:
          application/vnd.android.package-archive     
