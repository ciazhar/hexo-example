---
title: Authorization and Authentification Service
date: 2017-05-20 21:03:29
categories:
  - Pemrograman
  - Angular
---
![](/images/angular.png)
# Membuat service otorisasi

- Membuat shared module.
```
ng g module shared
```
- Membuat service auth di dalam shared module
```
cd shared
ng g service auth
```
- Membuat service (auth.service.ts)
```
import { Injectable } from '@angular/core';

@Injectable()
export class AuthService {

  constructor() { }

  isLogin() : boolean{
    return localStorage.getItem("authentification")!=null;
  }

  getUserInfo() : any{
    return localStorage.getItem("authentification");
  }

  login(username : string, password : string) : boolean{
    if(username == "admin" && password == "123"){
      let userObject = {
        username: "admin",
        permissions: [
          "TRANSAKSI_VIEW",
          "TRANSAKSI_EDIT"
        ]
      }
      localStorage.setItem("authentification",JSON.stringify(userObject));
      return true;
    }
    return false;
  }

  logout(){
    localStorage.removeItem("authentification");
  }
}
```
- Import auth service (shared.module.ts)
```
import { AuthService } from './auth.service';
```
- Definisikan di ngModule sebagai exports
```
@NgModule({
  exports: [
    AuthService
  ]
})
```
- Membuat file authguard.ts
```
import { Injectable }     from '@angular/core';
import { CanActivate, CanActivateChild }    from '@angular/router';

import { AuthService } from './auth.service';

@Injectable()
export class AuthGuard implements CanActivate, CanActivateChild {

  constructor(private auth : AuthService){}

  canActivate() {
    console.log('AuthGuard#canActivate called');
    return this.auth.isLogin();
  }

  canActivateChild() {
	  console.log('AuthGuard#canActivateChild called');
      return this.canActivate();
  }
}
```
- import shared module (app.module.ts)
```
import { AuthService } from './shared/auth.service';
import { AuthGuard } from './shared/authguard';
```
- definisikan di ngModule sebagai provider
```
@NgModule({
  providers: [
    AuthGuard, AuthService
  ],
})
```
- implement ke routing (app.module.ts)
```
const routingAplikasi: Routes = [
  { path: "about", component: AboutComponent, canActivate : [AuthGuard] },
  { path: "transaksi", redirectTo: "/transaksi", pathMatch: "full", canActivateChild : [AuthGuard]},
  { path: "**", component: WelcomeComponent }
]
```
- implement ke routing (transaksi.module.ts)
```
const routingTransaksi : Routes = [
  { path: "transaksi/beli", component: BeliComponent, canActivate : [AuthGuard] },
  { path: "transaksi/jual", component: JualComponent, canActivate : [AuthGuard] },
  { path: "transaksi/rekap", component: RekapComponent }
]
```

## Mengatur kondisi layout jika belum login
Apabila anda ingin membuat suatu menu tidak ditampilkan jika belum login, anda dapat menggunakan fungsi `isLogin` yang telah kita buat tadi. Anda cukup menyisipkan menu yang tidak ingin ditampilkan diantara tag yang berisi kondisi isLogin. Berikut adalah contoh penggunaannya :
```html
<span *ngIf="authService.isLogin()"> <a routerLink="path">Menu yang tidak ingin ditampilkan</a> </span>
```
Kemudian definisikan service pada konstruktor pada module.ts nya.
```
constructor(private authService : AuthService) { }
```
Jangan lupa di import AuthService nya

# Membuat Form Login
- membuat component login form
```
cd shared
ng g component login
```
- membuat html nya
```
<div class="container">
  <form class="form-signin">
   <h2 class="form-signin-heading">Please sign in</h2>
   <label for="username" class="sr-only">Username</label>
   <input [(ngModel)]="username" type="text" id="username" name="username" class="form-control" placeholder="Username" required autofocus>
   <label for="password" class="sr-only">Password</label>
   <input [(ngModel)]="password" type="password" id="password" name="password" class="form-control" placeholder="Password" required>
   <button class="btn btn-lg btn-primary btn-block" (click)=login()>Sign in</button>
 </form>
</div>
```

- import shared.module
```
import { FormsModule } from '@angular/forms';
import { LoginComponent } from './login/login.component';
```
- definisikan
```
@NgModule({
  imports: [
    FormsModule
  ],
  declarations: [LoginComponent],
})

```

- import app.module
```
import { LoginComponent } from './shared/login/login.component';
```
- definisikan
```
@NgModule({
  declarations: [LoginComponent],
})

```
- routing
```
{ path: "login", component: LoginComponent},
```


- method login login.component
```
username : string;
password : string;

login(){
  let apa = this.authService.login(this.username, this.password);
}
```
- constructor
```
constructor (private authService : AuthService){}
```
- import
```
import { AuthService } from '../auth.service';
```

# Membuat Logout
```
<li *ngIf="authService.isLogin()"><a (click)="logout()">Keluar</a></li>
```
```
logout(){
  this.authService.logout();
  this.router.navigate(['login']);
}
```
```
import { AuthService } from '../shared/auth.service';
import { Router }   from '@angular/router';
```
