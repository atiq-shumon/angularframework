setting basepath in angular(index.html) || [PWA](https://github.com/atiq-shumon/react/blob/main/installationanddeployment/PWA/pwa.md)
-------------------------------------
```
<base href="/">
```
***href="/" means root folder(i.e. http://192.168.44.31:80(default port)) in iis or application server***
```
ng build --prod  --base-href="/advancederp/" or <base href="/icmsuinew">  and productiton command  : ng build --prod

ng build --prod  --base-href="/cssapcountersales/"
dist user: 005724
dist pass:737032
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
