---
title: Integrasi Spring dan Oauth2 + JWT
date: 2017-05-27 15:30:21
categories:
  - Pemrograman
  - Spring
---
![](/images/springboot.png)

# Gambaran Umum
Aplikasi yang akan kita buat nantinya akan dibagi menjadi beberapa aplikasi kecil dengan fungsinya masing-masing. Diantaranya adalah :
- Resource Server. Aplikasi ini menyediakan resource yang dibutuhkan oleh user.
- Authorization Server. Aplikasi ini menyediakan layanan otorisasi.
- Aplikasi Client. Aplikasi yang dipakai oleh client. Dapat berupa aplikasi web ataupun native.

## Konfigurasi Resource Server ##
- Tambahkan dependeny OAuth2 dan JWT(resource-server/pom.xml)
  ```xml
    <dependency>
        <groupId>org.springframework.security.oauth</groupId>
        <artifactId>spring-security-oauth2</artifactId>
        <version>2.0.7.RELEASE</version>
    </dependency>
    <dependency>
				<groupId>org.springframework.security</groupId>
				<artifactId>spring-security-jwt</artifactId>
		</dependency>
  ```
- Buat class KonfigurasiResourceServer (resource-server/src/main/java/domain/config/KonfigurasiResourceServer.java)
  ```java
  @EnableResourceServer
  public class KonfigurasiResourceServer extends ResourceServerConfigurerAdapter{

  }
  ```
- override methode untuk authorisasi (resource-server/src/main/java/domain/config/KonfigurasiResourceServer.java/ResourceServerConfiguration).
  ```java
  @Override
  public void configure(HttpSecurity http) throws Exception {
      http.authorizeRequests().anyRequest().authenticated()
      ;
  }
  ```
- Konfigurasi JWT
  ```yml
  security.oauth2.resource.jwt.key-uri=http://localhost:10000/oauth/token_key
  ```
## Konfigurasi Authorization Server ##
- Tambahkan dependeny OAuth2 dan JWT(resource-server/pom.xml)
  ```xml
    <dependency>
        <groupId>org.springframework.security.oauth</groupId>
        <artifactId>spring-security-oauth2</artifactId>
        <version>2.0.7.RELEASE</version>
    </dependency>
    <dependency>
				<groupId>org.springframework.security</groupId>
				<artifactId>spring-security-jwt</artifactId>
		</dependency>
  ```
- setup port (auth-server/src/main/resources/application.properties)
  ```yml
    server.port=10000
  ```
- setup session cookies(auth-server/src/main/resources/application.properties)
```yml
server.session.cookie.name=AUTHSERVER
```
- membuat class KonfigurasiAuthorizationServer (auth-server/src/main/java/domain/config/KonfigurasiAuthorizationServer.java)
  ```java
    @Configuration
    public class KonfigurasiAuthorizationServer {

    }
  ```
- Membuat inner class
- Setup AuthenticationManager
  ```
    @Autowired
    @Qualifier("authenticationManagerBean")
    private AuthenticationManager authenticationManager;
  ```
- Buat methode (auth-server/src/main/java/domain/config/KonfigurasiAuthorizationServer.java/AuthorizationServerConfiguration). Methode ini berfungsi untuk menyimpan token yang nanti akan di cek kembali
  ```
    @Override
    public void configure(AuthorizationServerEndpointsConfigurer endpoints)
            throws Exception {
        endpoints
                .tokenStore(new InMemoryTokenStore())
                .authenticationManager(authenticationManager);
    }
  ```
- Buat methode (auth-server/src/main/java/domain/config/KonfigurasiAuthorizationServer.java/AuthorizationServerConfiguration). Methode ini berfungsi untuk menentukan role apa saja yang dapat mendapat mengakses check token
  ```
    @Override
    public void configure(AuthorizationServerSecurityConfigurer oauthServer) throws Exception {
        oauthServer.checkTokenAccess("hasRole('CLIENT')");
    }
  ```
