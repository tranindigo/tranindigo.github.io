---
title: "Angular HTTP Interceptors: Modifying Request Headers"
date: "2021-02-17"
categories: 
  - "angular"
tags: 
  - "angular-8"
  - "javascript"
  - "spa"
---

In newer versions of Angular, HTTPInterceptor is an interface which intercepts and handles an HttpRequest or HTTPResponse, which allows you to transform the outgoing request or incoming response. This may be useful when you want to inject a header into your HTTPRequest that contains your authorization token or any other important changes to the request that is relevant to your business logic.

Some use cases for HTTP Interceptor may be:

1. Catch HTTP responses to do some custom formatting (i.e. convert CSV to JSON) before handing the data over to your service/component
2. Logging all HTTP requests/responses
3. Like I mentioned above, you can use an interceptor to add a custom header

Let's break it down and concretely see how you can do this. First, you'll need to import `HTTP_INTERCEPTOR` in your `app.module.ts` file and then add it in the `providers` array:

```javascript
@NgModule({  
  bootstrap: \[AppComponent\],  
  imports: \[ ... \],  
  providers: \[{  
    provide: HTTP\_INTERCEPTORS,  
    useClass: HttpTokenInterceptor,  
    multi: true  
  }\]  
})
```
The `HttpTokenInterceptor`, which implements the `HttpInterceptor` interface, will handle all logic relevant to the interceptor. It looks like this:

```javascript
import { Injectable } from '@angular/core';  
import { HttpRequest, HttpHandler, HttpEvent, HttpInterceptor } from '@angular/common/http';
import { Observable } from 'rxjs/Observable';

@Injectable()  
export class TokenInterceptor implements HttpInterceptor { 

constructor() {} 

intercept(request: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {  
    request = request.clone({  
      setHeaders: {  
        Authorization: `Bearer ${ a_jwt_token }`  
      }  
    }); 
    return next.handle(request);  
  }  
}
```

The `intercept` method will perform the necessary changes to the request. In our example, the `intercept` method clones the request and assigns a new `Authorization` header which contains a JWT token that will allow us to authenticate into an API. This will make it so that we don't have to manually add an `Authorization` header every API request.

And that's all you have to do to modify a HTTP request! Easy, huh?
