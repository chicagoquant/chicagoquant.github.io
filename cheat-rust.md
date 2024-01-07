
# Rust

### Rust build commands
```shell
cargo new proj
cargo build
cargo run
cargo check
cargo build --release

rustc main.rs
```

### Rust Basics
```rust
fn main() { println!("Hello world!"); }

let val = 10;                                   // immutable
assert_eq(val, 10);
assert!(val == 10);

println!("val={}", val);
let val: i64 = 10;                              // with specified type

// data types, scalars
u8, u16, u32, u64, u128, usize                  // usize - architecture dependent 64-bit vs 32-bit
i8, i16, i32, i64, i128, isize                  // default integer type is: i32
f32, f64                                        // default f64
bool                                            // true, false
char                                            // 4-bytes, unicode scalar value. 'a'

// compound data types
let tup: (i32, f64, char) = (500, 6.9, 'A');    // tuple
let (x, y, z) = tup;                            // destructuring
tup.0, tup.1, tup.2                             // indexing
()                                              // empty tuple, called 'unit'

let arr = [1, 2, 3, 4];
let arr = [100; 5];                             // [ 100, 100, 100, 100 ], repeat 100 x 5 times

for i in 0..5 { ... }                           // [from, to)
if i%2 == 0 { ... } else { ... }

let mut sum = 0;                                // mutable
sum += 10;

i as f64;                                       // cast int to float

fn sqr(x: f64) -> f64 { x*x }                   // fn with param and return type, last expression in {} is returned
fn sqr(x: f64) -> f64 { return x*x; }

fn by_ref(x: &i32) -> i32 { *x+1 }              // ref: &v, deref: *v, immutable
let i = 10;
by_ref(&i);

fn square_it(x: &mut f64) { *x *= *x; }         // mutable ref

let f: f64 = 1.0;
f.cos()
f.abs()

use std::f64::consts;
consts::PI;

let arr = [1,2,3,4];                            // array type is [i32; 4], [type; len]
arr[i];
arr.len()
println!("arr: {:?}", arr);                     // debug print for array
let slice = &arr[i..j];
let slice = &arr;
let slice = &arr[i..];

for x in arr { ... }

fn sum(arr: &[i32]) -> i32 { ... }              // passing array/slice to a function
sum(&arr);                                      // & is called "borrow", means pass by reference, borrowed from original owner
sum(&arr[2..3]);                                // calling fn with array/slice

let arr = [1,2,3,4,5,6];
let item_ref = arr.get(i);                      // returns Option<&i32> (containing a reference to i32) -- Some / None
let first_ref = arr.get(0);                     // first: Some(1)
let last_ref = arr.get(100);                    // last: None
first_ref.is_some()                             // true
last_ref.is_none()                              // true
*first_ref.unwrap()                             // value stored in Some is &i32, dereference with *
*first_ref.unwrap_or(&-1)                       // will return value in first or if it is None, then will return -1

let mut v = Vec::new();
v.push(10);
v.pop();
v.extend(10..60);
v.insert(3, 200);                               // inefficient
v.remove(10);                                   // inefficient
v.clear();                                      // size = 0, capacity = unchanged
v.sort();                                       // in-place sorting
v.dedup();
let v_copy = v.clone();

let first = v[0];
let maybe_first = v.get(0);                     // Option<&i32>
sum(&v);                                        // Vector converts to slice[i32], coercing Vec<T> -> &[T]
let slice = &v[1..];                            // slice borrows the memory owned by Vector, vec manages lifetime of memory

let iter = 0..10;
iter.next()
assert!(iter.next() == Some(0));
assert!(Iter.next() == None);

let iter = arr.iter();
for i in arr.iter() { ... }
for i in slice { ... }

let s1: i32 = (0..5).sum();
let s2: i32 = [10, 20, 30].iter().sum();
let s3: i32 = arr.iter().sum();
let s4: i32 = slice.iter().sum();

for w in slice.windows(5) { ... }               // w is a sub-slice of size 5, we get sliding windows in the loop

for c in slice.chunks(4) { ... }                // c is a sub-slice of size 4, we get disjoint chunks

let v1 = vec![10, 20, 30, 40];
assert_eq(v1, &[10, 20, 30, 40]);

// String vs &str (string slice)                String = Vec<u8>    &str = &[u8]
let text = "hello world";
dump(text);
let s = text.to_string();                       // String
dump(&s);                                       // String s coerced to &str

fn dump(s: &str) {                              // takes a string slice &str, not String
  println!("str: '{}'", s);
}

s.push('A');
s.push_str("ha!");
s += "ahoy!";
s += &s2.to_string();                           // += needs a &str, to_string() returns String
s.pop();
assert_eq!(s, "abcd");

let text_slice = &text[1..];
let string_slice = &s[1..];

let char_iter = text.chars();
char_iter.count();
text.chars().count();
for ch in text.chars() { ... }                    // ch is 4-byte unicode code point, char type

text.len();
let maybe = text.find('w');
if maybe.is_some() { &text[maybe.unwrap()..] }
&text[from..to]                                   // only use from, to returned by a string method like find(),
                                                  // should align with unicode char boundary

let words: Vec<&str> = text.split_whitespace().collect(); // collect() needs a cue, to return Vec<&str>, infers from type
let stripped: String =
        text.chars()                              // iterator
          .filter(|ch| !ch.is_whitespace())       // closure (aka lambda or anonymous function)
          .collect()                              // cue is to return String
        ;

for arg in std::env::args() { ... }
let args: Vec<String> = std::env::args().skip(1).collect();
if args.len() > 0 { ... }

use std::env;
let first_arg = env::args().nth(1).expect("Required argument not found");
                                                    // .expect() is like unwrap(), but with a readable message
let n: i32 = first_arg.parse().expect("Expected an integer arg");
                                                    // convert string to number

match text.find('h') {
  Some(idx) => { ... text[idx..]} ... },
  None => { ... some message ... }
};

if let Some(idx) = text.find('h') {
  ... text[idx..] ...
}
else {
  ... some message ...
}

let text = match n {
  0 => "zero",
  1 => "one",
  2 => "two",
  _ => "many",
};

let text = match r {
  0...3 => "small",
  4...6 => "medium",
  _ => "large",
};

use std::fs::File;
use std::io::Read;

let mut file = File::open(&filename).expect("failed to open the file");
let mut data = String::new();
file.read_to_string(&mut data).expect("cannot read the file");
data.len();
file.read_to_end()

// Option = Some | None, use unwrap(), expect()
// Result = Ok | Error, can use unwrap(), expect()   -- example: Result<i32, String>, Result<String, io::Error>

use std::env;
use std::fs::File;
use std::io::Read;
use std::io;

fn read_to_string(filename: &str) -> io::Result<String> {       // io::Result<T> is same as Result<T, io::Error>
  let mut file = File::open(&filename)?;                        // note: ? operator, returns on error
  let mut text = String::new();
  file.read_to_string(&mut text)?;                              // note: ? operator, returns on error
  Ok(text)                                                      // no errors, so return io::Result = Ok(string)
}

// equivalent to this expanded version
fn read_to_string(filename: &str) -> Result<String, io::Error> {
  let mut file = match File::open(&filename) {
    Ok(f) => f,                                                 // file handle f
    Err(e) => return Err(e),                                    // return if failed to open file
  };
  let mut text = String::new();
  match file.read_to_string(&mut text) {
    Ok(_) => Ok(text),
    Err(e) => Err(e),
  }
}

let mut input_str = String::new();
io::stdin()
    .read_line(&mut input_str)
    .expect("Failed to read line")
  ;
let num: i64 = input_str
    .trim()
    .parse()
    .expect("Failed to parse number")
  ;

// https://stevedonovan.github.io/rust-gentle-intro/1-basics.html

// https://stevedonovan.github.io/rust-gentle-intro/2-structs-enums-lifetimes.html
```

### More rust things
```rust
struct User {
  active: bool,
  username: String,
  email: String,
  sign_in_count: u64,
}

fn main() {
  let user1 = User {
    active: true,
    username: String::from("james smith"),
    email: String::from("nospam@gmail.com"),
    sign_in_count: 1,
  };
}
```
