setting basepath in angular(index.html)
-------------------------------------
```
<base href="/">

ng build --prod  --base-href="/icmsuinew/"

```
setting basepath in angular(angular.json)
-------------------------------------
```
"root": "/"
```
deploy script:
----------------------------
```
 ng build --prod --aot --outputHashing=all

```
