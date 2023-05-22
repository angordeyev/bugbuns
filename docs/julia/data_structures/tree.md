# Tree

```julia
export Node
mutable struct Node
  text::String
  children::Vector{Node}
end
```

```julia
n =
    Node("1", [
        Node("11", [])
        Node("12", [
          Node("121", []),
          Node("122", []),
          Node("123", [])
        ])
    ])
```

```julia
n.children[2].children[3]
```

```output
Node("123", Node[])
```
