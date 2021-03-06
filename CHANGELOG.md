##v0.5.21

* Fix connection timeout when throwing/returning an ErrorResponse within a Future ([#83](https://github.com/luizmineo/redstone.dart/issues/83))
* Fix crash when reading text files in multipart requests ([#77](https://github.com/luizmineo/redstone.dart/issues/77))

##v0.5.20

* Update `route_hierarchical` version constraint.

##v0.5.19
* Fix: Error when setting `Interceptor.parseRequestBody = true` (Thanks to [platelk](https://github.com/platelk). See PR [#46](https://github.com/luizmineo/redstone.dart/pull/46)).

## v0.5.18
* Updated to Grinder v0.6.1 (see [documentation](https://github.com/luizmineo/redstone.dart/wiki/Deploy))

## v0.5.17
* Updated dependencies.
* Added the `autoCompress` parameter to the `start()` function.
* Added `Route.statusCode` and `DefaultRoute.statusCode` parameters.

**Note:** this version requires Dart 1.7 or above

## v0.5.16
* Fix: Setting a new value in a `QueryMap` with the dot notation is not working properly.

## v0.5.15
* Fix: Correctly log an exception when no stack trace is provided

## v0.5.14
* Fix: `Manager.findMethods()` should include inherited methods.

## v0.5.13
* Improved plugin API: 
    * Added the `Manager.getInjector()` and `Manager.createInjector()` methods, which allow plugins to retrieve objects from di modules more easily.
    * Added the `Manager.findFunctions()`, `Manager.findClasses()` and `Manager.findMethods()` methods, which allow plugins to scan imported libraries.
    * Added the `Manager.getShelfHandler()` and `Manager.setShelfHandler()` methods, which allow plugins to access and replace the current installed shelf handler.

## v0.5.12
* New feature: If a route has `matchSubPaths = true`, the requested subpath can be assigned to a parameter (see issue #36).

## v0.5.11
* Minor performance fix: Redstone.dart shouldn't create a new `shelf.Pipeline` per request.

## v0.5.10
* Upgraded to di 2.0.1

## v0.5.9
* Fix: Redstone.dart can't be used with shelf_web_socket (issue #30).

## v0.5.8+1
* Fixed docgen issue (see [dartdocs log](http://www.dartdocs.org/buildlogs/b-4066095f44173ae2e2ca3bb6a2f72-startupscript.log))

## v0.5.8
* Added support for https (Thanks to [vicb](https://github.com/vicb) PR #26, see [documentation](https://github.com/luizmineo/redstone.dart/wiki/Server-Configuration#secure-connections-https))
* Code cleanup (Thanks to [vicb](https://github.com/vicb) PR #29)
* Fix: Properly handle error responses produced by a shelf handler

## v0.5.7+2
* Improved error handling. See issue #24.

## v0.5.7+1
* Fixed docgen issue (see [dartdocs log](http://www.dartdocs.org/buildlogs/b-324b8609c46a0a8b9060d0b59539a-startupscript.log))

## v0.5.7
* Improved plugin API:
    * It's now possible to inspect installed routes, interceptors, error handlers and groups.
    * Added the `Manager.addRouteWrapper()` method, which allows plugins to modify routes that are annotated with a specific annotation.

## v0.5.6
* Fixed logging issues.

## v0.5.5+1
* Fixed issue with docgen.

## v0.5.5
* Added the `ErrorResponse` class. A route can return or throw an ErrorResponse, to respond a request with a status code different than 200. 

## v0.5.4
* Fix: Response processors are not being invoked when a route returns a `Future` (Plugin API).
* Code cleanup (Thanks to [vicb](https://github.com/vicb) PR #20)
* Added the `QueryMap` class, a Map wrapper that allows the use of the dot notation to retreive its values (Thanks to [digitalfiz](https://github.com/digitalfiz) issue #18)
    * `app.request.queryParams`, `app.request.headers` and `app.request.attributes` now returns a QueryMap.
    * The request body can also be retrieved as a QueryMap.
* Added the `handleRequest(HttpRequest)` method.

## v0.5.3+1
- Widen the version constraint for `di`

## v0.5.3
- Improved integration with Shelf
- `shelf.Request.hijack()` method is now supported (although it does not work in unit tests)
- The default error handler now uses the `stack_trace` package to print stack traces.

## v0.5.2
- Fix: Request's state is being improperly cached (see issue #16).

## v0.5.1
- Fix: Correctly handle route exceptions.

## v0.5.0
- Added support for Shelf middlewares and handlers (see [documentation](https://github.com/luizmineo/redstone.dart/wiki/Shelf-Middlewares))
- BREAKING CHANGE: Redstone.dart will no longer serve static files directly. You can use a Shelf handler for this (see [documention](https://github.com/luizmineo/redstone.dart/wiki/Server-Configuration))
- BREAKING CHANGE: It's no longer possible to access `HttpRequest` and `HttpResponse`. If you need to inspect or modify the response, you can use the global `response` object (see [documentation](https://github.com/luizmineo/redstone.dart/wiki/Routes#the-response-object))
- It's now possible to define multiple routes to the same path (see [documentation](https://github.com/luizmineo/redstone.dart/wiki/Routes#http-methods))
- Added `@DefaultRoute` annotation (see [documentation](https://github.com/luizmineo/redstone.dart/wiki/Groups))
- Added `serveRequests(Stream<HttpRequest> requests)` method, which is an alternative to the `start()` method.

## v0.4.0
- Added new annotations: `@Install` and `@Ignore` (see [documentation](https://github.com/luizmineo/redstone.dart/wiki/Importing-libraries))
- Added support for plugins (see [documentation](https://github.com/luizmineo/redstone.dart/wiki/Plugins))

## v0.3.1
- Renamed project to **Redstone.dart**
- New and improved documentation

## v0.3.0
- Added `Route.matchSubPaths` property (see issue #5)
- Added `ErrorHandler.urlPattern` property (check documentation for details)
- Added request attributes (check documentation for details)
- Added support for dependency injection (check documentation for details)

## v0.2.1
- Added support for basic authentication (thanks **Y12STUDIO** for the contribution)
  - Added `parseAuthorizationHeader()` method.
  - Added `authenticateBasic()` method.

## v0.2.0
- BREAKING CHANGES (check documentation for more details):
  - [VirtualDirectory](https://api.dartlang.org/apidocs/channels/stable/dartdoc-viewer/http_server/http_server.VirtualDirectory) is now configured with `jailRoot = true` and `followLinks = false`. You can change these flags through `start()` method.
  - For security and perfomance reasons, the parse of request body is now delayed as much as possible, so interceptors will receive `null` if they call `request.body` (although request.bodyType is still filled). If your interceptor need to inspect the request body, you can set `Interceptor.parseRequestBody = true`.
  - Multipart requests (file uploads) are now refused by default. If your method need to receive multipart requests, you can set `Route.allowMultipartRequest = true`.
  - All arguments of `chain.interrupt()` method are now optional.
- Bug fixes in `abort()`, `redirect()` and `chain.interrupt()` methods. (see issue #3).

## v0.1.2
- Fix: bloodless crashes on Dart 1.3.

## v0.1.1
- Fix: malformed requests can cause a crash

## v0.1.0
- Bug fixes
- BREAKING CHANGE: `chain.next()` now receives a callback, instead of returning a `Future`
- Added new API for unit tests
- Updated documentation

## v0.0.4
- Fix: `chain.interrupt()` is not closing the `HttpResponse` stream

## v0.0.3
- Added a [grinder](http://pub.dartlang.org/packages/grinder) task to properly copy sever's files to the build folder
- Updated documentation with a better approach for building projects

## v0.0.2
- Small fix to VirtualDirectory configuration

## v0.0.1
- First release
