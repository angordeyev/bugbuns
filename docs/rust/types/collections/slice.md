# Slice

Create a slice from an array:

```rust
{
    let a = [0,1,2,3,4];
    let a_type = std::any::type_name_of_val(&a);
    println!("a type: {a_type}");

    let sl1 = &a[1..2];
    let sl1_type = std::any::type_name_of_val(&sl1);
    println!("sl1 type: {sl1_type}");
    // Array and slice are equal because they implement PartialEq trait
    assert_eq!(sl1, [1]);

    let sl2 = &a[1..];
    let sl2_type = std::any::type_name_of_val(&sl2);
    println!("sl2 type: {sl2_type}");
    assert_eq!(sl2, [1,2,3,4]);
}
```

```output
a type: [i32; 5]
sl1 type: &[i32]
sl1 type: &[i32]
```

