+++
title = "Einops"
weight = 1

[extra]
links = [
	{ label = "github-link", link = "https://github.com/VasanthakumarV/einops" },
	{ label = "docs-link", link = "https://docs.rs/einops/0.1.0/einops/" },
	{ label = "crates-link", link = "https://crates.io/crates/einops" },
]
+++

This is a rust port of the incredible [einops](https://github.com/arogozhnikov/einops) library.

Einops provides flexible and powerful api to represent tensor operations in a readable and reliable way.

__Example__

```rust
// We create a random tensor as input
let input = Tensor::randn(&[100, 32, 64], (Kind::Float, Device::Cpu));

// Rearrange operation
let output = Rearrange::new("t b c -> b c t")?.apply(&input)?;
assert_eq!(output.size(), vec![32, 64, 100]);
```