- Buat methode (auth-server/src/main/java/domain/config/KonfigurasiAuthorizationServer.java/AuthorizationServerConfiguration). Methode ini berisi list role client berasarkan grant tye
  ```
    @Override
    public void configure(ClientDetailsServiceConfigurer clients) throws Exception {
      clients
        .inMemory()
        .withClient("clientauthcode")
          .secret("123456")
          .authorizedGrantTypes("authorization_code","refresh_token")
          .authorities("CLIENT")
          .scopes("read","write")
          .resourceIds(RESOURCE_ID)
        .and()
        .withClient("clientcred")
          .secret("123456")
          .authorizedGrantTypes("client_credentials")
          .scopes("trust")
          .resourceIds(RESOURCE_ID)
        .and()
        .withClient("clientapp")
          .secret("123456")
          .authorizedGrantTypes("password")
          .scopes("read","write")
          .resourceIds(RESOURCE_ID)  
        .and()
        .withClient("jsclient")
          .secret("123456")
          .authorizedGrantTypes("implicit")
          .authorities("CLIENT")
          .scopes("read","write")
          .resourceIds(RESOURCE_ID)
          .redirectUris("http://localhost:20000/implicit-client")
          .accessTokenValiditySeconds(60* 60 *24)
          .autoApprove(true);
    }
  ```
- Konfigurasi Security (auth-server/src/main/java/domain/config/KonfigurasiSecurity)
  ```
    @Override
        @Bean
        public AuthenticationManager authenticationManagerBean() throws Exception {
            return super.authenticationManagerBean();
        }
  ```


# Flow untuk masing masing role clint #
Perlu diketahui authorization server akan jalan di port 10000 dan resource server akan jalan di port 8080. OAuth 2 sendiri menyediakan 4 role yaitu :
- Authorization Code (Akses yang dalam mendapatkan resource memerlukan kode)
- Username Password
- Client Credential (Akses yang memungkinkan client tidak perlu login untuk mendapatkan akses)
- Client Impicit (Akses yang biasanya digunakan untuk mendapatkan resource berupa js)

