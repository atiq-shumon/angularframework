Tips for Running an Angular app in IIS
------------------------------------------------
File Downloading
-------------------------------------------
#### add MIME Type

  ##### File name extension:
         .apk
  #####MIME Type:
          application/vnd.android.package-archive     


 404 - File or directory not found
------------------------------------------------

*** Step 1: Install IIS URL Rewrite Module ***

```
   https://www.iis.net/downloads/microsoft/url-rewrite
   
```     

*** Step 2: Add a rewrite rule to web.config ***

```
<configuration>

<system.webServer>

  <rewrite>

    <rules>

      <rule name="Angular Routes" stopProcessing="true">

        <match url=".*" />

        <conditions logicalGrouping="MatchAll">

          <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />

          <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />

        </conditions>

        <action type="Rewrite" url="/icmsuinew/" />

        <!--<action type="Rewrite" url="/" />-->

      </rule>

    </rules>

  </rewrite>

</system.webServer>

</configuration>

```

STEP 3: add web.config link to angular.json: (because after ng build it will skipped)

```
"architect": {
                "build": {
                    "builder": "@angular-devkit/build-angular:browser",
                    "options": {
                         ..........
                        "assets": [
                            "src/favicon.ico",
                            "src/assets",
                            **"src/web.config"**
                        ]

```
