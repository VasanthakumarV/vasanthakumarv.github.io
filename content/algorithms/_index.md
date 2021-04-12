+++
title = "Algorithms"
template = "algorithms.html"
+++

# Sorted squared array

Write a function that takes in a non-empty array of integers that are sorted in ascending order and returns a new array of the same length with the squares of the original integers also sorted in ascending order.

```rust
fn sort_squared_slice<const N: usize>(slice: [isize; N]) -> [isize; N] {
    let mut output = [0; N];
    
    let mut small_idx = 0;
    let mut large_idx = slice.len() - 1;
    
    for i in (0..slice.len()).rev() {
        if slice[small_idx].abs() > slice[large_idx].abs() {
            output[i] = slice[small_idx].pow(2);
            small_idx += 1;
        } else {
            output[i] = slice[large_idx].pow(2);
            large_idx = large_idx.saturating_sub(1);
        }
    }
    
    output
}

fn main() {
    let answer = sort_squared_slice([-11, 2, 3, 5, 6, 8, 9]);
    dbg!(&answer);
}
```
