setting basepath in angular(index.html)
-------------------------------------
```
<base href="/">

means root folder in iis or application server


ng build --prod  --base-href="/icmsuinew/"

```
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
