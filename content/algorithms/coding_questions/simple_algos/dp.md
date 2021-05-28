+++
title = "Dynamic programming"
weight = 2
+++

# Maximum non-adjacent sum

Write a function that takes in an array of positive integers and returns the maximum sum of non-adjacent elements in the array.

If the input array is empty, the function should return 0.

```rust
#![feature(destructuring_assignment)]

fn max_sum_no_adj<const N: usize>(array: [usize; N]) -> usize {
    if array.is_empty() {
        return 0;
    } else if array.len() == 1 {
        return array[0];
    }

    let mut second = array[0];
    let mut first = array[0].max(array[1]);

    for item in array.iter().skip(2) {
        (first, second) = (first.max(second + item), first);
    }

    first
}

fn main() {
    let input = [75, 105, 120, 75, 90, 135];
    let output = max_sum_no_adj(input);
    dbg!(&output);
}
```

# Number of ways to make change

Given an array of distinct positive integers representing coin denominations and a single non-negative integer n representing a target amount of money, write a function that returns the number of ways to make change for that target amount using the given coin denominations.

Note that an unlimited amount of coins is at your disposal.

```rust
fn ways_to_make_change<const N: usize>(n: usize, denoms: [usize; N]) -> usize {
    let mut ways = vec![0; n + 1];

    ways[0] = 1;

    denoms.iter().for_each(|denom| {
        (1..=n).for_each(|amount| {
            if *denom <= amount {
                ways[amount] += ways[amount - denom];
            }
        });
    });

    ways[n]
}

fn main() {
    let output = ways_to_make_change(6, [1, 5]);
    dbg!(&output);
}
```

# Minimum number of coins for change

Given an array of positive integers representing coin denominations and a single non-negative integer n representing a target amount of money, write a function that returns the smallest number of coins needed to make change for (to sum up to) that target amount using the given coin denominations.

Note that you have access to an unlimited amount of coins. In other words, if the denominations are [1, 5, 10], you have access to an unlimited amount of 1s, 5s, and 10s.

If it's impossible to make change for the target amount, return -1. 

```rust
fn min_num_of_coins<const N: usize>(n: usize, denoms: [usize; N]) -> isize {
    let mut num_coins = vec![isize::MAX; n + 1];
    num_coins[0] = 0;

    denoms.iter().for_each(|denom| {
        (0..=n).for_each(|amount| {
            if *denom <= amount {
                num_coins[amount] = std::cmp::min(num_coins[amount], num_coins[amount - denom] + 1);
            }
        });
    });

    if num_coins[n] != isize::MAX {
        return num_coins[n];
    }
    -1
}

fn main() {
    let output = min_num_of_coins(7, [1, 5, 10]);
    dbg!(&output);
}
```
