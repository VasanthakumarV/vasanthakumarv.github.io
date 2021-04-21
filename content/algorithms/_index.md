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

# Tournament winner 

There's an algorithms tournament taking place in which teams of programmers compete against each other to solve algorithmic problems as fast as possible. Teams compete in a round robin, where each team faces off against all other teams. Only two teams compete against each other at a time, and for each competition, one team is designated the home team, while the other team is the away team. In each competition there's always one winner and one loser; there are no ties. A team receives 3 points if it wins and 0 points if it loses. The winner of the tournament is the team that receives the most amount of points.

```rust
use std::collections::HashMap;

const POINTS: usize = 3;
const WIN_FLAG: usize = 1;

fn tournament_winner<'a, const N: usize>(
    competitions: [(&'a str, &'a str); N],
    results: [usize; N],
) -> &'a str {
    let mut best_team = ("", 0);
    let mut tracker = HashMap::new();

    competitions
        .iter()
        .enumerate()
        .for_each(|(i, (home_team, away_team))| {
            let winning_team = match results[i] {
                WIN_FLAG => home_team,
                _ => away_team,
            };

            if let Some(value) = tracker.get_mut(winning_team) {
                *value += POINTS;

                if *value > best_team.1 {
                    best_team = (winning_team, *value);
                }
            } else {
                tracker.insert(winning_team, POINTS);
            }
        });

    best_team.0
}

fn main() {
    let winner = tournament_winner(
        [("html", "c#"), ("c#", "python"), ("python", "html")],
        [0, 0, 1],
    );
    dbg!(&winner);
}
```

# Non-constructible change

Given an array of positive integers representing the values of coins in your possession, write a function that returns the minimum amount of change (the minimum sum of money) that you cannot  create. The given coins can have any positive integer value and aren't necessarily unique (i.e., you can have multiple coins of the same value).


```rust
fn non_constructible_change<const N: usize>(mut coins: [usize; N]) -> usize {
    coins.sort_unstable();

    coins.iter().fold(0, |change_created, coin| {
        if *coin > change_created + 1 {
            return change_created + 1;
        }

        change_created + 1
    })
}

fn main() {
    let answer = non_constructible_change([1, 2, 4]);
    dbg!(&answer);
}
```

# Minimum waiting time

You're given a non-empty array of positive integers representing the amounts of time that specific queries take to execute. Only one query can be executed at a time, but the queries can be executed in any order.

A query's waiting time is defined as the amount of time that it must wait before its execution starts. In other words, if a query is executed second, then its waiting time is the duration of the first query; if a query is executed third, then its waiting time is the sum of the durations of the first two queries.

```rust
fn min_wait_time<const N: usize>(mut queries: [usize; N]) -> usize {
    queries.sort_unstable();

    queries
        .iter()
        .enumerate()
        .fold(0, |mut wait_time, (i, duration)| {
            let queries_left = queries.len() - (i + 1);
            wait_time += duration * queries_left;
            wait_time
        })
}

fn main() {
    let input = [3, 2, 1, 2, 6];
    let answer = min_wait_time(input);
    dbg!(&answer);
}
```

# Array of products

Write a function that takes in a non-empty array of integers and returns an array of the same length, where each element in the output array is equal to the product of every other number in the input array.

```rust
fn array_of_prods<const N: usize>(array: [isize; N]) -> [isize; N] {
    let mut prods = [1; N];

    let _ = array
        .iter()
        .enumerate()
        .fold(1, |mut left_running, (i, value)| {
            prods[i] = left_running;
            left_running *= value;
            left_running
        });

    let _ = array
        .iter()
        .enumerate()
        .rev()
        .fold(1, |mut right_running, (i, value)| {
            prods[i] *= right_running;
            right_running *= value;
            right_running
        });

    prods
}

fn main() {
    let answer = array_of_prods([5, 1, 4, 2]);
    dbg!(&answer);
}
```

# First duplicate value

Given an array of integers between 1 and n, inclusive, where n is the length of the array, write a function that returns the first integer that appears more than once (when the array is read from left to right).

In other words, out of all the integers that might occur more than once in the input array, your function should return the one whose first duplicate value has the minimum index.

If no integer appears more than once, your function should return -1.

```rust
fn first_dup_value<const N: usize>(mut array: [isize; N]) -> isize {
    for value in std::array::IntoIter::new(array) {
        let abs_value = value.abs();

        if array[abs_value as usize] < 0 {
            return abs_value;
        }

        array[abs_value as usize] *= -1;
    }

    -1
}

fn main() {
    let answer = first_dup_value([2, 1, 5, 3, 3, 2, 4]);
    dbg!(&answer);
}
```

# Merge overlapping intervals

Write a function that takes in a non-empty array of arbitrary intervals, merges any overlapping intervals, and returns the new intervals in no particular order.

Each interval interval is an array of two integers, with interval[0] as the start of the interval and interval[1] as the end of the interval.

Note that back-to-back intervals aren't considered to be overlapping. For example, [1, 5] and [6, 7] aren't overlapping; however, [1, 6] and [6, 7] are indeed overlapping.

Also note that the start of any particular interval will always be less than or equal to the end of that interval. 

```rust
fn merge_overlapping<const N: usize, const M: usize>(
    mut intervals: [[usize; M]; N],
) -> Vec<[usize; M]> {
    intervals.sort_by_key(|k| k[0]);
    
    let mut current = intervals[0];

    let mut output =
        intervals
            .iter()
            .skip(1)
            .fold(Vec::with_capacity(intervals.len()), |mut output, next| {
                if current[1] >= next[0] {
                    current[1] = std::cmp::max(current[1], next[1]);
                } else {
                    output.push(current);
                    current = *next;
                }

                output
            });
    output.push(current);

    output
}

fn main() {
    let input = [[1, 2], [3, 5], [4, 7], [6, 8], [9, 10]];
    let output = merge_overlapping(input);
    dbg!(&output);
}
```
