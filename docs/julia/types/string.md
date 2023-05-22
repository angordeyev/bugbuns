# Strings

## Interpolation

```julia
x = 1 
y = "Hello $x"
```
```output
"Hello 1"
```

## Subsrings compatible with Unicode

```julia
function substr_first_last(string::String, first:: Integer, last:: Integer)
  indexes = collect(eachindex(string))
  first = indexes[first]
  last = indexes[last]
  string[first:last]
end

function substr_first_count(string, first, count)
  indexes = collect(eachindex(string))
  first = indexes[first]
  last = indexes[first + count - 1]
  string[first:last]
end


```
