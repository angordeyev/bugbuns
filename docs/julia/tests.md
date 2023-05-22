# Tests

## Create Tests

Add `Tests` package

```sh
(MyProject) pkg> add Test
```

Create `test/runtests.jl` file with the following content

```julia
using SomeProject
using Test

@testset "Test 1" begin
    @test true
end

@testset "Test 2 " begin
    @test false
end
```

Activate the project

```sh
(MyProject) pkg> activate .
```
our run the project using `julia --project=.`

## Run tests

```sh
(MyProject) pkg> test
```

```output
Test Summary: | Pass  Total  Time
Test 1        |    1      1  0.0s
Test 2 : Test Failed at MyProject/test/runtests.jl:9
```
