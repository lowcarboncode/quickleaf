# Quickleaf Cache

Quickleaf Cache is a Rust library that provides a simple and efficient in-memory cache with support for filtering, ordering, and limiting results. It is designed to be lightweight and easy to use.

## Features

- Insert and remove key-value pairs
- Retrieve values by key
- Clear the cache
- List cache entries with support for filtering, ordering, and limiting results
- Custom error handling

## Installation

Add the following to your `Cargo.toml`:

```toml
[dependencies]
quickleaf = "0.1"
```

## Usage

Here's a basic example of how to use Quickleaf Cache:

```rust
use quickleaf::{Quickleaf, ListProps, Order, Filter};

fn main() {
    let mut cache = Quickleaf::new(2);
    cache.insert_str("key1", 1);
    cache.insert_str("key2", 2);
    cache.insert_str("key3", 3);

    assert_eq!(cache.get("key1"), None);
    assert_eq!(cache.get("key2"), Some(&2));
    assert_eq!(cache.get("key3"), Some(&3));

    let list_props = ListProps::default()
        .order(Order::Asc)
        .limit(10);

    let result = cache.list(list_props).unwrap();
    for (key, value) in result {
        println!("{}: {}", key, value);
    }
}
```

### Using Filters

You can use filters to narrow down the results when listing cache entries. Here are some examples:

#### Filter by Start With

```rust
use quickleaf::{Quickleaf, ListProps, Order, Filter};

fn main() {
    let mut cache = Quickleaf::new(10);
    cache.insert_str("apple", 1);
    cache.insert_str("banana", 2);
    cache.insert_str("apricot", 3);

    let list_props = ListProps::default()
        .order(Order::Asc)
        .filter(Filter::StartWith("ap"))
        .limit(10);

    let result = cache.list(list_props).unwrap();
    for (key, value) in result {
        println!("{}: {}", key, value);
    }
}
```

#### Filter by End With

```rust
use quickleaf::{Quickleaf, ListProps, Order, Filter};

fn main() {
    let mut cache = Quickleaf::new(10);
    cache.insert_str("apple", 1);
    cache.insert_str("banana", 2);
    cache.insert_str("pineapple", 3);

    let list_props = ListProps::default()
        .order(Order::Asc)
        .filter(Filter::EndWith("apple"))
        .limit(10);

    let result = cache.list(list_props).unwrap();
    for (key, value) in result {
        println!("{}: {}", key, value);
    }
}
```

#### Filter by Start And End With

```rust
use quickleaf::{Quickleaf, ListProps, Order, Filter};

fn main() {
    let mut cache = Quickleaf::new(10);
    cache.insert_str("applemorepie", 1);
    cache.insert_str("banana", 2);
    cache.insert_str("pineapplepie", 3);

    let list_props = ListProps::default()
        .order(Order::Asc)
        .filter(Filter::StartAndEndWith("apple", "pie"))
        .limit(10);

    let result = cache.list(list_props).unwrap();
    for (key, value) in result {
        println!("{}: {}", key, value);
    }
}
```

## Modules

### `error`

Defines custom error types used in the library.

### `filter`

Defines the `Filter` enum used for filtering cache entries.

### `list_props`

Defines the `ListProps` struct used for specifying properties when listing cache entries.

### `quickleaf`

Defines the `Quickleaf` struct which implements the cache functionality.

## Running Tests

To run the tests, use the following command:

```sh
cargo test
```

## License

This project is licensed under the Apache 2.0 License. See the [LICENSE](LICENSE) file for more information.
