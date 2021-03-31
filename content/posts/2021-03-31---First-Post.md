---
title: "First Post"
date: "2021-03-31"
template: "post"
draft: false
slug: ""
category: "misc"
tags:
  - "misc"
  - "Gatsby"
description: "gatsbyの練習"
socialImage: "me.png"
---

# 最初
いろいろ試す
## h2
### h3
#### h4
##### h5
- hoge
- hoge2
- **hgoe**
- `hoge`

```python
# python
m = 'post'
print(f'first {post}')
```

```rust
# rust
fn main() -> Result<()> {
  println!("first {}", "post");
}
```

```go
package main

import "fmt"

func main() {
  desc := "first post"
  fmt.Println(desc)
}
```

## Fermet's little theorem[^1]
if $p$ is a prime number, any interger a is coprime to p:

$a^{p-1} \equiv 1 \mod p$

## Euler's criterion[^2]
if $p$ is a prime number, any interger a is coprime to p:

$$
a ^ {\frac{p-1}{2}} \equiv
\begin{cases}
  1 & \mod p \text{ (if exist } x \text{ such that } a \equiv x^2 \text{ )} \\
  -1 & \mod p \text{ (if not exist } x \text{ such that } a \equiv x^2 \text{ )}
\end{cases}
$$

[^1]: https://en.wikipedia.org/wiki/Fermat%27s_little_theorem
[^2]: https://en.wikipedia.org/wiki/Euler%27s_criterion
