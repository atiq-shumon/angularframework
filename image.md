Reading and showing data from url
---------------------------------------------
service
---------------------
```
import { Injectable } from '@angular/core';
import {Observable} from 'rxjs';
// import {CONFIGURATION} from '.../model/constants/app.constants';

//import {HttpModule,Http, Response,Headers,RequestOptions} from '@angular/http/Common';
import {HttpClient, HttpErrorResponse,HttpHeaders  } from '@angular/common/http';
@Injectable()
export class URLToImageServiceProvider {
// private userServiceURL=CONFIGURATION.baseUrls.server;
//private userServiceURL=CONFIGURATION.baseUrls.serverlocalacms;
  constructor(public httpClient: HttpClient) { }
  
   getImage(imageUrl: string): Observable<Blob> {
        return this.httpClient.get(imageUrl, { responseType: 'blob' });
    }
  // private handleError(error:Response)
  // {
  //   // console.error(error);
  //    return observableThrowError(error.json()||"Server Error");
  // }
   
}
```

```
 let imgUrl="https://i.picsum.photos/id/866/200/300.jpg?hmac=rcadCENKh4rD6MAp6V_ma-AyWv641M4iiOpe1RyFHeI";
 this.imageService.getImage(imgUrl).subscribe(data => {
   this.createImageFromBlob(data);
 // this.isImageLoading = false;
    // console.log(data)
   }, error => {
     // this.isImageLoading = false;
       console.log(error);
});
 //let img="https://i.picsum.photos/id/866/200/300.jpg?hmac=rcadCENKh4rD6MAp6V_ma-AyWv641M4iiOpe1RyFHeI";
  };

  createImageFromBlob(image: Blob) {
    let reader = new FileReader();
    reader.addEventListener("load",
      () => {
        this.base64Image= reader.result.toString();
        this.imageForm.get("ImageFileId").setValue(this.base64Image);
      },
      false);

    if (image) {
      if (image.type !== "application/pdf")
        reader.readAsDataURL(image);
    }
  }
```
