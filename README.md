SwiftRouter
===========

[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)

A URL Router for iOS, written in Swift 2.0, inspired by [HHRouter](https://github.com/Huohua/HHRouter) and [JLRoutes](https://github.com/joeldev/JLRoutes).

## Installation

SwiftRouter is compatible with [Carthage](https://github.com/Carthage/Carthage). Add it to your `Cartfile`:

    github "skyline75489/SwiftRouter"


## Usage
   
### Routing ViewController

Define properties in your custom ViewController:

```swift
class UserViewController: UIViewController {
    var userId:String?
    var username:String?
    var password:String?
}
```

Map URL to ViewController:

```swift
import SwiftRouter

let router = Router.sharedInstance
router.map("/user/:userId", controllerClass: UserViewController.self)
```

Get instance of ViewController directly from the URL. Parameters will be parsed automatically:

```swift
let vc = router.matchController("/user/1?username=hello&password=123")!
XCTAssertEqual(vc.userId, "1")
XCTAssertEqual(vc.username, "hello")
XCTAssertEqual(vc.password, "123")
```


Push custom ViewController:

```swift
router.routeURL("/user/123", navigationController: self.navigationController!)
// The custom ViewController will be pushed with parameters.

```

### Routing handler

Define your custom handler function and map it to URL:

```swift
router.map("/user/add", handler: { (params:[String: String]?) -> (Bool) in
    XCTAssertNotNil(params)
    if let params = params {
        XCTAssertEqual(params["username"], "hello")
        XCTAssertEqual(params["password"], "123")
    }
    return true
})
```

Call the handler from router:

```swift
router.routeURL("/user/add?username=hello&password=123") 
// The handler function will be called with parameters.
```

## License

[MIT License](https://github.com/skyline75489/SwiftRouter/blob/master/LICENSE)