## Authorization Code ##
Karena kita belum memiliki aplikasi client maka kita akan langsung redirect ke authorization server dengan memasukkan url
  ```
    http://localhost:10000/oauth/authorize?client_id=clientauthcode&response_type=code&redirect_uri=http://localhost:8080/api/halo
  ```
  Note : url tersebut akan diproses oleh auth server (http://localhost:10000/oauth/authorize) dengan parameter client_id yaitu `clientauthcode`, response_type berupa `code` dan ingin request ke `http://localhost:8080/api/halo`
- Kita akan langsung di redirect ke `http://localhost:10000/login`. Kita diminta untuk memasukkan otorisasi login
- Lalu akan muncul form approval dengan scope `read` dan `write`, untuk approval ini dapat dikonfigurasi agar tidak tampil atau otomatis authorize.
- Lalu akan muncul url sebagai berikut
  ```
    http://localhost:8080/api/halo?code=Ixd8e
  ```
  Kemudian kita ambil code tersebut
- Lalu ditukarkan kode tersebut dengan access token dengan cara mengakses kembali ke auth server dengan mencantumkan
  - Methode HTTP berupa `POST`
  - client_id berupa `clientauthcode` dan secret `123456`
  - Url berupa `http://localhost:10000/oauth/token`
  - Header berupa `application/json`
  - data yaitu:
  	- grant_type berupa `authorization_code`
  	- code berupa `Ixd8e`
  	- redirect_uri berupa `http://localhost:8080/api/halo`
- Setelah itu kita akan mendapatkan data sebagai berikut :
  - access_token : `blablabla`
  - token_type : `bearer`
  - refresh_token : `baba`
  - expires_in : `43199`
  - scope : `read`,`write`
- Lalu akses ke resource server dengan menambahkan access token yang telah kita dapatkan tadi dengan url `http://localhost:8080/api/halo?access_token=blablabla`
- Selamat anda sudah dapat mengakses resource.
	Sebenarnya sebelum token mendapatkan resource tersebut resource server melakukan pengecekan ke authorization server terhadap acces token tadi apakah valid atau tidak.Namun perlu diketahui bahwa saat ini kedua aplikasi berjalan di port yang berbeda (auth server port 10000, dan resource server di port 8080) sehingga tidak dapat sharing token via memory.
Solusinya adalah :
- Token tadi akan disimpan ke database menggunakan jdbc token store oleh auth server. Lalu resource server akan diarahkan ke database tersebut. Tetapi ada kalanya resource server tidak dapat mendapatkan akses ke database.
- Menggunakan RemoteTokenServices yang ada pada setting KonfigurasiResourceServer
  ```
    @Override
    public void configure(ResourceServerSecurityConfigurer resources) {
        RemoteTokenServices tokenService = new RemoteTokenServices();
        tokenService.setClientId("clientauthcode");
        tokenService.setClientSecret("123456");
        tokenService.setCheckTokenEndpointUrl("http://localhost:10000/oauth/check_token");
        resources
                .resourceId(RESOURCE_ID)
                .tokenServices(tokenService);
    }
  ```
  resource server akan mengarahkan ke url `http://localhost:10000/oauth/check_token` dengan menambahkan client id berupa `clientauthcode`, secret berupa `123456` dan access_token menggunakn methode GET. sehingga resource server mendapat data sebagai berikut :
  - rid :  `belajar`
  - exp : `14441`
  - username : `endy`
  - authorities : `[ROLE_OPERATOR]`,`[ROLE_SUPERVISOR]`
  - client_id : `clientauthcode`
  - scope : `read`,`write`
  dari sini resource server tahu role dari user tersebut dan dapat memutuskan user tersebut dapat mengakses resource tersebut atau tidak

## Username Password ##
- Kita akses auth server dengan mencantumkan
  - Methode HTTP berupa `POST`
  - client_id berupa `clientapp` dan secret `123456`
  - Url berupa `http://localhost:10000/oauth/token`
  - Header berupa `application/json`
  - data yaitu:
  	- client_id berupa `clientapp`
  	- grant_type berupa `password`
  	- username berupa `endy`
    - password berupa `123`
- Setelah itu kita akan mendapatkan data sebagai berikut :
  - access_token : `blablabla`
  - token_type : `bearer`
  - expires_in : `43199`
  - scope : `read`,`write`
- Kemudian Kita akses auth server dengan mencantumkan
  - Methode HTTP berupa `GET`
  - client_id berupa `clientapp` dan secret `123456` dan authorization header `Bearer blablabla`
  - Url berupa `http://localhost:8080/api/halo`
  - Header berupa `application/json`
- Selamat anda sudah dapat mengakses resource.

## Client Credential ##
- Kita akses auth server dengan mencantumkan
  - Methode HTTP berupa `POST`
  - client_id berupa `clientcred` dan secret `123456`
  - Url berupa `http://localhost:10000/oauth/token`
  - Header berupa `application/json`
  - data yaitu:
  	- client_id berupa `clientcred`
  	- grant_type berupa `client_credentials`
- Setelah itu kita akan mendapatkan data sebagai berikut :
  - access_token : `blablabla`
  - token_type : `bearer`
  - expires_in : `43199`
  - scope : `read`,`write`
- Kemudian Kita akses auth server dengan mencantumkan
  - Methode HTTP berupa `GET`
  - client_id berupa `clientcred` dan secret `123456` dan authorization header `Bearer blablabla`
  - Url berupa `http://localhost:8080/api/halo`
  - Header berupa `application/json`
  - data yaitu:
  	- client_id berupa `clientcred`
- Perlu diketahui karena client cred ini tidak menggunakan username dan password maka dia tidak dapat digunakan dalam aplikasi ini karena resource server telah kita setting hanya untuk menerima authentifikasi dari user dengan role operator.

## Implicit Client ##
- Karena kita belum memiliki aplikasi client maka kita akan langsung redirect ke authorization server dengan memasukkan url
  ```
    http://localhost:10000/oauth/authorize?client_id=jsclient&response_type=token&redirect_uri=http://localhost:2000/implicit-client
  ```
  Note : url tersebut akan diproses oleh auth server (http://localhost:10000/oauth/authorize) dengan parameter client_id yaitu `jsclient`, response_type berupa `token` dan ingin request ke `http://localhost:2000/implicit-client`
- Kita akan langsung di redirect ke `http://localhost:10000/login`. Kita diminta untuk memasukkan otorisasi login
- Selanjutnya kita akan mendapatkan url `http://localhost:2000/implicit-client/#access_token=blabla&token_type=bearer`
- Kemudian Kita akses auth server dengan mencantumkan
  - Methode HTTP berupa `GET`
  authorization header `Bearer blablabla`
  - Url berupa `http://localhost:8080/api/halo`
  - Header berupa `application/json`

# Mendapatkan Informasi User #
- Pertama class buat controller(resource-server/src/main/java/domain/controller/InfoController)
  ```
    @RestController
    @EnableResourceServer
    public class InfoController{

    }
  ```
- Buat methode untuk mengakses info user
  ```
    @RequestMapping("/userinfo")
    public Principal user info (Principal principal){
      return principal;
    }
  ```
- Untuk mengaksesnya kita login dulu dengan menggunakan grant type clientauthcode sampai kita mendapatkan access tokenya
- Setelah mendapatkanya masukkan url `http://localhost:8080/userinfo?access_token=blabla`

# Membuat Aplikasi Client Auhtorization Code#
Pertama kita akan membuat aplikasi client authcode sedehana menggunakan Spring Framework.
Step by Step nya adalah sebagai berikut :
- Download Setup projek di `http://start.spring.io`
- Isi projek metadata berupa :
  * artifact id :
  * groupId :
- Isi dependency yang dubutuhkan berupa :
  * web
  * thymeleaf
- Download lalu pindahkan ke text editor
- Kita coba bikin Controller sebagi resources (client-authcode/src/main/java/domain/controller/InfoController)
  ```
    @Controller
    public class InfoController {


    }
  ```
- Kita bikin methode untuk di proses ke user. Methode ini akan mengembalikan waktu sekarang menggunakan variabel `waktu`. methode ini dapat diakses di url /halo.(client-authcode/src/main/java/domain/controller/InfoController)
  ```
    @RequestMapping("/info")
    public void info(Model m){
      m.addAttribute("waktu", new Date().toString());
    }
  ```
- Kita bikin UI untuk mengeluarkan informasi dari methode halo yang telah buat tadi.(client-authcode/src/main/resources/templates/halo.html)
  ```
    <html>
        <head>
            <title>Halo Spring Boot</title>
        </head>
        <body>
            <h1>Halo Spring Boot</h1>
            <h2>Waktu saat ini : <span th:text="${waktu}"></span></h2>
        </body>
    </html>
  ```
## Proteksi Client Authorization Code Dengan Spring Security
- Lalu coba kita proteksi Resource Server kita menggunakan Spring Security dengan menambahkan dependency di pom.xml. (client-authcode/pom.xml)
  ```
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.security.oauth</groupId>
        <artifactId>spring-security-oauth2</artifactId>
        <version>2.0.7.RELEASE</version>
    </dependency>
  ```
  Pada keadaan ini kita akan diminta otorisasi jika kita mengakses di browser dengan username : `user` dan password yang ada pada CLI. karena tidak efisien mengabaikan otorisasi.
- Buat class untuk konfigurasi otorisasi (/client-authcode/src/main/java/domain/config/KonfigurasiSecurity)
  ```
    @Configuration
    public class KonfigurasiSecurity  extends WebSecurityConfigurerAdapter {

    }
  ```
- Override methode configure (/client-authcode/src/main/java/domain/config/KonfigurasiSecurity). Methode untuk mengabaikan otorisasi
  ```
    @Override
    public void configure (WebSecurity web) throws Exception{
      web.ignoring().anyRequest();
    }
  ```
- Buat class untuk konfigurasi OAuth Client (/client-authcode/src/main/java/domain/config/KonfigurasiOauth2Client).
  ```
    @Configuration
    @EnableOAuth2Client
    public class KonfigurasiOauth2Client{

    }
  ```
- Konfigurasi untuk Oauth2 Client (/client-authcode/src/main/java/domain/config/KonfigurasiOauth2Client)
  ```
    private String urlAuthorization = "http://localhost:10000/oauth/authorize";
    private String urlToken = "http://localhost:10000/oauth/token";

    @Bean
    public OAuth2RestOperations restOperations(OAuth2ClientContext context){
        OAuth2RestTemplate restTemplate = new OAuth2RestTemplate(resource(),context);
        return restTemplate;
    }

    @Bean
    public OAuth2ProtectedResourceDetails resource(){
        AuthorizationCodeResourceDetails resourceDetails= new AuthorizationCodeResourceDetails();
        resourceDetails.setClientId("clientauthcode");
        resourceDetails.setClientSecret("123456");
        resourceDetails.setUserAuthorizationUri(urlAuthorization);
        resourceDetails.setAccessTokenUri(urlToken);
        return resourceDetails;
    }
  ```
- Membuat Controler untuk mengakses api dari resource server
  ```
    @Autowired
    private OAuth2RestOperations restOperations;

    private String urlApi = "http://localhost:8080/api/halo";

    @RequestMapping("/api")
    @ResponseBody
    public Map<String, Object> api (){
      Map<String, Object> hasil = restOperations.getForObject(urlApi, HashMap.class);
      return hasil;
    }
  ```
- Tambahkan konfigurasi context path dan server port
  ```
  server.port=9090
  server.context-path=/authcode
  ```
  Keterangan :
  membuat context-path wajib dikarenakan agar tidak terjadi error saat penyimpanan cookies

# Membuat Aplikasi Client Implicit
Pertama kita akan membuat aplikasi client authcode sedehana menggunakan Spring Framework.
Step by Step nya adalah sebagai berikut :
- Download Setup projek di `http://start.spring.io`
- Isi projek metadata berupa :
  * artifact id :
  * groupId :
- Isi dependency yang dubutuhkan berupa :
  * web
- Download lalu pindahkan ke text editor

### Setting Server port dan Server Context Path
```
  server.port=7070
  server.context-path=/implicit
```
### Membuat HTML sederhana
```
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <title>Oauth Client Implicit</title>
  </head>
  <body>
      <div>
          <h1>Oauth Client Implicit</h1>
      </div>
  <body>
```
### Setup Angular JS
- tambahkan file angualar js ke project
- buat file aplikasi js
  ```
    var app = angular.module('ImplicitApp',[]);
    app.controller('DummyController',function(){
    )};
  ```
- include ke html
  ```
    <body ng-app="ImplicitApp">
    <div ng-controller="DummyController">
        <h1>Oauth Client Implicit</h1>
    </div>

    <script src="js/angular.min.js"></script>
    <script src="js/aplikasi.js"></script>
  </body>
  ```
- test angular js
  ```
    <div ng-controller="DummyController">
        <h1>Oauth Client Implicit</h1>
        Masukkan Nama Anda : <input type="text" ng-model="nama"><br>
        Selamat Datang  {{nama}}
    </div>
  ```
### Impicit Client
- angular js
```
  app.controller('DummyController',function($http, $scope, $window, $location){
      var urlResourceServer = "http://localhost:8080/api/halo";
      var urlAuthServer = "http://localhost:10000/oauth/authorize?client_id=jsclient&response_type=token";

      $scope.bukaLoginPage = function () {
          $window.location.href = urlAuthServer;
      };

      $scope.ambilTokenDariServer = function () {
          var location = $location.url(); /// ngambil hash yang isinya #access_token=f2b50438-2c3a-4637-b6b9-e469543ff26d&token_type=bearer&expires_in=86399&scope=read%20write
          console.log("Location : "+location);
          var params = location.split("&");///jadi array yang isinya [access_token=f2b50438-2c3a-4637-b6b9-e469543ff26d , token_type=bearer , expires_in=86399 , scope=read%20write]
          console.log("Param : "+params);
          var tokenParam = params[0];///ambile param indek ke 0 yaitu access token
          console.log("token Param : "+tokenParam);
          var token = tokenParam.split("=")[1];
          console.log("token : "+token);
          $window.sessionStorage.setItem('token',token);
      };

      $scope.requestKeResourceServer = function () {

          var token = $window.sessionStorage.getItem('token');
          if (!token){
              alert('Belum Login');
              return;
          }
          $http.get(urlResourceServer+"?access_token="+token).then(
              function (response) {
                  $scope.responseDariServer = response.data;
              },
              function (response) {
                  alert('Error Code'+response.status+', Error Text : '+response.statusText);
              }
          );
      };
  });
```
- html
```
  <div ng-controller="DummyController">
      <h1>Oauth Client Implicit</h1>
      Masukkan Nama Anda : <input type="text" ng-model="nama"><br>
      Selamat Datang  {{nama}}

      <hr>

      <button ng-click="bukaLoginPage()">Login ke Server</button>
      <button ng-click="ambilTokenDariServer()">Ambil Token dari Server</button>

      <hr>

      <button ng-click="requestKeResourceServer()">Merequest ke Resource Server</button>
      <div>
          {{responseDariServer}}
      </div>
  </div>
```
- Note
Untuk mengatasi masalah CORS pastikan api anda telah mengunakan anotasi `@CrossOrigin`
