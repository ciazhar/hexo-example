---
title: security
date: 2017-08-28 15:40:16
tags:
---


# Session
```
Router router = Router.router(vertx);

    router.route().handler(CookieHandler.create());
    router.route().handler(SessionHandler
        .create(LocalSessionStore.create(vertx))
        .setCookieHttpOnlyFlag(true)
        .setCookieSecureFlag(true)
    );

    router.route().handler(routingContext -> {

      Session session = routingContext.session();

      Integer cnt = session.get("hitcount");
      cnt = (cnt == null ? 0 : cnt) + 1;

      session.put("hitcount", cnt);

      routingContext.response().end("Hitcount: " + cnt);
    });

    vertx.createHttpServer().requestHandler(router::accept).listen(8080);
```

# Security Header
```
public class App extends AbstractVerticle {

  @Override
  public void start() {

    Router router = Router.router(vertx);
    router.route().handler(ctx -> {
      ctx.response()
          // do not allow proxies to cache the data
          .putHeader("Cache-Control", "no-store, no-cache")
          // prevents Internet Explorer from MIME - sniffing a
          // response away from the declared content-type
          .putHeader("X-Content-Type-Options", "nosniff")
          // Strict HTTPS (for about ~6Months)
          .putHeader("Strict-Transport-Security", "max-age=" + 15768000)
          // IE8+ do not allow opening of attachments in the context of this resource
          .putHeader("X-Download-Options", "noopen")
          // enable XSS for IE
          .putHeader("X-XSS-Protection", "1; mode=block")
          // deny frames
          .putHeader("X-FRAME-OPTIONS", "DENY");
    });

    vertx.createHttpServer().requestHandler(router::accept).listen(8080);
  }
}
```

# CSFR
```
public class App extends AbstractVerticle {

  @Override
  public void start() {

    Router router = Router.router(vertx);

    router.route().handler(CookieHandler.create());
    router.route().handler(SessionHandler
        .create(LocalSessionStore.create(vertx))
        .setCookieSecureFlag(true)
    );
    router.route().handler(CSRFHandler.create("not a good secret"));

    router.route().handler(ctx -> {
      ...
    });
```
# Limit Upload
```
public class App extends AbstractVerticle {

  private static final int KB = 1024;
  private static final int MB = 1024 * KB;

  @Override
  public void start() {

    Router router = Router.router(vertx);
    router.route().handler(BodyHandler.create().setBodyLimit(50 * MB));
```

