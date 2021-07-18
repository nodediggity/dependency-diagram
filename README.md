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

### 3. Solid line, filled head = "depends on" / "has a" (strong dependency)
![2_0_solid_line_filled_head](https://user-images.githubusercontent.com/25435000/126058841-409698ae-af39-44fc-bc7b-0bf1d3f132d7.png)

A solid line with a filled head denotes a strong dependency.

When a type instance depends on another type instance to exist, it's considered a stronger dependency, such as Association, Aggregation, and Composition.

For example:

```swift
class RemoteFeedLoader {
  private let client: HTTPClient

  init(client: HTTPClient) {
    self.client = client
  }
}
```

![2_1_strong_dependency](https://user-images.githubusercontent.com/25435000/126058872-5dd52ad6-425d-4cd6-9100-e1656f2946f2.png)

The `RemoteFeedLoader` *has an* `HTTPClient`.

You cannot instantiate a `RemoteFeedLoader` without an `HTTPClient` instance. The code wouldn't even compile. So that's a strong dependency.

The `RemoteFeedLoader` depends on an `HTTPClient` to exist.

### 4. Dashed line, filled head = "depends on" (weak dependency)
![3_0_dashed_line_filled_head](https://user-images.githubusercontent.com/25435000/126058925-abd25d37-2358-46f5-8963-09781c30ba67.png)

A dashed line with a filled head denotes a weak dependency.

It's important to note that a type can depend on and use another but still work without one.

For example:

```swift
class RemoteFeedLoader {
  func load(with client: HTTPClient) {
    client.doSomething()
  }
}
```

![3_1_weak_dependency](https://user-images.githubusercontent.com/25435000/126058941-8aefd8d6-0ffa-4710-a54f-3473d8448bc4.png)

The `RemoteFeedLoader` has a source code dependency to the `HTTPClient` because it references and uses it. But it doesn't require an `HTTPClient` instance to exist.

You can create a `RemoteFeedLoader` without an `HTTPClient`.

That's considered a weaker dependency, but still a dependency!

The `RemoteFeedLoader` *uses an* `HTTPClient` dependency in the load method. But it doesn't *have* one. It must be provided as a parameter.

