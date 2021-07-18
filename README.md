# dependency-diagram
Visualizing the dependency graph

## Writing/Reading Dependency Diagrams
There are different types of dependency you can represent in a dependency diagram using different annotations, lines, and arrows. 

Here are the main ones:

### 1. Solid line, empty head = "inherits from" / "is a".
![0_0_solid_line_empty_head](https://user-images.githubusercontent.com/25435000/126058742-648cf3d9-a477-4b12-868b-9ddf6eda63df.png)

  
A solid line with an empty head denotes that a class inherits from another class.

For example:
```swift
class MyViewController: UIViewController { ... }
```
The `MyViewController` class inherits from the `UIViewController` class, or the `MyViewController` "is a" subtype of `UIViewController`.
![0_1_inheritance](https://user-images.githubusercontent.com/25435000/126058749-52af2f95-7a7e-4de1-aede-90a3bde205df.png)

### 2. Dashed line, empty head = "conforms to" or "implements"
![1_0_dashed_line_empty_head](https://user-images.githubusercontent.com/25435000/126058791-49d1836b-f20c-444a-ab5f-0157f5f588d4.png)

A dashed line with an empty head denotes that a component conforms/implements a protocol/abstract interface.

For example:

```swift
protocol HTTPClient { ... }

class URLSessionHTTPClient: HTTPClient { ... }
```
![1_1_conformance](https://user-images.githubusercontent.com/25435000/126058809-f20d58c1-4f68-4848-b94e-e86a902a2ca1.png)

The `URLSessionHTTPClient` conforms to the `HTTPClient` protocol.

