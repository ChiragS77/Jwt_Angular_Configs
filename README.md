Http Interceptor :
This code is an Angular HTTP Interceptor, which is used to intercept and modify HTTP requests made by the Angular application before they are sent to the server.


1. What the Method Does
The intercept method is:

Part of the HttpInterceptor interface.
Automatically invoked for every HTTP request sent from the application.
Used here to add an Authorization header containing a JWT token (if available) to authenticated requests.

### Auth Interceptor ##
export class AuthInterceptor implements HttpInterceptor {

  intercept(request: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const currentUser = JSON.parse(localStorage.getItem('currentUser') || '{}');
    if (currentUser && currentUser.token) {
      request = request.clone({
        setHeaders: {
          Authorization: `Bearer ${currentUser.token}`
        }
      });
    }
    return next.handle(request);
  }
}
